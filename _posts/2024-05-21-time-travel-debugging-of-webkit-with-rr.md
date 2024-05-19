---
layout: post
title: "Time travel debugging of WebKit with rr"
tags: debugging rr webkit igalia
---

## Introduction

[rr](https://rr-project.org/) is a debugging tool for Linux that was originally developed by Mozilla for [Firefox](https://firefox-source-docs.mozilla.org/contributing/debugging/debugging_firefox_with_rr.html).
It has long been adopted by Igalia and other web platform developers for [Chromium](https://developer.chrome.com/blog/chromium-chronicle-13) and WebKit too.
Back in 2019, there were breakout sessions on this topic at the [Web Engines Hackfest](https://blogs.igalia.com/mrego/2019/11/14/web-engines-hackfest-2019/#debugging-tools) and [BlinkOn](https://www.youtube.com/watch?v=pV7AYofV95A&t=565s).

For WebKitGTK, the Flatpak SDK provides a copy of rr, but recently I was unable to use the [instructions on trac.webkit.org](https://trac.webkit.org/wiki/WebKitFlatpakSDK/DebugWithRR).
Fortunately, my colleague [Adrián Pérez](https://www.igalia.com/team/aperez) suggested using a direct build without [flatpak](https://flatpak.org/) or the [bubblewrap](https://github.com/containers/bubblewrap) sandbox, and that indeed solved my problem.
I thought it might be interesting to share this information with others, so I decided to write this blog post.

**Disclaimer: The build instructions below may be imperfect, will likely become outdated, and are in any case not a replacement for the [official ones for WebKitGTK development](https://trac.webkit.org/wiki/BuildingGtk#BuildingWebKitGTKfromgit).
Use them at your own risk!**

## CMake configuration

The approach that worked for me was thus to perform a direct build from my system.
I came up with the following configuration step:

```bash
cmake -S. -BWebKitBuild/Release \
   -DCMAKE_BUILD_TYPE=Release \
   -DCMAKE_INSTALL_PREFIX=$HOME/WebKit/WebKitBuild/install/Release \
   -GNinja -DPORT=GTK -DENABLE_BUBBLEWRAP_SANDBOX=OFF \
   -DDEVELOPER_MODE=ON -DDEVELOPER_MODE_FATAL_WARNINGS=OFF \
   -DENABLE_TOOLS=ON -DENABLE_LAYOUT_TESTS=ON
```

where:

* The `-B` option specifies the build directory, which is traditionnaly called `WebKitBuild/` for the WebKit project.
* [CMAKE_BUILD_TYPE](https://cmake.org/cmake/help/latest/variable/CMAKE_BUILD_TYPE.html) specifies the build type, e.g. optimized release builds (`Release`, corresponding to `--release` for the offical script) or debug builds with assertions (`Debug`, corresponding to `--debug`) [^2].
* [CMAKE_INSTALL_PREFIX](https://cmake.org/cmake/help/latest/variable/CMAKE_INSTALL_PREFIX.html) specifies the installation directory, which I place inside `WebKitBuild/install/` [^1].
* The `-G` option specifies the build system generator. I used [Ninja](https://ninja-build.org/), which is the default for the offical script too.
* `-DPORT=GTK` is for building WebKitGTK. I haven't tested rr with other Linux ports.
* `-DENABLE_BUBBLEWRAP_SANDBOX=OFF` was suggested by Adrián. The bubblewrap sandbox probably does not make sense without flatpak, so it should be safe to disable it anyway.
* I extracted the other `-D` flags from the official script, trying to stay as close as possible to what it provides for WebKit development (being able to run layout tests, building the `Tools/`, ignoring fatal warnings, etc).

Needless to say, the advantage of using flatpak is that it automatically downloads and install all the required dependencies.
But if you do your own build, you need to figure out what they are and perform the setup manually.
Generally, this is straightforward using your distribution's package manager, but there can be some tricky exceptions [^3].

While we are still at the configuration step, I believe it's worth sharing two more tricks for WebKit developers:

* You can use `-DENABLE_SANITIZERS=address` to produce [Asan builds](https://searchfox.org/wubkat/rev/16f147d06627e9accc8fa041ccc0f639b5c510cf/Tools/Scripts/webkitdirs.pm#2719) or builds with other [sanitizers](https://github.com/google/sanitizers).
* You can use `-DCMAKE_CXX_FLAGS="-DENABLE_TREE_DEBUGGING"` in release builds if you want to get access to the [tree debugging functions](https://searchfox.org/wubkat/search?q=ENABLE(TREE_DEBUGGING)) (`ShowRenderTree` and the like). This flag is turned on by default for debug builds.

## Building and running WebKit

Once the configure step is successful, you can build and install WebKit using the following CMake command [^1].

```bash
cmake --build WebKitBuild/Release --target install
```

When that operation completes, you should be able to run `MiniBrowser` with the following command:

```bash
LD_LIBRARY_PATH=WebKitBuild/install/Release/lib ./WebKitBuild/Release/bin/MiniBrowser
```

For `WebKitTestRunner`, some extra environment variables are necessary [^1]:

```bash
TEST_RUNNER_INJECTED_BUNDLE_FILENAME=$HOME/WebKit/WebKitBuild/Release/lib/libTestRunnerInjectedBundle.so LD_LIBRARY_PATH=WebKitBuild/install/Release/lib ./WebKitBuild/Release/bin/WebKitTestRunner filename.html
```

You can also use the official scripts, `Tools/Script/run-minibrowser` and `Tools/Script/run-webkit-tests`.
They expect some particular paths, but a quick workaround is to use a symbolic link:

```bash
ln -s $HOME/WebKit/WebKitBuild $HOME/WebKit/WebKitBuild/GTK
```

## Using rr for WebKit debugging

rr is generally easily installable from your distribution's package manager.
However, as stated on [the project wiki page](https://github.com/rr-debugger/rr/wiki/Building-And-Installing):

> Support for the latest hardware and kernel features may require building rr from Github master.

Indeed, using the source has always worked best for me to avoid mysterious execution failures when starting the recording [^4].

If you are not familiar with rr, I strongly invite you to take a look at the overview on the [project home page](https://rr-project.org/) or at some of the references I mentioned in the introduction.
In any case, the first step is to record a trace by passing the program and arguments to rr.
For example, to record a trace for `MiniBrowser`:

```bash
LD_LIBRARY_PATH=WebKitBuild/install/Debug/lib rr ./WebKitBuild/Debug/bin/MiniBrowser https://www.igalia.com/
```

After the program exits, you can replay the recorded trace as many times as you want.
For hard-to-reproduce bugs (e.g. non-deterministic issues or involving a lot of manual steps), that means you only need to be able to record and reproduce the bug once and then can just focus on debugging.
You can even turn off your machine after hours of exhausting debugging, then continue the effort later when you have more time and energy!
The trace is played in a deterministic way, always using the same timing and pointer addresses.
You can use most gdb commands (to run the program, interrupt it, and inspect data), but the real power comes from new commands to perform reverse execution!

Before coming to that, let's explain how to handle programs with multiple processes, which is the case for WebKit and modern browsers in general.
After you recorded a trace, you can display the pids of all recorded processes using the `rr ps` command.
For example, we can see in the following output that the MiniBrowser process (pid 24103) actually forked three child processes, including the Network Process (pid 24113) and the Web Process (24116):

```bash
PID     PPID    EXIT    CMD
24103   --      0       ./WebKitBuild/Debug/bin/MiniBrowser https://www.igalia.com/
24113   24103   -9      ./WebKitBuild/Debug/bin/WebKitNetworkProcess 7 12
24115   24103   1       (forked without exec)
24116   24103   -9      ./WebKitBuild/Debug/bin/WebKitWebProcess 15 15
```

Here is a small debugging session similar to the single-process example from [Chromium Chronicle #13](https://developer.chrome.com/blog/chromium-chronicle-13) [^5].
We use the option `-p 24116` to attach the debugger to the Web Process and `-e` to start debugging from where it exited:

```bash
rr replay -p 24116 -e
(rr) break RenderFlexibleBox::layoutBlock
(rr) rc # Run back to the last layout call
Thread 2 hit Breakpoint 1, WebCore::RenderFlexibleBox::layoutBlock (this=0x7f66699cc400, relayoutChildren=false) at /home/fred/src-obj/WebKit/Source/WebCore/rendering/RenderFlexibleBox.cpp:420
(rr) # Inspect anything you want here. To find the previous Layout call on this object:
(rr) cond 1 this == 0x7f66699cc400
(rr) rc
Thread 2 hit Breakpoint 1, WebCore::RenderFlexibleBox::layoutBlock (this=0x7f66699cc400, relayoutChildren=false) at /home/fred/src-obj/WebKit/Source/WebCore/rendering/RenderFlexibleBox.cpp:420
420     {
(rr) delete 1
(rr) watch -l m_style.m_nonInheritedFlags.effectiveDisplay # Or find the last time the effective display was changed
Thread 4 hit Hardware watchpoint 2: -location m_style.m_nonInheritedFlags.effectiveDisplay

Old value = 16
New value = 0
0x00007f6685234f39 in WebCore::RenderStyle::RenderStyle (this=0x7f66699cc4a8) at /home/fred/src-obj/WebKit/Source/WebCore/rendering/style/RenderStyle.cpp:176
176     RenderStyle::RenderStyle(RenderStyle&&) = default;
```

`rc` is an abbreviation for `reverse-continue` and continues execution backward.
Similarly, you can use `reverse-next`, `reverse-step` and `reverse-finish` commands, or their abbreviations.
Notice that the watchpoint change is naturally reversed compared to normal execution: the old value (sixteen) is the one after intialization, while the new value (zero) is the one before initialization!

## Restarting playback from a known point in time

rr also has a concept of "event" and associates a number to each event it records.
They can be obtained by the `when` command, or printed to the standard output using the `-M` option.
To elaborate a bit more, suppose you add the following `printf` in `RenderFlexibleBox::layoutBlock`:

```diff
@@ -423,6 +423,8 @@ void RenderFlexibleBox::layoutBlock(bool relayoutChildren, LayoutUnit)
     if (!relayoutChildren && simplifiedLayout())
         return;

+    printf("this=%p\n", this);
+
```

After building, recording and replaying again, the output should look like this:

```bash
$ rr -M replay -p 70285 -e # replay with the new PID of the web process.
...
[rr 70285 57408]this=0x7f742203fa00
[rr 70285 57423]this=0x7f742203fc80
[rr 70285 57425]this=0x7f7422040200
...
```

Each printed output is now annotated with two numbers in bracket: a PID and an event number.
So in order to restart from when an interesting output happened (let's say `[rr 70285 57425]this=0x7f7422040200`), you can now execute `run 57425` from the debugging session, or equivalently:

```bash
rr replay -p 70285 -g 57425
```

## Older traces and parallel debugging

Another interesting thing to know is that traces are stored in `~/.local/share/rr/` and you can always specify an older trace to the rr command e.g. `rr ps ~/.local/share/rr/MiniBrowser-0`.
Be aware that the [executable image must not change](https://github.com/rr-debugger/rr/wiki/Usage#limitations), but you can use `rr pack` to be able to run old traces after a rebuild, or even to copy traces to another machine.

To be honest, most the time I'm just using the latest trace.
However, one thing I've sometimes found useful is what I would call the "parallel debugging" technique.
Basically, I'm recording one trace for a testcase that exhibits the bug and another one for a very similar testcase (e.g. with one CSS property difference) that behaves correctly.
Then I replay the two traces side by side, comparing them to understand where the issue comes from and what can be done to fix it.

The [usage documentation](https://github.com/rr-debugger/rr/wiki/Usage) also provides further tips, but this should be enough to get you started with time travel debugging in WebKit!


[^1]: Using an installation directory might not be necessary, but without that, I had trouble making the whole thing work properly (wrong libraries loaded or libraries not found).
[^2]: `RelWithDebInfo` build type (which yields an optimized release build with debug symbols) might also be interesting to consider in some situations, e.g. debugging bugs that reproduce in release builds but not in debug builds.
[^3]: In my case, I chose the easiest path to disable some features, namely `-DUSE_JPEGXL=OFF`, `-DUSE_LIBBACKTRACE=OFF`, and `-DUSE_GSTREAMER_TRANSCODER=OFF`.
[^4]: Incidentally, you are likely to get an error saying that [perf_event_paranoid](https://docs.kernel.org/admin-guide/sysctl/kernel.html#perf-event-paranoid) is required to be at most 1, which you can force using `sudo sysctl kernel.perf_event_paranoid=1`.
[^5]: The equivalent example would probably have been to watch for the previous style change with `watch -l m_style`, but this was exceeding my hardware watchpoint limit, so I narrowed it down to a smaller observation scope.
