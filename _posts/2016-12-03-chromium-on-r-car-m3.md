---
layout: post
title: "Chromium on R-Car M3 & AGL/Wayland"
tags: igalia chromium
---

{% raw %}

  <p>As my fellow igalian
<a href="https://www.igalia.com/nc/igalia-247/igalian/item/agomes/">Antonio Gomes</a>
explained
<a href="https://blogs.igalia.com/tonikitoo/2016/11/14/chromium-ozone-wayland-and-beyond/">on his blog</a>, we have recenly been working on making the master
branch of Chromium run on Linux Desktop using the upstream
<a href="https://chromium.googlesource.com/chromium/src/+/master/docs/ozone_overview.md">Ozone/Wayland backend</a>.
This effort is supported by <a href="https://www.renesas.com/">Renesas</a> and they were
interested to rely on these recent developments to showcase
Chromium running on the latest generation of their
<a href="https://www.renesas.com/en-us/solutions/automotive/products.html">R-Car systems-on-chip for automotive applications</a>. Ideally, they were willing to see this
happening for the
<a href="https://www.automotivelinux.org/">Automotive Grade Linux</a> distribution.</p>

<div>
<div style="width: 364px; margin-left: auto; margin-right: auto;"><a href="http://www.igalia.com"><img src="https://frederic-wang.fr/images/igalia-logo-364x130.png" width="364" height="130" alt="Igalia Logo" /></a></div>
<div style="width: 763px; margin-left: auto; margin-right: auto;"><a href="https://www.renesas.com/en-eu/"><img src="https://frederic-wang.fr/images/renesas_logomark_l.jpg" width="763" height="130" alt="Renesas Logo" /></a></div>
</div>

<p>Luckily, support for
<a href="https://www.renesas.com/en-us/solutions/automotive/products/rcar-m3.html">R-Car M3</a> was
already available in the development branch of AGL and
the <a href="https://wiki.automotivelinux.org/start/building_for_the_renesas_r-car_m2">AGL instructions for R-Car M2</a> actually worked pretty well for M3 too
<em>mutatis mutandis</em>. There is also an
<a href="https://github.com/OSSystems/meta-browser">OpenEmbedded/Yocto BSP layer for Chromium</a> but unfortunately Wayland is only supported up to m48 (using the Ozone backend from <a href="https://github.com/01org/ozone-wayland">Intel’s fork</a>) and X11
is only supported up to m52. Hence we created a (for-now-private) fork of
meta-browser that:</p>

<ul>
  <li>Uses the latest development version of Chromium, in particular the
Linux/Ozone/Mash/Wayland support Igalia has been working on recently.</li>
  <li>Relies on the new GN build system rather than the deprecated GYP one.</li>
  <li>Supports the ARM64 architecture instead of just ARM32.</li>
  <li>Installs more resources such as <a href="https://chromium.googlesource.com/chromium/src/+/master/services/service_manager/README.md">Mojo service manifests</a>.</li>
  <li>Applies more patches (e.g. build fixes or the workaround for <a href="https://codereview.chromium.org/2485673002/">issue 2485673002</a>).</li>
</ul>

<p>Renesas also provided us some R-Car M3 boards.
I received my package this week and hence
was able to start playing with it on Wednesday. Again, the
<a href="https://wiki.automotivelinux.org/start/building_for_the_renesas_r-car_m2">AGL instructions for R-Car M2</a> apply well to M3 and the
<a href="http://www.elinux.org/R-Car/Boards/M3SK">elinux page</a> is very helpful to
understand the various parts of the board. After having started AGL on the
board and opened a Weston terminal (using mouse &amp; keyboard as on the video or
using ssh) I was able to run chromium via the following command:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>/usr/bin/chromium/chrome --mash --ozone-plaform=wayland \
                         --user-data-dir=/tmp/user-data-dir \
                         --no-sandbox
</code></pre></div></div>

<p>The first line is the usual command currently used to execute
Ozone/Mash/Wayland. The second line works around the fact that the AGL demo is
running as root. The third line disables <a href="https://chromium.googlesource.com/chromium/src/+/master/docs/linux_sandboxing.md#Sandbox-types-summary">sandbox</a>
because the deprecated setuid sandbox does not work with Ozone and the newer
user namespaces sandbox is not supported by the AGL kernel.</p>

<p>The <a href="https://player.vimeo.com/video/194030827">following video</a> a gives an
overview of the hardware preparation as well as some basic tests with
<a href="http://bouncyballs.org/">bouncyballs.org</a> and
<a href="http://webengineshackfest.org/">webengineshackfest.org</a>:</p>

<div style="width: 640px; margin-left: auto; margin-right: auto;"><iframe src="https://player.vimeo.com/video/194030827" width="640" height="360" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen=""><p><a href="https://vimeo.com/194030827">chromium-57-r-car-M3-2016-12-02</a> from <a href="https://vimeo.com/user41690319">Fr&eacute;d&eacute;ric Wang</a> on <a href="https://vimeo.com">Vimeo</a>.</p></iframe></div>

<p>You can see that chromium runs relatively smoothly but we will do more testing
to confirm these initial experiments. Also, we find the general issues with
Linux/Ozone/Mash (internal VS external windows, no fullscreen, keyboard
restricted to US layout, unwanted ChromeOS widgets etc) but we expect to
continue to collaborate with Google to fix these bugs!</p>

{% endraw %}
