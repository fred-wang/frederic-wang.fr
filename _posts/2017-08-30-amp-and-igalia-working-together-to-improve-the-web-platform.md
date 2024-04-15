---
layout: post
title: "The AMP Project and Igalia working together to improve WebKit and the Web Platform"
tags: igalia webkit
---

{% raw %}

  <h2 id="tldr">TL;DR</h2>

<p><a href="https://www.ampproject.org/">The AMP Project</a> and
<a href="https://www.igalia.com/">Igalia</a>
have recently been collaborating to
improve <a href="http://webkit.org/">WebKit</a>’s implementation of
the <a href="https://platform.html5.org/">Web platform</a>.
Both teams are committed to make the Web better and we expect
that all developers and users will benefit from this effort.
In this blog post, we review some of the bug fixes and features currently being
considered:</p>

<ul>
  <li>
    <p><strong>Frame sandboxing</strong>: Implementing sandbox values to allow trusted
third-party resources to open unsandboxed popups
or restrict unsafe operations of malicious ones.</p>
  </li>
  <li>
    <p><strong>Frame scrolling on iOS</strong>: Trying to move to a more standard and
 interoperable approach via <code class="language-plaintext highlighter-rouge">iframe</code> elements; addressing miscellaneous
 issues with scrollable nodes (e.g. visual artifacts while scrolling, view
 not scrolled when using “Find Text”…).</p>
  </li>
  <li>
    <p><strong>Root scroller</strong>: Finding a solution to the
<a href="https://bugs.webkit.org/show_bug.cgi?id=5991">old interoperability issue</a>
about how to scroll the main frame; considering a
<a href="https://github.com/bokand/NonDocumentRootScroller">new rootScroller API</a>.</p>
  </li>
</ul>

<p>Some demo pages for <a href="https://webkit.org/demos/frames/">frame sandboxing and scrolling</a> are also available if you wish to test features discussed in this blog post.</p>

<h2 id="introduction">Introduction</h2>

<p>AMP is an open-source project to enable websites and ads that are consistently fast, beautiful and high-performing across devices and distribution platforms.
Several interoperability bugs and missing features in WebKit have
caused problems to AMP users and to Web developers in general. Although
it is possible to add platform-specific workarounds to AMP, the best way to
help the Web Platform community is to directly fix these issues in WebKit,
so that everybody can benefit from these improvements.</p>

<p>Igalia is a consulting company with a team dedicated to Web Platform
developments in
all open-source Web Engines (Chromium, WebKit, Servo, Gecko) working
in the implementation and standardization of miscellaneous technologies
(CSS Grid/flexbox, ECMAScript, WebRTC, WebVR, ARIA, MathML, etc).
Given this expertise,
the AMP Project sponsored Igalia so that they can lead these
developments in WebKit. It is worth noting that this project aligns with the
<a href="https://www.chromium.org/blink/platform-predictability">Web Predictability effort</a> supported by both Google and Igalia, which aims at making the Web more
predictable for developers. In particular, the following aspects are considered:</p>

<ul>
  <li>Interoperability: Effort is made to write
<a href="https://github.com/w3c/web-platform-tests">Web Platform Tests</a> (WPT), to follow
<a href="https://platform.html5.org/">Web standards</a> and ensure consistent behaviors
between web engines or operating systems.</li>
  <li>Compatibility: Changes are carefully analyzed using telemetry techniques or
user feedback in order to avoid breaking compatibility with previous versions
of WebKit.</li>
  <li>Reducing footguns: Removals of non-standard features (e.g. CSS vendor prefixes) are attempted while new features are carefully introduced.</li>
</ul>

<p>Below we provide further description of the WebKit
improvements, showing concretely how the above principles are followed.</p>

<h2 id="frame-sandboxing">Frame sandboxing</h2>

<p>A <a href="https://html.spec.whatwg.org/#attr-iframe-sandbox">sandbox</a> attribute can
be specified on the <code class="language-plaintext highlighter-rouge">iframe</code> element in order to enable a set of
restrictions on any content it hosts.
These conditions can be relaxed by specifying a list of values such as
<code class="language-plaintext highlighter-rouge">allow-scripts</code> (to allow javascript execution in the frame) or <code class="language-plaintext highlighter-rouge">allow-popups</code>
(to allow the frame to open popups). By default, the same restrictions apply
to a popup opened by a sandboxed frame.</p>

