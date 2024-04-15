---
layout: post
title: "Review of Igalia's Web Platform activities (H1 2018)"
tags: igalia
---

{% raw %}

  <p>This is the semiyearly report to let people know a bit more about Igalia’s activities around <a href="https://en.wikipedia.org/wiki/Web_platform">the Web Platform</a>,
focusing on the activity of the first semester of year 2018.</p>

<h2 id="projects">Projects</h2>

<h3 id="javascript">Javascript</h3>

<p>Igalia has proposed and developed the specification for <a href="https://github.com/tc39/proposal-bigint/">BigInt</a>, enabling math on arbitrary-sized integers in JavaScript. Igalia has been developing implementations in <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1366287">SpiderMonkey</a> and <a href="https://bugs.webkit.org/show_bug.cgi?id=179001">JSC</a>, where core patches have landed. Chrome and Node.js shipped implementations of BigInt, and the proposal is at Stage 3 in TC39.</p>

<p>Igalia is also continuing to develop several features for JavaScript classes, including <a href="https://github.com/tc39/proposal-class-fields">class fields</a>. We developed a prototype implementation of class fields in JSC. We have maintained Stage 3 in TC39 for our specification of class features, including static variants.</p>

<p>We also participated to <a href="https://webassembly.org/">WebAssembly</a> (now at First Public Working Draft) and <a href="https://github.com/tc39/proposals/blob/master/ecma402/README.md">internationalization features</a> for new features such as Intl.RelativeTimeFormat (currently at Stage 3).</p>

<p>Finally, we have written more tests for JS language features, performed maintenance and optimization and participated to other spec discussions at TC39. Among performance optimizations, we have contributed a significant optimization to Promise performance to V8.</p>

<h3 id="accessibility">Accessibility</h3>

<p>Igalia has continued the standardization effort at the W3C. We are pleased to
announce that the following milestones have been reached:</p>

<ul>
  <li><a href="https://www.w3.org/TR/graphics-aria-1.0/">WAI-ARIA Graphics Module</a> and <a href="https://www.w3.org/TR/graphics-aam-1.0/">Graphics Accessibility API Mappings</a> moved to proposed recommendation.</li>
  <li><a href="https://www.w3.org/TR/accname-1.1/">Accessible Name and Description Computation</a> moved to Candidate Recommendation.</li>
</ul>

<p>A new <a href="https://www.w3.org/2015/10/aria-charter.html">charter</a> for the ARIA WG as well as drafts for <a href="https://w3c.github.io/aria/">ARIA 1.2</a> and <a href="https://w3c.github.io/core-aam/">Core Accessibility API Mappings 1.2</a> are in preparation and are expected to be published this summer.</p>

<p>On the development side, we implemented new ARIA features and fixed several bugs in WebKit and Gecko. We have refined platform-specific tools that are needed to automate accessibility Web Platform Tests (examine the accessibility tree, obtain information about accessible objects, listen for accessibility events, etc) and hope we will be able to integrate them in Web Platform Tests. Finally we continued maintenance of the <a href="https://help.gnome.org/users/orca/stable/">Orca</a> screen reader, in particular fixing some accessibility-event-flood issues in Caja and Nautilus that had significant impact on Orca users.</p>

<h3 id="web-platform-predictability">Web Platform Predictability</h3>

<p>Thanks to support from <a href="http://www.bloomberg.com/company/">Bloomberg</a>, we were
able to improve interoperability for various Editing/Selection use cases.
For example when <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=731000">using backspace to delete text content just after a table</a> (<a href="https://github.com/w3c/editing/issues/164">W3C issue</a>) or <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=731913">deleting a list item inside a content cell</a>.</p>

<p>We were also pleased to continue our collaboration with <a href="https://www.ampproject.org/">the AMP project</a>.
They provide us a list of bugs and enhancement requests
(mostly for the WebKit iOS port) with concrete use cases and repro cases.
We check the status and plans in WebKit, do
debugging/analysis and of course actually submit patches to address
the issues. That’s not always easy (e.g. when it is touching proprietary code
or requires to find some specific reviewers) but at least we make discussions move
forward. The topics are very diverse, it can be about
<a href="https://bugs.webkit.org/show_bug.cgi?id=186593">MessageChannel API</a>,
<a href="https://bugs.webkit.org/show_bug.cgi?id=106133">CSSOM View</a>,
<a href="https://bugs.webkit.org/show_bug.cgi?id=177684">CSS transitions</a>,
<a href="https://bugs.webkit.org/show_bug.cgi?id=170784">CSS animations</a>,
<a href="https://bugs.webkit.org/show_bug.cgi?id=149264">iOS frame scrolling</a>
<a href="https://bugs.webkit.org/show_bug.cgi?id=183586">custom elements</a> or
<a href="https://bugs.webkit.org/show_bug.cgi?id=165627">navigating special links</a>
and many others.</p>

<p>In general, our projects are always a good opportunity to write new
<a href="https://github.com/web-platform-tests/wpt">Web Platform Tests</a> import them
in WebKit/Chromium/Mozilla or improve the testing infrastructure. We have been able
to work on tests for several specifications we work on.</p>

<h3 id="css">CSS</h3>

<p>Thanks to support from <a href="http://www.bloomberg.com/company/">Bloomberg</a> we’ve been pursuing our activities around CSS:</p>

