---
layout: post
title: "Review of Igalia's Web Platform activities (H2 2017)"
tags: igalia mathml
---

{% raw %}

  <p>Last september, I published a first <a href="https://frederic-wang.fr/review-of-igalia-s-web-platform-activities-H1-2017.html">blog post</a> to let people know a bit more about Igalia’s activities around the Web platform, with a plan to repeat such a review each semester. The present blog post focuses on the activity of the second semester of 2017.</p>

<h2 id="accessibility">Accessibility</h2>

<p>As part of <a href="https://www.igalia.com/nc/igalia-247/news/item/our-commitment-to-diversity-and-inclusion">Igalia’s commitment to diversity and inclusion</a>, we continue our effort to standardize and implement accessibility technologies. More specifically, Igalian <a href="https://www.igalia.com/nc/igalia-247/igalian/item/jdiggs/">Joanmarie Diggs</a> continues to serve as chair of the W3C’s <a href="https://www.w3.org/WAI/ARIA/">ARIA working group</a> and as an editor of <a href="https://www.w3.org/TR/wai-aria/">Accessible Rich Internet Applications (WAI-ARIA) 1.1</a>, <a href="https://www.w3.org/TR/core-aam/">Core Accessibility API Mappings 1.1</a>, <a href="https://www.w3.org/TR/dpub-aria/">Digital Publishing WAI-ARIA Module 1.0</a>, <a href="https://www.w3.org/TR/dpub-aam/">Digital Publishing Accessibility API Mappings 1.0</a> all of which <a href="https://lists.w3.org/Archives/Public/w3c-wai-ig/2017OctDec/0239.html">became W3C Recommandations in December</a>! Work on versions 1.2 of ARIA and the Core AAM will begin in January. Stay tuned for the First Public Working Drafts.</p>

<p>We also contributed patches to fix several issues in the ARIA implementations of WebKit and Gecko and implemented support for the new DPub ARIA roles. We expect to continue this collaboration with Apple and Mozilla next year as well as to resume more active maintenance of <a href="https://help.gnome.org/users/orca/stable/">Orca</a>, the screen reader used to access graphical desktop environments in GNU/Linux.</p>

<p>Last but not least, progress continues on switching to <a href="https://github.com/w3c/web-platform-tests">Web Platform Tests</a> for ARIA and “Accessibility API Mappings” tests. This task is challenging because, unlike other aspects of the Web Platform, testing accessibility mappings cannot be done by solely examining what is rendered by the user agent. Instead, an additional tool, an “<a href="https://spec-ops.github.io/atta-api/index.html">Accessible Technology Test Adapter</a>” (ATTA) must be also be run. ATTAs work in a similar fashion to assistive technologies such as screen readers, using the implemented platform accessibility API to query information about elements and reporting what it obtains back to WPT which in turn determines if a test passed or failed. As a result, the tests are currently officially <a href="http://web-platform-tests.org/writing-tests/manual.html">manual</a> while the platform ATTAs continue to be developed and refined. We hope to make sufficient progress during 2018 that ATTA integration into WPT can begin.</p>

<h2 id="css">CSS</h2>

<p>This semester, we were glad to receive <a href="http://www.bloomberg.com/company/">Bloomberg</a>’s support again to pursue our activities around CSS. After a long commitment to CSS and a lot of feedback to Editors, <a href="https://twitter.com/regocas/status/908604005999357952">several of our members finally joined the Working Group</a>! Incidentally and as mentioned in a <a href="https://frederic-wang.fr/recent-browser-events.html">previous blog post</a>, during the <a href="https://wiki.csswg.org/planning/paris-2017">CSS Working Group face-to-face meeting in Paris</a> we got the opportunity to answer Microsoft’s questions regarding <a href="https://alistapart.com/article/the-story-of-css-grid-from-its-creators">The Story of CSS Grid, from Its Creators</a> (see also the <a href="https://www.youtube.com/watch?v=J9uaT9dggZE">video</a>). You might want to take a look at our own videos for CSS Grid Layout, regarding <a href="https://www.dropbox.com/s/co24b12wd81zaau/201709_gridlayout_alignment.mp4?dl=0">alignment and placement</a> and <a href="https://matrix.igalia.com/_matrix/media/v1/download/igalia.com/AEMEmqJXZvPAQGjlXFiCyceW">easy design</a>.</p>