<div style="text-align: center;">
    <div style="width: 300px; margin-left: auto; margin-right: auto;"><img src="https://frederic-wang.fr/images/iframe-sandboxing.svg" alt="iframe sandboxing" width="300" height="200" /></div>
    <div><small>Figure 1: Example of sandboxed frames (Can they navigate their top frame or open popups? Are such popups also sandboxed?)</small></div>
</div>

<p>However, sometimes this behavior is not wanted. Consider for example the case
of an
advertisement inside a sandboxed frame. If a popup is opened from this frame
then it is likely that a non-sandboxed context is desired on the landing page.
In order to handle this use case, a new <a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-popups-to-escape-sandbox">allow-popups-to-escape-sandbox</a> value
has been introduced. The value is now supported in <a href="https://developer.apple.com/safari/technology-preview/release-notes/#r34">Safari Technology Preview 34</a>.</p>

<p>While performing that work, it was noticed that some WPT tests for the sandbox
attribute were still failing. It turns out that WebKit does not really
follow the <a href="https://html.spec.whatwg.org/multipage/browsers.html#allowed-to-navigate">rules to allow navigation</a>. More specifically, navigating a top context
is never allowed when such context corresponds to an opened popup.
<a href="https://trac.webkit.org/changeset/218921">We have made some changes to WebKit</a>
so that it behaves more closely to the specification. This is integrated into <a href="https://developer.apple.com/safari/technology-preview/release-notes/#r35">Safari Technology Preview 35</a> and you can for example
try <a href="http://w3c-test.org/html/semantics/embedded-content/the-iframe-element/iframe_sandbox_popups_escaping-3.html">this W3C test</a>. Note that this test requires to change preferences to allow popups.</p>

<p>It is worth noting that web engines may slightly depart from the specification
regarding the previously mentioned rules. In particular, WebKit checks a
same-origin condition to be sure that one frame is allowed to navigate another
one.
WebKit always has contained
a special case to ignore this condition when a sandboxed frame with
the
<a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-top-navigation">allow-top-navigation</a> flag
tries and navigate its top frame. This feature, sometimes known 
as “frame busting,” has been used by third-party resources
to perform malicious auto-redirecting.
As a consequence, Chromium developers proposed to restrict
frame busting to the case where the navigation is triggered by a user gesture.</p>

<p>According to <a href="https://www.chromestatus.com/metrics/feature/timeline/popularity/1752">Chromium’s telemetry</a> frame busting without a user gesture is very rare.
But when experimenting with the <a href="https://github.com/WICG/interventions/issues/16">behavior change of <code class="language-plaintext highlighter-rouge">allow-top-navigation</code></a> several regressions were reported.
Hence it was instead decided to introduce the
<a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-top-navigation-by-user-activation">allow-top-navigation-by-user-activation</a> flag in order to provide this improved
safety context while still preserving backward compatibility.
We implemented this feature in WebKit and it is now available in <a href="https://developer.apple.com/safari/technology-preview/release-notes/#r37">Safari Technology Preview 37</a>.</p>

<p>Finally, another proposed security improvement is to use an
<a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-modals">allow-modals</a>
flag
to explicitly allow sandboxed frames to display modal dialogs (with <code class="language-plaintext highlighter-rouge">alert</code>,
<code class="language-plaintext highlighter-rouge">prompt</code>, etc). That is, the default behavior for sandboxed frames will be
to forbid such modal dialogs. Again, such a change of behavior must be done with
care. Experiments in Chromium showed that the
<a href="https://www.chromestatus.com/metrics/feature/timeline/popularity/767">usage of modal dialogs in sandboxed frames</a> is very low and no users complained.
Hence we
<a href="https://trac.webkit.org/changeset/221193">implemented that behavior in WebKit</a>
and the feature should arrive in Safari Technology Preview soon.</p>

