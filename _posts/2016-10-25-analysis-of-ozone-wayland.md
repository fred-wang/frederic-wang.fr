---
layout: post
title: "Analysis of Ozone Wayland"
tags: igalia chromium
---

{% raw %}

  <h1 id="introduction">Introduction</h1>

<p>In the past two months, I have been working with my colleague
<a href="https://www.igalia.com/nc/igalia-247/igalian/item/agomes/">Antonio Gomes</a> on
a Chromium project supported by
<a href="https://www.renesas.com/en-eu/">Renesas</a>. <strong>The goal
is to have Chrome running on Wayland with accelerated rendering happening in a
separate GPU process</strong>. Intel has done a great job to
develop a <a href="https://github.com/01org/ozone-wayland">specific Wayland platform</a>
for <a href="https://www.chromium.org/developers/design-documents/ozone">Ozone</a> but
unfortunately the code
<a href="https://groups.google.com/a/chromium.org/d/msg/ozone-dev/ptwW3pVpUYs/aXEZet-dAgAJ">only works for older releases of Chromium and is not fully upstreamed yet</a>.
In theory, <a href="https://www.chromium.org/developers/design-documents/ozone">easy out-of-tree platforms</a> was one of the guiding principles of Ozone but in
practice <a href="https://groups.google.com/a/chromium.org/forum/#!topic/ozone-dev/5lRcidwo7ik">we had to fix many build and run time
errors for Ozone</a>, even though we were working upstream. More generally,
it is very challenging to keep in sync with all the refactoring work happening
upstream and some work is definitely required to align Intel’s code with
Google’s goals.</p>

<p>To summarize the situation briefly, <strong>if we follow Intel’s approach then the
currently upstreamed Wayland code only
compiles for ChromeOS</strong> (i.e. <code class="language-plaintext highlighter-rouge">target_os="chromeos"</code> in your build config)
not for standard Linux
build of Chrome. You can <strong>only have accelerated rendering at the price of
removing separation of UI/GPU processes</strong> (i.e. via the <code class="language-plaintext highlighter-rouge">--in-process-gpu</code>
switch). If you keep the default behavior of having the UI and GPU components
running in separate processes then accelerated rendering fails. A fallback
to software rendering is then attempted but it in turn fails
in <a href="https://cs.chromium.org/chromium/src/content/browser/compositor/gpu_process_transport_factory.cc?dr=C&amp;q=content/browser/compositor/gpu_process_transport_factory.cc">gpu_process_transport_factory.cc</a>.</p>

<p>When Antonio joined Igalia, he
<a href="https://blogs.igalia.com/tonikitoo/2016/05/18/chromium-content_shell-running-on-wayland-desktop-weston-compositor/">did some experiments on Ozone/Wayland</a> and wrote a quick workaround
to make the software rendering fallback work when UI and GPU are in separate
processes. He was also able to run standard Linux build of Chrome on Wayland
by upstreaming more code from Intel. He also noticed that in Google’s code,
only GL drawing is happening in the GPU component (i.e. Wayland objects are
owned by the UI, contrary to Intel’s approach) which is the reason why
accelerated rendering fails in separate-process mode.
<strong>After discussion with Google developers it however became clear that
they would prefer a different approach</strong>
that is consistent with two features they are working on:</p>

<ul>
  <li>
    <p><a href="https://www.chromium.org/developers/mus-ash">Mus-ash</a>, a project to separate
the window management and shell functionality of ash from the chrome browser
process.</p>
  </li>
  <li>
    <p><a href="https://www.chromium.org/developers/design-documents/mojo">Mojo</a>, a new
API for inter-process communication.</p>
  </li>
</ul>

<p>During the project, <strong>we were able to get chrome running on Wayland using
the Mus code path, either on ChromeOS or on standard Linux build</strong>.
For that code path, GPU and UI components are
<a href="https://bugs.chromium.org/p/chromium/issues/detail?id=611505">currently running in the same process</a> so as discussed above accelerated rendering works for Wayland. However, the plan for mus is to move these two components into separate
processes and hence we need to adapt the Wayland code in
order to allow communication between the GPU (doing GL drawings) and the UI
(owning Wayland objects).</p>

<p>I’ll let Antonio describe more precisely on
<a href="https://blogs.igalia.com/tonikitoo/">his blog</a> the work we have been
doing to get <code class="language-plaintext highlighter-rouge">chrome --mash</code> running on Wayland.
In this blog post, I’m aligning with Google’s goal and hence I’m focusing on
this Mus code path. I’m going to give a quick overview of the structure of
Ozone and more specifically what is used by the Wayland platform to perform
accelerated rendering.</p>