<p>On the development side, we maintained and fixed bugs in Grid Layout implementation for Blink and WebKit. We also implemented alignment of positioned items in Blink and WebKit. We have several improvements and bug fixes for editing/selection from Bloomberg’s downstream branch that we’ve already upstreamed or plan to upstream. Finally, it’s worth mentioning that the <a href="https://blogs.igalia.com/mrego/2018/01/11/display-contents-is-coming/">work done on <code class="language-plaintext highlighter-rouge">display: contents</code></a> by our former coding experience student <a href="https://twitter.com/ecbos_">Emilio Cobos</a> was taken over and completed by antiik (for WebKit) and rune (for Blink) and is now enabled by default! We plan to pursue these developments next year and have various ideas. One of them is improving the way grids are stored in memory to allow huge grids (e.g. spreadsheet).</p>

<h2 id="web-platform-predictability">Web Platform Predictability</h2>

<p>One of the area where we would like to increase our activity is <a href="https://www.chromium.org/blink/platform-predictability">Web Platform Predictability</a>. This is obviously essential for our users but is also instrumental for a company like Igalia making developments on all the open source Javascript and Web engines, to ensure that our work is implemented consistently across all platforms. This semester, we were able to put more effort on this thanks to financial support from <a href="http://www.bloomberg.com/company/">Bloomberg</a> and <a href="https://www.ampproject.org/">Google AMP</a>.</p>

<p>We have implemented more
<a href="https://www.dropbox.com/s/k9y5wxw4mdrr41p/201708-sandboxing.mp4">frame sandboxing attributes WebKit</a>
to improve user safety and make control of sandboxed documents more flexible.
We improved the
<a href="https://html.spec.whatwg.org/#sandboxed-navigation-browsing-context-flag">sandboxed navigation browser context flag</a> and implemented the new
<a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-popups-to-escape-sandbox">allow-popup-to-escape-sandbox</a>, <a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-top-navigation-by-user-activation">allow-top-navigation-without-user-activation</a>, and <a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-modals">allow-modals</a> values for the <code class="language-plaintext highlighter-rouge">sandbox</code> attribute.</p>

<p>Currently, <a href="https://bugs.webkit.org/show_bug.cgi?id=149264">HTML frame scrolling</a> is not implemented in WebKit/iOS. As a consequence, one has to use the non-standard <code class="language-plaintext highlighter-rouge">-webkit-overflow-scrolling: touch</code> property on overflow nodes to emulate scrollable elements. In parallel to the progresses toward using more standard HTML frame scrolling we have also worked on annoying issues related to overflow nodes, including
<a href="https://bugs.webkit.org/show_bug.cgi?id=175135">flickering/jittering of “position: fixed” nodes</a> or <a href="https://bugs.webkit.org/show_bug.cgi?id=178789">broken Find UI</a> or a <a href="https://github.com/ampproject/amphtml/issues/11829">regression causing content to disappear</a>.</p>

<p>Another important task as part of our CSS effort was to address compatibility issues between the different browsers. For example we fixed editing bugs related to HTML List items: <a href="https://webkit.org/b/174593">WebKit’s Bug 174593</a>/<a href="https://crbug.com/744936">Chromium’s Issue 744936</a> and <a href="https://webkit.org/b/173148">WebKit’s Bug 173148</a>/<a href="https://crbug.com/731621">Chromium’s Issue 731621</a>. Inconsistencies in web engines regarding selection with floats have also been detected and we submitted the first patches for <a href="https://webkit.org/b/176096">WebKit</a> and <a href="https://crbug.com/643106">Blink</a>. Finally, we are currently improving line-breaking behavior in <a href="https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/fP1jDcQu68g/qSjd8EI8BQAJ">Blink</a> and <a href="https://bugs.webkit.org/show_bug.cgi?id=177327">WebKit</a>, which implies the implementation of new CSS values and properties defined in the last draft of the CSS Text 3 specification.</p>

<p>We expect to continue this effort on Web Platform Predictability next year and we are discussing more ideas e.g. <a href="https://github.com/WICG/webpackage">WebPackage</a> or <a href="https://drafts.csswg.org/css-flexbox/">flexbox</a> compatibility issues. For sure, <a href="https://github.com/w3c/web-platform-tests">Web Platform Tests</a> are an important aspect to ensure cross-platform inter-operability and we would like to help improving synchronization with the conformance tests of browser repositories. This includes the accessibility tests mentioned above.</p>

<h2 id="mathml">MathML</h2>

<p>Last November, we launched a <a href="https://mathml.igalia.com/">fundraising Campaign</a> to implement MathML in Chromium and presented it during Frankfurt Book Fair and TPAC. We have gotten very positive feedback so far with encouragement from people excited about this project. We strongly believe the native MathML implementation in the browsers will bring about a huge impact to STEM education across the globe and all the incumbent industries will benefit from the technology. As <a href="https://twitter.com/RickByers/status/928305865555296256">pointed out by Rick Byers</a>, the web platform is a commons and we believe that a more collective commitment and contribution are essential for making this world a better place!</p>