<p>Check out the
<a href="https://webkit.org/demos/frames/sandboxing/">frame sandboxing demos</a> if
if you want to test the new <code class="language-plaintext highlighter-rouge">allow-popup-to-escape-sandbox</code>,
<code class="language-plaintext highlighter-rouge">allow-top-navigation-without-user-activation</code> and <code class="language-plaintext highlighter-rouge">allow-modals</code> flags.</p>

<h2 id="frame-scrolling-on-ios">Frame scrolling on iOS</h2>

<p>Apple’s UI choice was to (almost) always “flatten” (expand) frames so that
users do not require to scroll them. The rationale for this is that it avoids to
be trapped into hierarchy of nested frames. Changing that behavior is likely
to cause a big backward compatibility issue on iOS
so for now we proposed a less radical solution:
Add a heuristic to support the case of “fullscreen” iframes used by the AMP
Project. Note that such exceptions already exist in WebKit, e.g. to
avoid making <a href="http://accessibilitytips.com/2008/03/04/positioning-content-offscreen/">offscreen content</a> visible.</p>

<p>We thus <a href="https://trac.webkit.org/changeset/218480">added the following heuristic</a> into
WebKit Nightly: do not flatten
out-of-flow iframes (e.g. <code class="language-plaintext highlighter-rouge">position: absolute</code>) that have viewport units
(e.g. <code class="language-plaintext highlighter-rouge">vw</code> and <code class="language-plaintext highlighter-rouge">vh</code>). This includes the case of the “fullscreen” iframe previously
mentioned. For now it is still under a developer flag so that WebKit developers
can control when they want to enable it. Of course, if this is successful we
might consider more advanced heuristics.</p>

<p>The fact that <a href="https://bugs.webkit.org/show_bug.cgi?id=149264">frames are never scrollable in iOS</a> is an obvious interoperability
issue. As a workaround, it is possible to emulate such “scrollable nodes”
behavior using
<code class="language-plaintext highlighter-rouge">overflow: scroll</code> nodes with the <code class="language-plaintext highlighter-rouge">-webkit-overflow-scrolling: touch</code>
property set. This is not really ideal for our Web Predictability goal as we
would like to get rid of browser vendor prefixes. Also, in practice such
workarounds lead to even more problems in AMP as explained in these
<a href="https://medium.com/@dvoytenko/amp-ios-scrolling-and-position-fixed-b854a5a0d451">blog</a>
<a href="https://hackernoon.com/amp-ios-scrolling-and-position-fixed-redo-the-wrapper-approach-8874f0ee7876">posts</a>. That’s why implementing scrolling of frames is
one of the main goals of this project and
significant steps have already been made in that direction.</p>

<div style="text-align: center;">
    <div style="width: 400px; margin-left: auto; margin-right: auto;"><a href="https://frederic-wang.fr/images/scrolling-classes.svg"><img src="https://frederic-wang.fr/images/scrolling-classes.svg" alt="Class Hierarchy" width="400" /></a></div>
    <div><small>Figure 2: C++ classes involved in frame scrolling</small></div>
</div>

<p>The (relatively complex) class hierarchy involved in frame scrolling is
summarized in Figure 2. The frame flattening heuristic mentioned above is
handled in the <code class="language-plaintext highlighter-rouge">WebCore::RenderIFrame</code> class (in purple).
The <code class="language-plaintext highlighter-rouge">WebCore::ScrollingTreeFrameScrollingNodeIOS</code> and
<code class="language-plaintext highlighter-rouge">WebCore::ScrollingTreeOverflowScrollingNodeIOS</code> classes from the
scrolling tree (in blue) are used to scroll, respectively,
the main frame and overflow nodes on iOS. Scrolling of
non-main frames will obviously have some code to share with the former, but
it will also have some parts in common with the latter. For example,
passing an extra <code class="language-plaintext highlighter-rouge">UIScrollView</code> layer is needed instead of relying on the one
contained in the <code class="language-plaintext highlighter-rouge">WKWebView</code> of the main frame. An important
step is thus to introduce a special class for scrolling inner frames that
would share some logic from the two other classes and
<a href="https://bugs.webkit.org/show_bug.cgi?id=174097">some refactoring to</a> <a href="https://bugs.webkit.org/show_bug.cgi?id=174130">ensure optimal code reuse</a>.
Similar refactoring has been done for scrolling node states (in red)
<a href="https://bugs.webkit.org/show_bug.cgi?id=174134">to move the scrolling layer parameter into <code class="language-plaintext highlighter-rouge">WebCore::ScrollingStateNode</code></a> instead of having separate members
for <code class="language-plaintext highlighter-rouge">WebCore::ScrollingStateOverflowScrollingNode</code> and <code class="language-plaintext highlighter-rouge">WebCore::ScrollingStateFrameScrollingNode</code>.</p>