<h1 id="ozone-architecture">Ozone Architecture</h1>

<h2 id="ozone-platform">Ozone Platform</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/ozone/public/ozone_platform.h">OzonePlatform</a>
is the main Ozone interface used to instantiate and initialize an Ozone
platform (X11, Wayland, DRM/GBM…). It provides factory getters for helper
classes (SurfaceFactoryOzone, PlatformWindow…).</p>

<p>The goal is to have OzonePlatform::InitializeForUI and
OzonePlatform::InitializeForGPU called from different processes as well as two
different Mojo connectors for the UI and GPU services respectively.
However at the time of writing, the two components are only in
different threads <em>in the same process</em>. There is also only one Mojo connector
available: The one for the <code class="language-plaintext highlighter-rouge">service:ui</code> service, passed to
OzonePlatform::InitializeForUI.</p>

<p>Two important implementations to consider in this project are <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/ozone_platform_wayland.cc">OzonePlatformWayland</a> (the one we work on) and <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/drm/ozone_platform_gbm.cc">OzonePlatformGbm</a> (the one that seems the best maintained and tested upstream).</p>

<h2 id="native-display-delegate">Native Display Delegate</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/display/types/native_display_delegate.h?q=NativeDisplayDelegate">NativeDisplayDelegate</a> is used to perform display configuration. The DRM/GBM platform has its own <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/drm/host/drm_native_display_delegate.h">DrmNativeDisplayDelegate</a> implementation. For the Wayland platform, we do not actually need real display devices, so we just do as for X11 and use the <a href="https://cs.chromium.org/chromium/src/ui/display/fake_display_delegate.h">FakeDisplayDelegate</a> class. See
<a href="https://codereview.chromium.org/2389053003/">Issue 2389053003</a>.</p>

<h2 id="window">Window</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/gfx/native_widget_types.h?q=AcceleratedWidget">AcceleratedWidget</a> is just a platform-specific object representing a surface on which compositors can paint pixels.</p>

<p><a href="https://cs.chromium.org/chromium/src/ui/platform_window/platform_window.h">PlatformWindow</a> represents a single window in the underlying platform windowing system with the usual property: It can be minimized, maximized, closed, put in fullscreen, etc</p>

<p><a href="https://cs.chromium.org/chromium/src/ui/platform_window_delegate.h">PlatformWindowDelegate</a>. This is just a delegate to which the PlatformWindow sends events like e.g. OnBoundsChanged.</p>

<p>The implementations of PlatformWindow used for the Wayland and DRM/GBM platforms are respectively <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/wayland_window.h">WaylandWindow</a> and <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/drm/gpu/drm_window.h">DrmWindow</a>. At the moment, several features in WaylandWindow are not fully implemented but the minimal code to paint content into the window is present.</p>

<h2 id="surface-and-opengl">Surface and OpenGL</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/ozone/public/surface_factory_ozone.h">SurfaceFactoryOzone</a> provides surface to be used to paint on a window.
The implementations for the Wayland and DRM/GBM platforms are respectively <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/wayland_surface_factory.h">WaylandSurfaceFactory</a> and <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/drm/gpu/gbm_surface_factory.h">GbmSurfaceFactory</a>. There are two options:</p>

<ul>
  <li>Accelerated drawing (GL path). This is done via a <a href="https://cs.chromium.org/chromium/src/ui/ozone/public/gl_ozone.h">GLOzone</a> instance returned by SurfaceFactoryOzone::GetGLOzone</li>
  <li>Software Drawing (Skia). This is done via a <a href="https://cs.chromium.org/chromium/src/ui/ozone/public/surface_ozone_canvas.h">SurfaceOzoneCanvas</a> instance returned by SurfaceFactoryOzone::CreateCanvasForWidget.</li>
</ul>

<p>In this project, we focus on accelerated rendering and on EGL, so we consider the <a href="https://cs.chromium.org/chromium/src/ui/ozone/common/gl_ozone_egl.h">GLOzoneEGL</a> class. The following virtual pure functions must be implemented in derived class:</p>