<p>While waiting for progress on Chromium’s side, we have provided minimal maintenance for MathML in WebKit:</p>
<ul>
  <li>We fixed all the debug ASSERTs reported on Bugzilla.</li>
  <li>We did follow-up code clean up and refactoring.</li>
  <li>We imported Web Platform tests in WebKit.</li>
  <li>We performed review of MathML patches.</li>
</ul>

<p>Regarding the last point, we would like to thank Minsheng Liu, a new volunteer who has started to contribute patches to WebKit to fix issues with MathML operators. He is willing to continue to work on MathML development in 2018 as well so stay tuned for more improvements!</p>

<h2 id="javascript">Javascript</h2>

<p>During the second semester of 2017, we worked on the design, standardization and implementation of several JavaScript features thanks to sponsorship from <a href="http://www.bloomberg.com/company/">Bloomberg</a> and <a href="https://www.mozilla.org/">Mozilla</a>.</p>

<p>One of the new features we focused on recently is <a href="https://github.com/tc39/proposal-bigint">BigInt</a>. We are working on an implementation of BigInt in SpiderMonkey, which is currently feature-complete but requires more optimization and cleanup. We wrote corresponding <a href="https://github.com/tc39/test262/">test262</a> conformance tests, which are mostly complete and upstreamed. Next semester, we intend to finish that work while our coding experience student <a href="https://github.com/caiolima">Caio Lima</a> continues work on a BigInt implementation on JSC, which has already started to land. Google also decided to implement that feature in V8 based on the specification we wrote. The BigInt specification that we wrote reached Stage 3 of TC39 standardization. We plan to keep working on these two BigInt implementations, making specification tweaks as needed, with an aim towards reaching Stage 4 at TC39 for the BigInt proposal in 2018.</p>

<p>Igalia is also proposing <a href="https://github.com/tc39/proposal-class-fields">class fields</a> and <a href="http://github.com/tc39/proposal-private-methods">private methods</a> for JavaScript. Similarly to BigInt, we were able to move them to Stage 3 and we are working to move them to stage 4. Our plan is to write test262 tests for private methods and work on an implementation in a JavaScript engine early next year.</p>

<p>Igalia implemented and shipped <a href="https://jakearchibald.com/2017/async-iterators-and-generators/">async iterators and generators</a> in Chrome 63, providing a convenient syntax for exposing and using asynchronous data streams, e.g., HTML streams. Additionally, we shipped a major performance optimization for Promises and async functions in V8.</p>

<p>We implemented and shipped two internationalization features in Chrome, <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/PluralRules">Intl.PluralRules</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat/formatToParts">Intl.NumberFormat.prototype.formatToParts</a>. To push the specifications of internationalization features forwards, we have been editing various other internationalization-related specifications such as <a href="https://github.com/tc39/proposal-intl-relative-time/">Intl.RelativeTimeFormat</a>, <a href="https://github.com/tc39/proposal-intl-locale/">Intl.Locale</a> and <a href="https://github.com/tc39/proposal-intl-list-format">Intl.ListFormat</a>; we also convened and led the first of what will be a monthly meeting of internationalization experts to propose and refine further API details.</p>

<p>Finally, Igalia has also been formalizing WebAssembly’s <a href="https://littledan.github.io/spec/document/js-api/">JavaScript API specification</a>, which reached the W3C first public working draft stage, and plans to go on to improve testing of that specification as the next step once further editorial issues are fixed.</p>

<h2 id="miscellaneous">Miscellaneous</h2>

<p>Thanks to sponsorship from <a href="http://mozilla.org/">Mozilla</a> we have continued our involvement in the <a href="https://wiki.mozilla.org/Platform/GFX/Quantum_Render">Quantum Render project</a> with the goal of using Servo’s WebRender in Firefox.</p>

<p>Support from <a href="https://www.metrological.com/index.html">Metrological</a> has also given us the opportunity to implement more web standards from some Linux ports of WebKit (<a href="https://webkitgtk.org/">GTK</a> and <a href="https://www.igalia.com/wpe/">WPE</a>, including:</p>
<ul>
  <li>WebRTC</li>
  <li>WebM</li>
  <li>WebVR</li>
  <li>Web Crypto</li>
  <li>Web Driver</li>
  <li>WebP animations support</li>
  <li>HTML interactive form validation</li>
  <li>MSE</li>
</ul>

<h2 id="conclusion">Conclusion</h2>

<p>Thanks for reading and we look forward to more work on the web platform in 2018. Onwards and upwards!</p>

{% endraw %}
