---
layout: post
title: "Mus Window System"
tags: igalia chromium
---

{% raw %}

  <p><ins style="color: orange">Update 2017/02/01: The day I published this blog post, the old mus client library was <a href="https://codereview.chromium.org/2651593002">removed</a>. Some stack traces were taken during the analysis Antonio &amp; I made in fall 2016, but they are now obsolete. I’m updating the blog in order to try and clarify things and fix possible inaccuracies.</ins></p>

<h1 id="tl-dr">TL; DR</h1>

<p><strong>Igalia has recently been working on <a href="https://www.reddit.com/r/blinkon7/comments/5p5w28/desktop_chrome_waylandozone/">making Chromium Desktop run natively on Ozone/Wayland</a></strong> thanks to support from <a href="https://www.renesas.com/">Renesas</a>.
This is however still experimental and there is a lot of UI work to do.
In order to <strong>facilitate discussion at BlinkOn7</strong> and more specifically how
browser windows are managed, we started an <strong>analysis of the Chromium Window
system</strong>. An overview is provided in this blog post.</p>

<h1 id="introduction">Introduction</h1>

<p>Antonio described how we were able to get <a href="https://blogs.igalia.com/tonikitoo/2016/11/14/chromium-ozone-wayland-and-beyond/">upstream Chromium running on Linux/Ozone/Wayland</a> last year. However for that purpose the browser
windows were really embedded in the “ash” environment (with additional widgets)
which was itself drawn in an Ozone/Wayland window. This configuration is
obviously not ideal but it at least allowed us to do some initial experiments
and to present demos of <a href="https://frederic-wang.fr/chromium-on-r-car-m3.html">Chromium running on R-Car M3</a> at <a href="https://www.igalia.com/nc/igalia-247/news/item/igalia-to-attend-ces-las-vegas-2017/">CES 2017</a>. If you are interested you can
check our <a href="https://github.com/Igalia/ces-demos-2017">ces-demos-2017</a>
and <a href="https://github.com/Igalia/meta-browser">meta-browser</a> repositories on
GitHub. Our next goal is to have all the browser windows handled as native
Ozone/Wayland windows.</p>

<p>In a <a href="https://frederic-wang.fr/analysis-of-ozone-wayland.html">previous blog post</a>, I gave an overview of the architecture of <a href="https://chromium.googlesource.com/chromium/src/+/master/docs/ozone_overview.md">Ozone</a>. In particular, I described classes used to handle Ozone windows for the <a href="https://en.wikipedia.org/wiki/X_Window_System">X11</a> or <a href="https://en.wikipedia.org/wiki/Wayland_\(display_server_protocol\)">Wayland</a> platforms. However, this was only a small part of the picture and to understand things globally one really has to take into account the classes for the Aura window system and Mus window client &amp; server.</p>

<h1 id="window-related-classes">Window-related Classes</h1>

<h2 id="class-hierarchy">Class Hierarchy</h2>

<p>A large number of C++ classes and types are involved in the chromium window
system. The following diagram provides an overview of the class hierarchy. It
can merely be divided into four parts:</p>

<ul>
  <li>In blue, the native Ozone Windows and their host class in Aura.</li>
  <li>In red and orange, the Aura Window Tree.</li>
  <li>In purple, the Mus Window Tree (client-side). <ins style="color: orange">Update 2017/02/01: These classes have been <a href="https://codereview.chromium.org/2651593002">removed</a>.</ins></li>
  <li>In green and brown, the Mus Window Tree (server-side) and its associated
factories.</li>
</ul>

<p><a href="https://frederic-wang.fr/images/windowing-system.svg"><img src="https://frederic-wang.fr/images/windowing-system.svg" alt="Windowing System" style="width: 100%" /></a></p>

<p>I used the following convention which is more or less based on UML:</p>

<ul>
  <li>Rectangles represent classes/interfaces while ellipses represent enums, types,
defines etc. You can click them to access the corresponding C++ source file.</li>
  <li>Inheritance is indicated by a white arrow to the base class from the derived
class. For implementation of Mojo interfaces, dashed white arrows are used.</li>
  <li>Other associations are represented by an arrow with open or diamond head.
