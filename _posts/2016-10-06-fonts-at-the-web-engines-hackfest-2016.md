---
layout: post
title: "Fonts at the Web Engines Hackfest 2016"
tags: mathml igalia fonts mozilla chromium
---

{% raw %}

  <p>Last week I travelled to
<a href="https://en.wikipedia.org/wiki/Galicia_%28Spain%29">Galicia</a> for one of the
regular gatherings organized by <a href="http://igalia.com/">Igalia</a>. It was a great
pleasure
to meet again all the Igalians and friends. Moreover, this time was a bit
special since we celebrated our <a href="https://www.igalia.com/nc/igalia-247/news/item/igalia-celebrates-our-15th-anniversary/">15th anniversary</a> :-)</p>

<div style="width: 600px; margin-left: auto; margin-right: auto; text-align: center;">
<div style="width: 500px; margin-left: auto; margin-right: auto;"><a href="https://secure.flickr.com/photos/bertogg/29962370082/" title="Igalia Summit October 2016"><img src="https://c3.staticflickr.com/9/8554/29962370082_024203fd6f.jpg" width="500" height="375" alt="Igalia Summit October 2016" /></a></div> <small>Photo by <a href="https://secure.flickr.com/photos/bertogg/">Alberto Garcia</a> licensed under <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC BY-SA 2.0</a>.</small></div>

<p><a data-flickr-embed="true" href="https://www.flickr.com/photos/bertogg/29962370082/in/photostream/" title="Igalia Summit October 2016"></a><script async="" src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script></p>

<p>I also attended the third edition of the
<a href="http://www.webengineshackfest.org/">Web Engines Hackfest</a>,
sponsored by Igalia,
<a href="https://www.collabora.com/">Collabora</a> and <a href="https://www.mozilla.org/">Mozilla</a>.
This year, we had various participants from the Web Platform including folks from
Apple, Collabora, Google, Igalia, Huawei, Mozilla or Red Hat.
For my first hackfest as an Igalian, I invited some experts on fonts &amp;
math rendering to collaborate
on OpenType MATH support HarfBuzz and its use in math rendering engines.
In this blog post, I am going to focus on the work I have made
with <a href="http://behdad.org/">Behdad Esfahbod</a> and
<a href="http://khaledhosny.org/">Khaled Hosny</a>. I think it was again a great and
productive hackfest and I am looking forward to attending the next edition!</p>

<h2 id="opentype-math-in-harfbuzz">OpenType MATH in HarfBuzz</h2>

<div style="width: 600px; margin-left: auto; margin-right: auto; text-align: center;">
<div style="width: 500px; margin-left: auto; margin-right: auto;"><a href="https://www.flickr.com/photos/webhackfest/30112185606/in/album-72157673583191111/" title="Behdad talking about HarfBuzz"><img src="https://c7.staticflickr.com/6/5279/30112185606_c3c14fcd66.jpg" width="500" height="281" alt="Web Engines Hackfest, main room" /></a></div> <small>Photo by <a href="https://www.flickr.com/photos/webhackfest/">@webengineshackfest</a> licensed under <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC BY-SA 2.0</a>.</small></div>

<p>Behdad <a href="https://github.com/Igalia/webengineshackfest/wiki#scheduling">gave a talk</a> with a nice overview of the work accomplished in
<a href="https://freedesktop.org/wiki/Software/HarfBuzz/">HarfBuzz</a> during ten years.
One thing appearing recently in HarfBuzz is the need for APIs to parse
OpenType tables on all platforms. As part of my job at Igalia, I had started
to experiment adding support for the
<a href="https://frederic-wang.fr/opentype-math-in-harfbuzz.html">MATH table</a>
some months ago and it was
nice to have Behdad finally available to review, fix and improve commits.</p>

<p>When I talked to Mozilla employee
<a href="http://blog.karlt.net">Karl Tomlinson</a>, it became apparent that
the simple shaping API for stretchy operators proposed
<a href="https://frederic-wang.fr/opentype-math-in-harfbuzz.html">in my blog post</a>
would not cover all the special cases currently implemented in Gecko. Moreover,
this shaping API is also very similar to another one existing in HarfBuzz for
non-math script so we would have to decide the best way to share the logic.</p>

<p>As a consequence, we decided for now to focus on providing an API to access all
the data of the MATH table. After the Web Engines Hackfest,
<a href="https://github.com/behdad/harfbuzz/blob/master/src/hb-ot-math.h">such a math API</a> is now integrated into the development
repository of HarfBuzz and will available in version 1.3.3 :-)</p>

<h2 id="mathml-in-web-rendering-engines">MathML in Web Rendering Engines</h2>