<ul>
  <li>GLOzoneEGL::LoadGLES2Bindings, performing the GL initalization. In general, <a href="https://cs.chromium.org/chromium/src/ui/ozone/common/egl_util.cc?q=LoadDefaultEGLGLES2Bindings">the default works well</a>.</li>
  <li>GLOzoneEGL::CreateOffscreenGLSurface returning an offscreen <a href="https://cs.chromium.org/chromium/src/ui/gl/gl_surface.h">GLSurface</a> of the specified dimension. It seems that it is mostly needed to create a dummy zero-dimensional offscreen surface during initialization. Hence the <a href="https://cs.chromium.org/chromium/src/ui/gl/gl_surface_egl.h?q=SurfacelessEGL">generic SurfacelessEGL</a> should work fine.
See <a href="https://codereview.chromium.org/2387063002/">Issue 2387063002</a>.</li>
  <li>GLOzoneEGL::GetNativeDisplay returns the EGL display connection to use.</li>
  <li>GLOzoneEGL::CreateViewGLSurface returns a new <a href="https://cs.chromium.org/chromium/src/ui/gl/gl_surface.h">GLSurface</a> associated to a gfx::AcceleratedWidget.</li>
</ul>

<p>SurfaceFactoryOzone also provides functions to create <a href="https://cs.chromium.org/chromium/src/ui/ozone/public/native_pixmap.h">NativePixmap</a>, which represents a  buffer that can be directly imported via GL for rendering, or exported via dma-buf fds. The DRM/GBM platform implements it and uses <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/drm/gpu/gbm_buffer.h?q=GbmPixmap">GbmPixmap</a>. For now, such pixmap objects are not needed by the Wayland platform so the SurfaceFactoryOzone function members are not implemented.</p>

<p>The instances of GLSurface returned by CreateViewGLSurface for the Wayland and DRM/GBM platforms are respectively <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/gl_surface_wayland.h">GLSurfaceWayland</a> and <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/drm/gpu/gbm_surface.h">GbmSurface</a>. GLSurfaceWayland is just a <a href="https://cs.chromium.org/chromium/src/ui/gl/gl_surface_egl.h?q=NativeViewGLSurfaceEGL">gl::NativeViewGLSurfaceEGL</a> associated to a window created by <code class="language-plaintext highlighter-rouge">wl_egl_window_create</code>. GbmSurface instead provides surface-like
semantics by deriving from <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/drm/gpu/gbm_surfaceless.h">GbmSurfaceless</a> itself deriving from <a href="https://cs.chromium.org/chromium/src/ui/gl/gl_surface_egl.h?q=SurfacelessEGL">gl::SurfacelessEGL</a>. Internally, a framebuffer is bound automatically for GL drawing in the GPU and the result are exported to the UI via pixmaps.</p>

<h1 id="wayland-platform">Wayland Platform</h1>

<h2 id="wayland-connection">Wayland Connection</h2>

<p><a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/wayland_connection.h">WaylandConnection</a> is a class specific to the Wayland platform that helps to instantiate all the objects necessary to communicate with the Wayland display server.</p>

<p>It also manages a map from gfx::AcceleratedWidget instances to WaylandWindow instances that you can modify with the public GetWindow, AddWindow and RemoveWindow function members.</p>

<h2 id="wayland-platform-initialization">Wayland Platform Initialization</h2>

<ul>
  <li>
    <p>OzonePlatformWayland::InitializeUI is called from the UI thread. It creates
instances of WaylandConnection and WaylandSurfaceFactory as members of
OzonePlatformWayland. The Mojo connection of the <code class="language-plaintext highlighter-rouge">service:ui</code> service is
discarded.</p>
  </li>
  <li>
    <p>OzonePlatformWayland::InitializeGPU in the same process but a different
thread. The WaylandConnection and WaylandSurfaceFactory members previously
created are hence accessible from the GPU thread too. Nothing is done by
this initialization function.</p>
  </li>
</ul>

<h2 id="wayland-window">Wayland Window</h2>

<p>A <a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/wayland_window.h">WaylandWindow</a> is tied to a WaylandConnection and takes care of registering and
unregistering itself to that WaylandConnection. It is merely a wrapper to
native Wayland surfaces (wl_surface and xdg_surface) with additional window
bounds. It also maintains communication with the PlatformWindowDelegate.</p>

<h2 id="wayland-surface-and-opengl">Wayland Surface and OpenGL</h2>