They mean that the origin of the arrow has a member involving one or more
instances of the pointed class, you can hover over the arrow head to
see the name of that class member.</li>
</ul>

<h2 id="native-ozone-windows-blue">Native Ozone Windows (blue)</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/platform_window/platform_window.h">ui::PlatformWindow</a> is an abstract class representing a single window
in the underlying platform windowing system. Examples of implementations include <a href="https://cs.chromium.org/chromium/src/ui/platform_window/x11/x11_window_ozone.h">ui::X11WindowOzone</a> or <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/wayland_window.h">ui::WaylandWindow</a>.</p>

<p><code class="language-plaintext highlighter-rouge">ui::PlatformWindow</code> can be stored in a
<a href="https://cs.chromium.org/chromium/src/services/ui/ws/platform_display_default.h">ui::ws::PlatformDisplayDefault</a> which implements the
<a href="https://cs.chromium.org/chromium/src/ui/platform_window/platform_window_delegate.h">ui::PlatformWindowDelegate</a> interface too. This in turn allows to use
platform windows as <a href="https://cs.chromium.org/chromium/src/services/ui/ws/display.h">ui::ws::Display</a>. <code class="language-plaintext highlighter-rouge">ui::ws::Display</code> also has an associated delegate class.</p>

<p><a href="https://cs.chromium.org/chromium/src/ui/aura/window_tree_host.h">aura::WindowTreeHost</a> is a generic class that hosts an embedded <code class="language-plaintext highlighter-rouge">aura:Window</code>
root and bridges between the native window and that embedded root window.
One can register instance of <a href="https://cs.chromium.org/chromium/src/ui/aura/window_tree_host_observer.h">aura::WindowTreeHostObserver</a> as observers. There are
various implementations of <code class="language-plaintext highlighter-rouge">aura::WindowTreeHost</code> but we only consider
<code class="language-plaintext highlighter-rouge">aura::WindowTreeHostPlatform</code> here.</p>

<p>Native <code class="language-plaintext highlighter-rouge">ui::PlatformWindow</code> windows are stored in an instance of
<a href="https://cs.chromium.org/chromium/src/ui/aura/window_tree_host_platform.h">aura::WindowTreeHostPlatform</a> which also holds the <a href="https://cs.chromium.org/chromium/src/ui/gfx/native_widget_types.h">gfx::AcceleratedWidget</a> to paint on.
<code class="language-plaintext highlighter-rouge">aura::WindowTreeHostPlatform</code> implements the
<a href="https://cs.chromium.org/chromium/src/ui/platform_window/platform_window_delegate.h">ui::PlatformWindowDelegate</a> so that it can listen events from the
underlying <code class="language-plaintext highlighter-rouge">ui::PlatformWindow</code>.</p>

<p><a href="https://cs.chromium.org/chromium/src/ui/aura/mus/window_tree_host_mus.h">aura::WindowTreeHostMus</a> is a derived class of <a href="https://cs.chromium.org/chromium/src/ui/aura/window_tree_host_platform.h">aura::WindowTreeHostPlatform</a> that has additional logic make it usable in mus. One can listen changes from
<code class="language-plaintext highlighter-rouge">aura::WindowTreeHostMus</code> by implementing the
<a href="https://cs.chromium.org/chromium/src/ui/aura/mus/window_tree_host_mus_delegate.h">aura::WindowTreeHostMusDelegate</a> interface.</p>

<h2 id="aura-windows-orange">Aura Windows (orange)</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/aura/window.h">aura::Window</a> represents
windows in Aura. One can communicate with instances of that class using
a <a href="https://cs.chromium.org/chromium/src/ui/aura/window_delegate.h&quot; color=&quot;green&quot; fontcolor=&quot;green&quot;">aura::WindowDelegate</a>. It is also possible to listen for events by registering a list of <a href="https://cs.chromium.org/chromium/src/ui/aura/window_observer.h">aura::WindowObserver</a>.</p>

<p><a href="https://cs.chromium.org/chromium/src/ui/aura/window_port.h">aura::WindowPort</a>
defines an interface to enable <a href="https://cs.chromium.org/chromium/src/ui/aura/window.h">aura::Window</a> to be used either with mus via <a href="https://cs.chromium.org/chromium/src/ui/aura/mus/window_mus.h">aura::WindowMus</a> or with the classical
environment via <a href="https://cs.chromium.org/chromium/src/ui/aura/window_port_local.h">aura::WindowPortLocal</a>. Here, we only consider the former.</p>