<p>Currently, several math rendering engines have their own code to parse the data
of the OpenType MATH table. But many of them actually use HarfBuzz for normal
text shaping and hence could just rely on the new math API the math rendering
too.
Before the hackfest, Khaled already had tested my work-in-progress branch with
<a href="https://github.com/khaledhosny/libmathview/">libmathview</a> and I had done the
same for <a href="https://github.com/fred-wang/chromium.src/tree/mathml">Igalia’s Chromium MathML branch</a>.</p>

<div style="text-align: center;">
   <div style="width: 600px; margin-left: auto; margin-right: auto;"><img src="https://frederic-wang.fr/images/mathml-fraction-parameters-test.png" width="600" height="464" alt="MathML Fraction parameters test" /></div>
   <small>MathML test for OpenType MATH Fraction parameters in Gecko, Blink and WebKit.</small>
</div>

<p>Once the new API landed into HarfBuzz, Khaled was also able to use it for the
<a href="https://en.wikipedia.org/wiki/XeTeX">XeTeX</a> typesetting system.
I also started to experiment this
for <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1305977">Gecko</a> and
<a href="https://bugs.webkit.org/show_bug.cgi?id=162671">WebKit</a>.
This seems to work pretty well and we get consistent results for
Gecko, Blink and WebKit! Some random thoughts:</p>

<ul>
  <li>The math data is exposed through a <code class="language-plaintext highlighter-rouge">hb_font_t</code> which contains the text size.
This means that the various values are now directly resolved and returned as a
<a href="https://en.wikipedia.org/wiki/Fixed-point_arithmetic">fixed-point number</a>
which should allow to avoid rounding errors we may currently have in
Gecko or WebKit when multiplying by float factors.</li>
  <li>HarfBuzz has some magic to automatically handle invalid offsets and sizes
that greatly simplifies the code, compared to what exist in Gecko and WebKit.</li>
  <li>Contrary to Gecko’s implementation, HarfBuzz does not cache the latest
result for glyph-specific data. Maybe we want to keep that?</li>
  <li>The WebKit changes were tested on the GTK port, where HarfBuzz is enabled.
Other ports may still need to use the existing parsing code from the
WebKit tree. Perhaps
Apple should consider adding support for the OpenType MATH table to
<a href="https://developer.apple.com/reference/coretext">CoreText</a>?</li>
</ul>

<h2 id="brotliwoff2ots-libraries">Brotli/WOFF2/OTS libraries</h2>

<div style="width: 600px; margin-left: auto; margin-right: auto; text-align: center;">
<div style="width: 500px; margin-left: auto; margin-right: auto;"><a href="https://www.flickr.com/photos/webhackfest/30147116385/in/album-72157673583191111/" title="Web Engines Hackfest, main room"><img src="https://c2.staticflickr.com/6/5232/30147116385_06a307626b.jpg" width="500" height="281" alt="Web Engines Hackfest, main room" /></a></div> <small>Photo by <a href="https://www.flickr.com/photos/webhackfest/">@webengineshackfest</a> licensed under <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC BY-SA 2.0</a>.</small></div>

<p>We also updated the copies of WOFF2 and OTS
libraries in <a href="https://bugs.webkit.org/show_bug.cgi?id=162608">WebKit</a> and
<a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1305944">Gecko</a> respectively.
This improves one <a href="https://www.w3.org/TR/WOFF2/#conform-mustNotRejectIncorrectTotalSize">requirement from the WOFF2 specification</a> and allows to
<a href="http://test.csswg.org/harness/test/woff2_dev/single/header-totalsfntsize-001/">pass the corresponding conformance test</a>.</p>

<p>Gecko, WebKit and Chromium bundle their own copy of the Brotli, WOFF2
or OTS libraries in their source repositories. However:</p>

<ul>
  <li>
    <p>We have to use more or less automated mechanisms to keep these bundled copies
up-to-date. This is especially annoying for Brotli and WOFF2 since they are
still in development and we must be sure to always integrate the latest security
fixes. Also, we get compiler warnings or coding style errors that do not exist
upstream and that must be disabled or patched until they are fixed upstream
and imported again.</p>
  </li>
  <li>
    <p>This obviously is not an optimal sharing of system library and may increase
the size of binaries.
Using shared libraries is what maintainers of Linux (or other
FLOSS systems) generally ask and this was raised during the WebKitGTK+
session. Similarly, we should really use the system Brotli/WOFF2 bundled in
future releases of Apple’s operating systems.</p>
  </li>
</ul>

<p>There are several issues that make hard for package maintainers to
provide these libraries: no released binaries or release tags, no proper build
system to generate shared libraries, use of git submodule to include one library source
code into another etc Things have
gotten a bit better for Brotli and I was able to
<a href="https://github.com/google/brotli/pull/421">tweak the CMake script to produce shared libraries</a>. For WOFF2,
<a href="https://github.com/google/woff2/issues/40">issue 40</a> and
<a href="https://github.com/google/woff2/issues/49">issue 49</a> have been inactive but
hopefully these will be addressed in the future…</p>

{% endraw %}