<ul>
  <li>CSS Grid Layout: we <a href="https://blogs.igalia.com/mrego/2018/04/04/getting-rid-of-grid-prefix-on-css-grid-layout-gutter-properties/">removed “grid-“ prefix from gutter properties</a> and added support percentage to column-gap property in Multicolumn. We worked on <a href="https://blogs.igalia.com/jfernandez/2017/05/03/can-i-use-css-box-alignment/">baseline alignment</a>. Finally we are now improving the memory structures of the implementation in order to make bigger grids possible.</li>
  <li>Composition underline is no longer always black in Chromium, it uses now the <a href="https://twitter.com/regocas/status/978638089781465088">current text color for by default</a></li>
  <li>CSS Containment: We updated Chromium implementation to align with the spec and fixed several bugs.</li>
  <li>CSS Text 3: We started to implement the new <a href="https://drafts.csswg.org/css-text-3/#valdef-overflow-wrap-break-spaces">CSS value ‘break-spaces’</a></li>
</ul>

<p>We also got more involved in the CSS Working Group, in particular participating to the <a href="https://blogs.igalia.com/mrego/2018/04/16/csswg-f2f-berlin-2018/">face-to-face meeting in Berlin</a> and will attend <a href="https://www.w3.org/wiki/TPAC/2018">TPAC’s meeting in October</a>.</p>

<h3 id="webkit">WebKit</h3>

<p>We have also continued improving the web platform implementation of some Linux ports of WebKit (namely <a href="https://webkitgtk.org/">GTK</a> and <a href="https://www.igalia.com/wpe/">WPE</a>). A lot of this work was possible thanks to the financial support of <a href="https://www.metrological.com/index.html">Metrological</a>.</p>

<ul>
  <li>We improved <a href="https://developer.mozilla.org/en-US/docs/Web/WebDriver">Web Driver</a> support and made it work with WPE too.</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API">Web Animations</a> are now enabled.</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API">Service Workers</a> are now <a href="https://bugs.webkit.org/show_bug.cgi?id=178576">enabled behind an experimental features flag</a>.</li>
  <li><a href="https://bugs.webkit.org/show_bug.cgi?id=182424">We implemented most</a> of the missing functionality of <a href="https://developer.mozilla.org/en-US/docs/Web/API/ImageBitmap">ImageBitmap</a>.</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/OffscreenCanvas">OffscreenCanvas</a> is now <a href="https://bugs.webkit.org/show_bug.cgi?id=183720">mostly implemented</a>, but pending review.</li>
  <li><a href="https://github.com/web-platform-tests/wpt">Web Platform Tests</a> integration: We landed a patch to <a href="https://bugs.webkit.org/show_bug.cgi?id=183356">make possible to run tests against the official Web Platform Tests repository</a>.</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API">WebRTC</a>: We made the raspberry pi work with Firefox and Chrome properly and started pushing upstream all the branch. We have already upstreamed all the changes required in the current WebKit classes, the libwebrtc compilation and the getUserMedia support. We have two main pending patches: PeerConnection support and EnumerateDevices support.</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Media_Source_Extensions_API">Media Source Extensions</a>: We refined our implementation and fixed several bugs ; dealing with the corresponding issues on the gstreamer side.</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API">WebVR</a>: Most of the API (85%) is now implemented using OpenVR and we can already get the <a href="https://www.youtube.com/watch?v=QS5uJdqvuD8">tracking information</a>.</li>
</ul>

<h2 id="other-activities">Other activities</h2>

<h3 id="preparation-of-web-engines-hackfest-2018">Preparation of Web Engines Hackfest 2018</h3>

<p>Igalia has been organizing and hosting the <a href="https://webengineshackfest.org/">Web Engines Hackfest</a> since 2009, a three days event where Web Platform developers can meet, discuss and work together. We are still working on the list of invited, <a href="https://webengineshackfest.org/#sponsors">sponsors</a> and talks but you can already save the date: It will happen from 1st to 3rd of October in A Coruña!</p>

<h3 id="new-igalians">New Igalians</h3>

<p>This semester, new developers have joined Igalia to pursue the Web platform effort:</p>

<ul>
  <li>
    <p><a href="https://www.igalia.com/igalia-247/igalian/item/rbuis/">Rob Buis</a>, a Dutch developer currently living in Germany. He is a well-known member of the Chromium community and is currently helping on the web platform implementation in WebKit.</p>
  </li>
  <li>
    <p><a href="https://www.igalia.com/igalia-247/igalian/item/qzhang/">Qiuyi Zhang (Joyee)</a>, based in China is a prominent member of the Node.js community who is now also assisting our compilers team on V8 developments.</p>
  </li>
  <li>
    <p><a href="https://www.igalia.com/igalia-247/igalian/item/dinfuehr/">Dominik Infuer</a>, an Austrian specialist in compilers and programming language implementation who is currently helping on our JSC effort.</p>
  </li>
</ul>

<h3 id="coding-experience-programs">Coding Experience Programs</h3>

<p>Two students have started a <a href="https://www.igalia.com/about-us/coding-experience">coding experience program</a> some weeks ago:</p>

<ul>
  <li>
    <p>Oriol Brufau, a recent graduate in math from Spain who has been an active collaborator of the CSS Working Group and a contributor to the Mozilla project. He is working on the CSS Logical Properties and Values specification, implementing it in Chromium implementation.</p>
  </li>
  <li>
    <p>Darshan Kadu, a computer science student from India, who contributed to GIMP and Blender. He is working on Web Platform Tests with focus on WebKit’s infrastructure and the GTK &amp; WPE ports in particular.</p>
  </li>
</ul>

<p>Additionally, <a href="https://github.com/caiolima">Caio Lima</a> is continuing his coding experience in Igalia and is among other things working on implementing BigInt in JSC.</p>

<h2 id="conclusion">Conclusion</h2>

<p>Thank you for reading this blog post and we look forward to more work on the web platform this semester!</p>

{% endraw %}