<p><code class="language-plaintext highlighter-rouge">WindowPortMus</code> holds a reference to a <code class="language-plaintext highlighter-rouge">aura::WindowTreeClient</code>. All the
changes to the former are forwarded to the latter so that we are sure they
are propagated to the server. Conversely, changes received by
<code class="language-plaintext highlighter-rouge">aura::WindowTreeClient</code> are sent back to <code class="language-plaintext highlighter-rouge">WindowPortMus</code>. However,
<code class="language-plaintext highlighter-rouge">aura::WindowTreeClient</code> uses an intermediary <a href="https://cs.chromium.org/chromium/src/ui/aura/mus/window_mus.h">aura::WindowMus</a> class for that purpose to avoid
that the changes are submitted again to the server.</p>

<h2 id="aura-window-tree-client-red">Aura Window Tree Client (red)</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/aura/mus/window_tree_client.h">aura::WindowTreeClient</a> is an implementation of the <code class="language-plaintext highlighter-rouge">ui::mojom::WindowManager</code> and
<code class="language-plaintext highlighter-rouge">ui::mojom::WindowTreeClient</code> Mojo interfaces for Aura.
As in previous classes, we can associate to it a <a href="https://cs.chromium.org/chromium/src/services/ui/aura/mus/window_tree_client_delegate.h">aura::WindowTreeClientDelegate</a> or register a list of <a href="https://cs.chromium.org/chromium/src/ui/aura/mus/window_tree_client_observer.h">aura::WindowTreeClientObserver</a>.</p>

<p><code class="language-plaintext highlighter-rouge">aura::WindowTreeClient</code> also implements the
<a href="https://cs.chromium.org/chromium/src/ui/aura/mus/window_manager_delegate.h">aura::WindowManagerClient</a> interface and has as an associated
<a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_manager_delegate.h">aura::WindowManagerDelegate</a>.
It has a set of roots <code class="language-plaintext highlighter-rouge">aura::WindowPortMus</code> which serve
as an intermediary to the actual <code class="language-plaintext highlighter-rouge">aura:Window</code> instances.</p>

<p>In order to use an Aura Window Tree Client, you first create it using a Mojo
connector, <code class="language-plaintext highlighter-rouge">aura::WindowTreeClientDelegate</code> as well as optional
<code class="language-plaintext highlighter-rouge">aura::WindowManagerDelegate</code> and Mojo interface request for
<code class="language-plaintext highlighter-rouge">ui::mojom::WindowTreeClient</code>. After that you need to call
<code class="language-plaintext highlighter-rouge">ConnectViaWindowTreeFactory</code> or <code class="language-plaintext highlighter-rouge">ConnectAsWindowManager</code> to connect
to the Window server and create the corresponding <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree</code>
connection. Obviously, <code class="language-plaintext highlighter-rouge">AddObserver</code> can be used to add observers.</p>

<p>Finally, the <code class="language-plaintext highlighter-rouge">CreateWindowPortForTopLevel</code> function can be used to request
the server to create a new top level window and associate a <code class="language-plaintext highlighter-rouge">WindowPortMus</code>
to it.</p>

<h2 id="mus-window-tree-client-purple">Mus Window Tree Client (purple)</h2>

<p><ins style="color: orange">Update 2017/02/01: These classes have been <a href="https://codereview.chromium.org/2651593002">removed</a>.</ins></p>

<p><a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_tree_client.h">ui::WindowTreeClient</a> is the equivalent of <code class="language-plaintext highlighter-rouge">aura:WindowTreeClient</code> in mus.
It implements the
<code class="language-plaintext highlighter-rouge">ui::mojom::WindowManager</code> and
<code class="language-plaintext highlighter-rouge">ui::mojom::WindowTreeClient</code> Mojo interfaces.
It derives from <a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_manager_delegate.h">ui::WindowManagerClient</a>, has a list of
<a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_tree_client_observer.h">ui::WindowTreeClientObserver</a> and
is associated to <a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_manager_delegate.h">ui::WindowManagerDelegate</a> and
<a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_tree_client_delegate.h">ui::WindowTreeClientDelegate</a>.</p>