<p>The scrolling coordinator classes (in green) are also important, for example to
handle hit testing. At the moment, this is not really implemented for
overflow nodes but it might be important to have it for scrollable frames.
Again, one sees that some logic is shared for asynchronous scrolling on macOS (<code class="language-plaintext highlighter-rouge">WebCore::ScrollingCoordinatorMac</code>) and iOS (<code class="language-plaintext highlighter-rouge">WebCore::ScrollingCoordinatorIOS</code>)
in ancestor classes. Indeed, our effort to make frames scrollable on iOS
is also opening the possibility of
<a href="https://bugs.webkit.org/show_bug.cgi?id=171667">asynchronous scrolling of frames on macOS</a>, something that is currently not implemented.</p>

<div style="text-align: center;">
   <div style="width: 500px; margin-left: auto; margin-right: auto;"><a target="_blank" href="https://player.vimeo.com/video/225557385"><img src="https://frederic-wang.fr/images/video-ios-frame-scrolling.png" alt="Class Hierarchy" width="500" /></a></div>
    <div><small>Figure 4: Video of this <a href="https://webkit.org/demos/frames/scrollable-iframes.html">demo page</a> on WebKit iOS with experimental patches to make frame scrollables (2017/07/10)</small></div>
</div>

<p>Finally, some more work is necessary in the render classes (purple) to ensure
that the layer hierarchies are correctly built. Patches
<a href="https://bugs.webkit.org/show_bug.cgi?id=173833">have been uploaded</a>
and you can view the result on the video of Figure 4.
Notice that this work has not been reviewed yet and
there are known bugs, for example with
overlapping elements (hit testing not implemented) or <code class="language-plaintext highlighter-rouge">position: fixed</code>
elements.</p>

<p>Various other scrolling bugs were reported, analyzed and sometimes fixed by
Apple. The switch from overflow nodes to scrollable iframes is unlikely to
address them. For example, the “Find Text” operation in iOS has
advanced features done by the UI process (highlight, smart magnification) but
the <a href="https://bugs.webkit.org/show_bug.cgi?id=163911">scrolling operation needed only works for the main frame</a>. It looks like this could be fixed
by unifying a bit the scrolling code path with macOS. There are also
several <a href="https://bugs.webkit.org/show_bug.cgi?id=154399">jump and flickering bugs</a> with <code class="language-plaintext highlighter-rouge">position: fixed</code> nodes. Finally, Apple fixed
<a href="https://bugs.webkit.org/show_bug.cgi?id=162499">inconsistent scrolling inertia</a>
used for the main frame and the one used for inner scrollable nodes by
making the former the same as the latter.</p>

<h2 id="root-scroller">Root Scroller</h2>

<p>The CSSOM View specification <a href="https://drafts.csswg.org/cssom-view/#extension-to-the-element-interface">extends the DOM element with some scrolling properties</a>.
That specification indicates that the element to consider to scroll the main view
is <code class="language-plaintext highlighter-rouge">document.body</code> in quirks mode while it is <code class="language-plaintext highlighter-rouge">document.documentElement</code>
in no-quirks mode. This is the behavior that has always been followed
by browsers like Firefox or Interner Explorer. However, WebKit-based browsers
always treat <code class="language-plaintext highlighter-rouge">document.body</code> as the root scroller. This interoperability issue
has been a big problem for web developers.
One convenient workaround was to introduce the
<a href="https://drafts.csswg.org/cssom-view/#dom-document-scrollingelement">document.scrollingElement</a> which returns the element to use for scrolling the main
view (<code class="language-plaintext highlighter-rouge">document.body</code> or <code class="language-plaintext highlighter-rouge">document.documentElement</code>) and was recently
<a href="https://bugs.webkit.org/show_bug.cgi?id=143609">implemented in WebKit</a>.
Use this
<a href="https://webkit.org/demos/frames/scrollingElement.html">test page</a>
to verify whether your browser supports the
<code class="language-plaintext highlighter-rouge">document.scrollingElement</code> property and which DOM element is used to scroll
the main view in no-quirks mode.</p>