<p>Currently, the constructor of
<a href="https://cs.chromium.org/chromium/src/ui/ozone/platform/wayland/wayland_surface_factory.h">WaylandSurfaceFactory</a> receives the
WaylandConnection. Because we want the UI process to hold the WaylandConnection
and the GPU process to use WaylandSurfaceFactory for the GL rendering, the
current setup will not work after mus is split. Instead, we should pass it the
Mojo connector of the <code class="language-plaintext highlighter-rouge">service:gpu</code> service in order to indirectly communicate with
the <code class="language-plaintext highlighter-rouge">service:ui</code> service (for testing purpose, we can for now just use the Mojo
connector of the <code class="language-plaintext highlighter-rouge">service:ui</code> service passed to OzonePlatformWayland::InitializeUI).</p>

<p>The WaylandSurfaceFactory::CreateCanvasForWidget function and the WaylandCanvasSurface instance created require the WaylandConnection. However, they are used for software rendering so we can ignore them for now.</p>

<p>GLOzoneEGL::LoadGLES2Bindings and GLOzoneEGL::CreateOffscreenGLSurface do not seem fundamental here and they do not need any Wayland-specific code. Hence we can probably just keep the current default implementations.</p>

<p>At the moment GLOzoneEGLWayland::GetNativeDisplay just returns a native display provided by the WaylandConnection. It seems that we will not be able to do so when the WaylandConnection is no longer available on the GPU side. Probably we should just do like GLOzoneEGLGbm and return EGL_DEFAULT_DISPLAY.</p>

<p>The remaining GLOzoneEGLWayland::CreateViewGLSurface uses WaylandConnection::GetWindow to retrieve the WaylandWindow associated to AcceleratedWidget to draw on.
This window provides a wl_surface and sizes that can be passed to wl_egl_window_create to create an egl_window. Then as said in the previous paragraph, a GLSurfaceWayland instance is created which is merely a gl::NativeViewGLSurfaceEGL associated to the egl_window.</p>

<h1 id="conclusion">Conclusion</h1>

<p>In this blog post, an overview of the Ozone Architecture was provided, with
focus on the Wayland platform. It also contains
an analysis of how we could get accelerated rendering in a separate GPU process
aligned with Google’s goals (Mus+ash and Mojo) and hence have it
well-integrated with upstream code.</p>

<p>The main problem is that <strong>the GLOzoneEGLWayland code
is very tied to the Wayland native objects</strong> (connection, surface, window…).
We should instead only provide a Mojo connector to the GLOzoneEGLWayland
class and hence to the GLSurfaceWayland class it constructs.
Instances of WaylandWindow and WaylandConnector will only live on the UI side
while the GL classes will live on the GPU side.</p>

<p>The GLSurfaceWayland should be rewritten to derive from SurfacelessEGL instead
of NativeViewGLSurfaceEGL. <strong>We would then follow what is done in GbmSurface</strong>
to provide some surface-like semantics but without the need to have a real
egl_window object. Under the hood, the GL drawings will be performed on
a framebuffer.</p>

<p>We should then <strong>find a way to export those framebuffers to the UI component via
the Mojo connector</strong>. Again, following the DRM/GBM code with this NativePixmap
objects seems the right option. At the end, the UI would convert the buffers
into wl_buffers that can finally be attach to the wl_surface of the WaylandWindow.</p>

<p>During the past two months we have been maintaining the upstream Ozone code and
made the Wayland platform work again. <strong>Try bots now build and run tests for the
Wayland platform</strong> and we expect that such continuous testing will make the whole
thing more robust. We have also been working on <strong>making Linux desktop work
with the Mus+ash code path</strong> and started
<strong>encouraging experiments of Mojo communication between the UI and GPU
components of the Wayland platform</strong>.</p>

<div>
<div style="width: 364px; margin-left: auto; margin-right: auto;"><a href="http://www.igalia.com"><img src="https://frederic-wang.fr/images/igalia-logo-364x130.png" width="364" height="130" alt="Igalia Logo" /></a></div>
<div style="width: 763px; margin-left: auto; margin-right: auto;"><a href="https://www.renesas.com/en-eu/"><img src="https://frederic-wang.fr/images/renesas_logomark_l.jpg" width="763" height="130" alt="Renesas Logo" /></a></div>
</div>

<p>It is really great to work with Antonio on this project and we are looking
forward to continuing the collaboration on this with Google and Ozone
developers. Last but not least, I would like to
<strong>thank Renesas for supporting Igalia in this work to add Wayland support to chromium</strong>.</p>

{% endraw %}