<p>Regarding windows, they are simpler than in Aura since we only have one class <a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_tree_client.h">ui::Window</a> class. In a similar way as Aura, we can register
<a href="https://cs.chromium.org/chromium/src/services/ui/public/cpp/window_observer.h">ui::WindowObserver</a>. We can also add <code class="language-plaintext highlighter-rouge">ui::Window</code> as root windows or embedded
windows of <code class="language-plaintext highlighter-rouge">ui::WindowTreeClient</code>.</p>

<p>In order to use a Mus Window Tree Client, you first create it using a
<code class="language-plaintext highlighter-rouge">ui::WindowTreeClientDelegate</code> as well as optional
<code class="language-plaintext highlighter-rouge">ui::WindowManagerDelegate</code> and Mojo interface request for
<code class="language-plaintext highlighter-rouge">ui::mojom::WindowTreeClient</code>. After that you need to call
<code class="language-plaintext highlighter-rouge">ConnectViaWindowTreeFactory</code> or <code class="language-plaintext highlighter-rouge">ConnectAsWindowManager</code> to connect
to the Window server and create the corresponding <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree</code>
connection. Obviously, <code class="language-plaintext highlighter-rouge">AddObserver</code> can be used to add observers.</p>

<p>Finally, the <code class="language-plaintext highlighter-rouge">NewTopLevelWindow</code> and <code class="language-plaintext highlighter-rouge">NewWindow</code> functions
can be used to create new
windows. This will cause the corresponding functions to be called on the
connected <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree</code>.</p>

<h2 id="mus-window-tree-server-green-and-brown">Mus Window Tree Server (green and brown)</h2>

<p>We just saw the Aura and Mus window tree clients. The <code class="language-plaintext highlighter-rouge">ui::ws::WindowTree</code> Mojo
interface is used to for the window tree server and is implemented in
<a href="https://cs.chromium.org/chromium/src/services/ui/ws/window_tree.h">ui::ws::WindowTree</a>. In order to create window trees, we can use
either the <a href="https://cs.chromium.org/chromium/src/services/ui/ws/window_manager_window_tree_factory.h">ui::ws::WindowManagerWindowTreeFactory</a> or the
<a href="https://cs.chromium.org/chromium/src/services/ui/ws/window_tree_factory.h&quot;  color=&quot;green&quot; fontcolor=&quot;green&quot;">ui::ws::WindowTreeFactory</a> which are available
through the corresponding <code class="language-plaintext highlighter-rouge">ui::mojom::WindowManagerWindowTreeFactory</code> and
<code class="language-plaintext highlighter-rouge">ui::mojom::WindowTreeFactory</code> Mojo interfaces.</p>

<p><a href="https://cs.chromium.org/chromium/src/services/ui/ws/window_tree_host_factory.h">ui::ws::WindowTreeHostFactory</a> implements the <code class="language-plaintext highlighter-rouge">ui::ws::WindowTreeHostFactory</code> Mojo interface. It allows to create
<a href="https://cs.chromium.org/chromium/src/services/ui/window_tree_host.mojom">ui::mojom::WindowTreeHost</a>, more precisely <code class="language-plaintext highlighter-rouge">ui::ws::Display</code> implementing that
interface. Under the hood, <code class="language-plaintext highlighter-rouge">ui::ws::Display</code> created that way actually have an
associated <a href="https://cs.chromium.org/chromium/src/services/ui/ws/display_binding.h">ws::DisplayBinding</a> creating a <code class="language-plaintext highlighter-rouge">ui::ws::WindowTree</code>. Of course, the display
also has a native window associated to it.</p>

<h2 id="mojo-window-tree-apis-pink">Mojo Window Tree APIs (pink)</h2>

<p><ins style="color: orange">Update 2017/02/01: The Mus client has been <a href="https://codereview.chromium.org/2651593002">removed</a>. This section only applies to the Aura client.</ins></p>

<p>As we have just seen in previous sections the Aura and Mus window systems are
very similar and in particular implement the same Mojo
<a href="https://cs.chromium.org/chromium/src/services/ui/public/interfaces/window_manager.mojom">ui::mojom::WindowManager</a>
and <a href="https://cs.chromium.org/chromium/src/services/ui/public/interfaces/window_tree.mojom">ui::mojom::WindowTreeClient</a> interfaces. In particular:</p>