<p>Nevertheless, this does not solve the issue with existing web pages.
Chromium’s Web Platform Predictability team has made a huge communication effort
with Web authors and developers which has
drastically reduced the use of <code class="language-plaintext highlighter-rouge">document.body</code> in no-quirks mode. For instance,
Chromium’s telemetry on Figure 3 indicates that the percentage of
<code class="language-plaintext highlighter-rouge">document.body.scrollTop</code> in no-quirks pages has gone
from 18% down to 0.0003% during the past three years. Hence the Chromium team
is now considering <a href="https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/X64Sg16RhT4">shipping the standard behavior</a>.</p>

<div style="text-align: center;">
    <div style="width: 400px; margin-left: auto; margin-right: auto;"><a href="https://www.chromestatus.com/metrics/feature/popularity#ScrollTopBodyNotQuirksMode"><img width="400" src="https://frederic-wang.fr/images/ScrollTopBodyNotQuirksMode.png" alt="UseCounter for ScrollTopBodyNotQuirksMode" /></a></div>
    <div><small>Figure 3: Use of <code>document.body.scrollTop</code> in no-quirks mode over time (Chromium's UseCounter)</small></div>
</div>

<p>In WebKit, the issue has been known for a long time and an
<a href="https://bugs.webkit.org/show_bug.cgi?id=106133">old attempt to fix it was reverted for causing regressions</a>. For now, we imported
the <a href="https://trac.webkit.org/changeset/215726/">CSSOM View tests</a> and just
marked the one related to the scrolling element as failing. An analysis
of the situation has been left on
<a href="https://bugs.webkit.org/show_bug.cgi?id=5991#c14">WebKit’s bug</a>; Depending on
how things evolve on Chromium’s side we could consider the discussion and
implementation work in WebKit.</p>

<p>Related to that work, a
<a href="https://github.com/bokand/NonDocumentRootScroller">new API</a> is being proposed
to set the root scroller to an arbitrary scrolling element, giving
more flexibility to authors of Web applications. Today, this is unfortunately
not possible
without losing some of the special features of the main view (e.g. on iOS,
Safari’s URL bar is hidden when scrolling the main view
to maximize the screen space). Such
API is currently being experimented in Chromium and we plan to
investigate whether this can be implemented in WebKit too.</p>

<h2 id="conclusion">Conclusion</h2>

<p>In the past months, The AMP Project and Igalia have worked on analyzing some
interoperability issue and fixing them in WebKit. Many improvements for
frame sandboxing are going to be available soon.
Significant progress has also been
made for frame scrolling on iOS and collaboration continues with
Apple reviewers to ensure that the work will be integrated in future versions of
WebKit. Improvements to “root scrolling” are also being considered although they
are pending on the evolution of the issues on Chromium’s side. All these
efforts are expected to be useful for WebKit users and the Web platform
in general.</p>

<div>
<div style="width: 364px; margin-left: auto; margin-right: auto;"><a href="http://www.igalia.com"><img src="https://frederic-wang.fr/images/igalia-logo-364x130.png" alt="Igalia Logo" width="364" height="130" /></a></div>
<div style="width: 400px; margin-left: auto; margin-right: auto;"><a href="https://www.ampproject.org/"><img src="https://frederic-wang.fr/images/amp-logo-400x210.png" alt="AMP Logo" width="400" height="210" /></a></div>
</div>

<p>Last but not least, I would like to thank Apple engineers Simon Fraser,
Chris Dumez, and Youenn Fablet for their reviews and help, as well as Google
and the AMP team for supporting that project.</p>

{% endraw %}
