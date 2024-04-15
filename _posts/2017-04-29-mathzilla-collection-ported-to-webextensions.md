---
layout: post
title: "MathZilla collection ported to WebExtensions"
tags: mathml mozilla igalia
---

{% raw %}

  <p><a href="https://addons.mozilla.org/en-US/collections/fred_wang/mathzilla/">MathZilla</a>
is a collection of MathML-related add-ons for Mozilla
applications. It provides nice features such as
forcing native MathML rendering (e.g. on Wikipedia),
using Web fonts to render MathML or
providing a context menu item to copy math formulas into the clipboard.</p>

<p>Initially written as a single
<a href="https://developer.mozilla.org/en-US/Add-ons/Overlay_Extensions">XUL overlay extension</a> (with even binary code for the LaTeX-to-MathML converter)
it grows up as a collection of restartless add-ons using
<a href="https://developer.mozilla.org/en-US/Add-ons/Bootstrapped_extensions">bootstrapped</a>
or <a href="https://developer.mozilla.org/en-US/Add-ons/SDK">SDK-based</a> extensions,
following the evolution of Mozilla’s recommendations.
Also, SDK-based extensions were first generated using
a Python program called
<a href="https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/cfx">cfx</a>
before Mozilla recommended to switch to a JS-based replacement called
<a href="https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/jpm">jpm</a>.</p>

<p>Mozilla <a href="https://blog.mozilla.org/addons/2015/08/21/the-future-of-developing-firefox-add-ons/">announced some time ago</a> that they will transition to the
<a href="https://developer.mozilla.org/en-US/Add-ons/WebExtensions">WebExtensions</a>
format. On the one hand this sounds bad because developers have to re-write
their legacy add-ons again and actually
be sure that the transition is even possible or does break anything.
On the other hand it is good for long-term interoperability since e.g.
Chromium browsers or Microsoft Edge support that format. My colleague
Michael Catanzaro also mentioned in a recent blog post <a href="https://blogs.gnome.org/mcatanzaro/2017/03/23/a-web-browser-for-awesome-people-epiphany-3-24/">that WebExtensions are considered for Epiphany too</a>. It is not clear what Mozilla’s plan is for
<a href="https://wiki.mozilla.org/Add-ons/2017#Thunderbird">Thunderbird</a> or
<a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1320556">SeaMonkey</a> but hopefully
they will use that format too (in the past I was suggested to
<a href="https://github.com/fred-wang/Mathzilla/issues/27">make the MathZilla add-ons compatible with SeaMonkey</a>).</p>

<p><strong>Recently, Mozilla announced their <a href="https://blog.mozilla.org/addons/2017/02/16/the-road-to-firefox-57-compatibility-milestones/">plans for Firefox 57</a> which
is basically to allow only add-ons written as WebExtensions</strong>. This means I had
to re-write the Mathzilla add-ons again or they will stop working at the end of the
year. In general, I believe the features have been preserved although <strong>there might be some small behavior changes or minor bugs due to the WebExtensions format</strong>. Please check the GitHub bug trackers and release notes for known
issues and report any other problems you find.
Finally, I reorganized a bit the git repositories and add-on names.
Here is the updated list (some add-ons are still being reviewed by Mozilla):</p>

<ul>
  <li><a href="https://github.com/fred-wang/MathFonts/tree/master/webextension">MathML Fonts</a> (<strong>~2300 users</strong>) - Provide <a href="https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts">MathML fonts</a> as Web fonts, which is useful when they can not
be installed (e.g. Firefox for Android).</li>
  <li><a href="https://github.com/fred-wang/webextension-native-mathml">Native MathML</a> (<strong>~1400 users</strong>) - Force MathJax/KaTeX/MediaWiki to use native MathML rendering.</li>
  <li><a href="https://github.com/fred-wang/webextension-mathml-copy">MathML Copy</a> (<strong>~500 users</strong>) - Add context menu items to copy a MathML formula or other annotations attached to it (e.g. LaTeX) into the clipboard.</li>
  <li><a href="https://github.com/fred-wang/TeXZilla/tree/master/webextension">TeXZilla</a> (<strong>~500 users</strong>) - Add-on giving access to TeXZilla, a Unicode TeX-to-MathML converter.</li>
  <li><a href="https://github.com/fred-wang/webextension-mathml-font-settings">MathML Font Settings</a> (<strong>~300 users</strong>) - Add context menu items to configure MathML font settings. Note that in recent Mozilla versions the advanced font preferences menu allows to configure “Fonts for Mathematics”.</li>
  <li><a href="https://github.com/fred-wang/webextension-presentation-mathml-polyfill">Presentation MathML Polyfill</a> (<strong>~200 users</strong>) - Add support for some advanced presentation MathML features (currently using David Carlisle’s “mml3ff” XSLT stylesheet).</li>
  <li><a href="https://github.com/fred-wang/webextension-content-mathml-polyfill">Content MathML Polyfill</a> (<strong>~200 users</strong>) - Add support for some content MathML features (currently using David Carlisle’s “ctop” XSLT stylesheet).</li>
  <li><a href="https://github.com/fred-wang/webextension-mathml-zoom">MathML Zoom</a> (<strong>~100 users</strong>) - Allow zooming of mathematical formulas.</li>
  <li><a href="https://github.com/fred-wang/webextension-mathml-view-source/">MathML View Source</a> (<strong>experimental</strong>) - This is a re-writing of Mozilla’s ‘view MathML source’ feature with better syntax highlighting and serialization. The idea originated from <a href="https://groups.google.com/forum/#!topic/mozilla.dev.tech.mathml/S0CdPUJuQnY">this thread</a>.</li>
  <li><a href="https://github.com/fred-wang/webextension-image-to-mathml">Image To MathML</a> (<strong>experimental</strong>) - Try and convert images of mathematical formulas into MathML. It has <a href="https://github.com/fred-wang/webextension-image-to-mathml/issues/1">not been ported to WebExtensions yet</a> and I do not plan to do it in the short term.</li>
</ul>

<p>As a conclusion, <strong>I’d like to thank all the MathZilla users for their kind comments, bug reporting and financial support</strong>. The next step will probably be to ensure addons work in more browsers but that will be for another time ;-)</p>


{% endraw %}