<ul>
  <li>
    <p>The <code class="language-plaintext highlighter-rouge">ui::mojom::WindowManager::WmCreateTopLevelWindow</code> function can
be used to create a new top level window. This results in a new windows
(<code class="language-plaintext highlighter-rouge">aura::Window</code> or <code class="language-plaintext highlighter-rouge">ui::Window</code>) being added to the set of embedded windows.</p>
  </li>
  <li>
    <p>The <code class="language-plaintext highlighter-rouge">ui::mojom::WindowManager::WmNewDisplayAdded</code> function is invoked when
a new display is added. This results in a new  window being added to the set
of window roots (<code class="language-plaintext highlighter-rouge">aura::WindowMus</code> or <code class="language-plaintext highlighter-rouge">ui::Window</code>).</p>
  </li>
  <li>
    <p>The <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTreeClient::OnEmbed</code> function is invoked when
<code class="language-plaintext highlighter-rouge">Embed</code> is called on the connected <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree</code>.
The window parameter will be set as the window root
(<code class="language-plaintext highlighter-rouge">aura:WindowMus</code> or <code class="language-plaintext highlighter-rouge">ui:Window</code>). Note that we assume that the set
of roots is empty when such an embedding happens.</p>
  </li>
</ul>

<p>Note that for Aura Window Tree Client, the creation of new
<code class="language-plaintext highlighter-rouge">aura::WindowMus</code> window roots implies the creation of the associated
<code class="language-plaintext highlighter-rouge">aura::WindowTreeHostMus</code> and <code class="language-plaintext highlighter-rouge">aura::WindowPortMus</code>. The creation of the new
<code class="language-plaintext highlighter-rouge">aura:Window</code> window by <code class="language-plaintext highlighter-rouge">aura::WmCreateTopLevelWindow</code> is left to the
corresponding implementation in <code class="language-plaintext highlighter-rouge">aura::WindowManagerDelegate</code>.</p>

<p>On the server side, the <code class="language-plaintext highlighter-rouge">ui::ws::WindowTree</code> implements the
<code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree</code> mojo interface. In particular:</p>

<ul>
  <li>
    <p>The <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree::Embed</code> function can be used to embed a
WindowTreeClient at a given window. This will result of <code class="language-plaintext highlighter-rouge">OnEmbed</code> being called
on the window tree client.</p>
  </li>
  <li>
    <p>The <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree::NewWindow</code> function can be used to create a new
window. It will call <code class="language-plaintext highlighter-rouge">OnChangeCompleted</code> on the window tree client.</p>
  </li>
  <li>
    <p>The <code class="language-plaintext highlighter-rouge">ui::mojom::WindowTree::NewTopLevelWindow</code> function can be used to
request the window manager to create a new top level window.
It will call <code class="language-plaintext highlighter-rouge">OnTopLevelCreated</code> (or <code class="language-plaintext highlighter-rouge">OnChangeCompleted</code> in case of failure)
on the window tree client.</p>
  </li>
</ul>

<h1 id="analysis-of-window-creation">Analysis of Window Creation</h1>

<h2 id="chromemash">Chrome/Mash</h2>

<p>In our project, we are interested in how Chrome/Mash windows are created. When
the chrome browser process is launched, it takes the regular content/browser
startup path. That means in
<a href="https://cs.chromium.org/chromium/src/chrome/app/chrome_main.cc">chrome/app/chrome_main.cc</a>
it does not take the <code class="language-plaintext highlighter-rouge">::MainMash</code> path, but instead <code class="language-plaintext highlighter-rouge">content::ContentMain</code>.
This is the call stack of Chrome window creation within the mash shell:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>#1 0x7f7104e9fd02 ui::WindowTreeClient::NewTopLevelWindow()
#2 0x5647d0ed9067 BrowserFrameMus::BrowserFrameMus()
#3 0x5647d09c4a47 NativeBrowserFrameFactory::Create()
#4 0x5647d096bbc0 BrowserFrame::InitBrowserFrame()
#5 0x5647d0877b8a BrowserWindow::CreateBrowserWindow()
#6 0x5647d07d5a48 Browser::Browser()
...
</code></pre></div></div>

<p><ins style="color: orange">Update 2017/02/01: This has changed since the time when the stack trace was taken. The BrowserFrameMus constructor now creates a views:DesktopNativeWidgetAura and thus an aura::Window.</ins></p>

<p>The outtermost window created when one executes <code class="language-plaintext highlighter-rouge">chrome --mash</code> happens as
follows. When the UI service starts (see <code class="language-plaintext highlighter-rouge">Service::OnStart</code> in
<a href="https://cs.chromium.org/chromium/src/services/ui/service.cc">services/ui/service.cc</a>), an instance of <code class="language-plaintext highlighter-rouge">WindowServer</code> is created. This creations triggers the
creation of a <code class="language-plaintext highlighter-rouge">GpuServiceProxy</code> instance. See related snippets below:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>void Service::OnStart() {
  (...)
  // Gpu must be running before the PlatformScreen can be initialized.
  window_server_.reset(new ws::WindowServer(this));
  (..)
}

WindowServer::WindowServer(WindowServerDelegate* delegate)
: delegate_(delegate),
  (..)
  gpu_proxy_(new GpuServiceProxy(this)),
  (..)
{ }
</code></pre></div></div>

<p><code class="language-plaintext highlighter-rouge">GpuServiceProxy</code>, then, starts off the GPU service initialization. By the time
the GPU connection is established, the following callback is called: <code class="language-plaintext highlighter-rouge">GpuServiceProxy::OnInternalGpuChannelEstablished</code>. This calls back to
<code class="language-plaintext highlighter-rouge">WindowServer::OnGpuChannelEstablished</code>, which calls
<code class="language-plaintext highlighter-rouge">Service::StartDisplayInit</code>. The later schedules a call to
<code class="language-plaintext highlighter-rouge">PlatformScreenStub::FixedSizeScreenConfiguration</code>. This finally triggers the
creation of an Ozone top level window via an <code class="language-plaintext highlighter-rouge">ui::ws::Display</code>:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>#0 base::debug::StackTrace::StackTrace()
#1 ui::(anonymous namespace)::OzonePlatformX11::CreatePlatformWindow()
#2 ui::ws::PlatformDisplayDefault::Init()
#3 ui::ws::Display::Init()
#4 ui::ws::DisplayManager::OnDisplayAdded()
#5 ui::ws::PlatformScreenStub::FixedSizeScreenConfiguration()
(..)
</code></pre></div></div>

<p><ins style="color: orange">On the client-side, the addition of a new display will cause <code class="language-plaintext highlighter-rouge">aura::WindowTreeClient::WmNewDisplayAdded</code> to be called and will eventually lead to the creation of an <code class="language-plaintext highlighter-rouge">aura::WindowTreeHostMus</code> with the corresponding display id. As shown on the graph, this class derives from <code class="language-plaintext highlighter-rouge">aura::WindowTreeHost</code> and hence instantiates an <code class="language-plaintext highlighter-rouge">aura::Window</code>.</ins></p>

<h2 id="mus-demo">Mus demo</h2>

<p>The Chromium source code contains a small
<a href="https://cs.chromium.org/chromium/src/services/ui/demo/mus_demo.cc">mus demo</a>
that is also useful do experiments. The demo is implemented via a class with the
following inheritance:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>class MusDemo : public service_manager::Service,
                public aura::WindowTreeClientDelegate,
                public aura::WindowManagerDelegate
</code></pre></div></div>

<p>i.e. it can be started as Mus service and handles some events from
<code class="language-plaintext highlighter-rouge">aura:WindowTreeClient</code> and <code class="language-plaintext highlighter-rouge">aura::WindowManager</code>.</p>

<p>When the demo service is launched, it creates a new Aura environment and an
<code class="language-plaintext highlighter-rouge">aura::WindowTreeClient</code>, it does the Mojo request to create an <code class="language-plaintext highlighter-rouge">ui::WindowTree</code>
and then performs the connection:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>#0 aura::WindowTreeClient::ConnectAsWindowManager()
#1 ui::demo::MusDemo::OnStart()
#2 service_manager::ServiceContext::OnStart()
</code></pre></div></div>

<p>Similarly to Chrome/Mash, a new display and its associated native window is
created by the UI:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>#0 ui::ws::WindowTree::AddRootForWindowManager()
#1 ui::ws::Display::CreateWindowManagerDisplayRootFromFactory()
#2 ui::ws::Display::InitWindowManagerDisplayRoots()
#3 ui::ws::PlatformDisplayDefault::OnAcceleratedWidgetAvailable()
#4 ui::X11WindowBase::Create()
#5 ui::(anonymous namespace)::OzonePlatformX11::CreatePlatformWindow()
#6 ui::ws::PlatformDisplayDefault::Init()
#7 ui::ws::Display::Init()
#8 ui::ws::DisplayManager::OnDisplayAdded()
</code></pre></div></div>

<p>The Aura Window Tree Client listens the changes and eventually
<code class="language-plaintext highlighter-rouge">aura::WindowTreeClient::WmNewDisplayAdded</code> is called. It then informs its
<code class="language-plaintext highlighter-rouge">MusDemo</code> delegate so that the display is <a href="https://cs.chromium.org/chromium/src/services/ui/demo/mus_demo.cc?q=MusDemo::OnWmWillCreateDisplay">added to the screen display list</a>…</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>#0 DisplayList::AddDisplay
#1 ui::demo::MusDemo::OnWmWillCreateDisplay
#2 aura::WindowTreeClient::WmNewDisplayAddedImpl
#3 aura::WindowTreeClient::WmNewDisplayAdded
</code></pre></div></div>

<p>…and <a href="https://cs.chromium.org/chromium/src/services/ui/demo/mus_demo.cc?q=MusDemo::OnWmNewDisplay">the animated bitmap window is added to the Window Tree</a>:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>#0  ui::demo::MusDemo::OnWmNewDisplay
#1  aura::WindowTreeClient::WmNewDisplayAddedImpl
#2  aura::WindowTreeClient::WmNewDisplayAdded
</code></pre></div></div>

<p><ins style="color: orange">Update 2017/02/01: Again, <code class="language-plaintext highlighter-rouge">aura::WindowTreeClient::WmNewDisplayAdded</code> will lead to the creation of an aura Window.</ins></p>

<h1 id="conclusion">Conclusion</h1>

<p>Currently, both Chrome/Mash or Mus demo create a <code class="language-plaintext highlighter-rouge">ui::ws::Display</code>
containing a native Ozone window. The Mus demo class uses the Aura
<code class="language-plaintext highlighter-rouge">WindowTreeClient</code> to track the creation of that display and pass it to the
Mus Demo class. The actual chrome browser window is created inside the native
Mash window using a Mus <code class="language-plaintext highlighter-rouge">WindowTreeClient</code>. Again, this is not what we want
since each chrome browser should have its own native window. It will be
interesting to first experiment multiple native windows with the Mus demo.</p>

<p><ins style="color: orange">Update 2017/02/01: <code class="language-plaintext highlighter-rouge">aura::WindowTreeClient</code> is now always used to create Aura Windows for both external windows (corresponding to a display &amp; a native window) and internal windows. However, we still want all chrome browser to be external windows.</ins></p>

<div>
<div style="width: 364px; margin-left: auto; margin-right: auto;"><a href="http://www.igalia.com"><img src="https://frederic-wang.fr/images/igalia-logo-364x130.png" width="364" height="130" alt="Igalia Logo" /></a></div>
<div style="width: 763px; margin-left: auto; margin-right: auto;"><a href="https://www.renesas.com/en-eu/"><img src="https://frederic-wang.fr/images/renesas_logomark_l.jpg" width="763" height="130" alt="Renesas Logo" /></a></div>
</div>

<p>It seems that the Ozone/Mash work has been mostly done with ChromeOS in mind
and will probably need some adjustments to make things work on desktop Linux.
We are very willing to discuss this and other steps for
<a href="https://www.reddit.com/r/blinkon7/comments/5p5w28/desktop_chrome_waylandozone/">Desktop Chrome Wayland/Ozone</a> in details with
Google engineers. <strong>Antonio will attend BlinkOn7 next week and will be very
happy to talk with you so do not hesitate to get in touch!</strong></p>

{% endraw %}
