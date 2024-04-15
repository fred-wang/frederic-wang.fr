---
layout: post
title: "Review of Igalia's Web Platform activities (H2 2018)"
tags: igalia mathml
---

{% raw %}

  <p>This blog post reviews Igalia’s activity around the
<a href="https://en.wikipedia.org/wiki/Web_platform">Web Platform</a>, focusing on
the second semester of 2018.</p>

<h2 id="projects">Projects</h2>

<h3 id="mathml">MathML</h3>

<p>During 2018 we have continued discussions to implement MathML in Chromium with Google and people interested in math layout. The project was finally <a href="https://mathml.igalia.com/news/2019/02/12/launch-of-the-project/#new">launched early this year</a> and we have encouraging progress. Stay tuned for more details!</p>

<h3 id="javascript">Javascript</h3>

<p>As mentioned in the previous report, Igalia has proposed and developed the specification for <a href="https://github.com/tc39/proposal-bigint/">BigInt</a>, enabling math on arbitrary-sized integers in JavaScript. We’ve continued to land patches for
 <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1366287">BigInt support in SpiderMonkey</a> and <a href="https://bugs.webkit.org/show_bug.cgi?id=179001">JSC</a>. For the
latter, you can watch this
<a href="https://vimeo.com/304865023">video demonstrating the current support</a>. Currently, these
two support are under a preference flag but we hope to make it enable by default
after we are done polishing the implementations. We also added support for BigInt to several Node.js APIs (e.g. <a href="https://github.com/nodejs/node/pull/20220"><code class="language-plaintext highlighter-rouge">fs.Stat</code></a> or <a href="https://github.com/nodejs/node/pull/21256"><code class="language-plaintext highlighter-rouge">process.hrtime.bigint</code></a>).</p>

<p>Regarding “object-oriented” features, we submitted patches
<a href="https://bugs.webkit.org/show_bug.cgi?id=174212">private and public instance fields support to JSC</a>
and they are pending review. At the same time, we are working on
<a href="https://chromium-review.googlesource.com/c/v8/v8/+/1301018">private methods for V8</a></p>

<p>We contributed other nice features to V8 such as a spec change for template
strings and iterator protocol, support for
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries">Object.fromEntries</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/description">Symbol.prototype.description</a>, miscellaneous optimizations.</p>

<p>At TC39, we maintained or developed many proposals (BigInt, class fields,
private methods, decorators, …) and led the ECMAScript Internationalization
effort. Additionally, at the WebAssembly Working Group we edited the WebAssembly
JS and Web API and early version of WebAssembly/ES Module integration specifications.</p>

<p>Last but not least, we contributed various conformance tests to test262
and Web Platform Tests to ensure interoperability between the various features
mentioned above (BigInt, Class fields, Private methods…). In Node.js, we worked on <a href="https://github.com/nodejs/node/pull/24035">the new Web Platform Tests driver with update automation</a> and continued porting and fixing more Web Platform Tests in Node.js core.</p>

<p>We also worked on <a href="https://github.com/nodejs/node/pull/24035">the new Web Platform Tests driver with update automation</a>, and continued porting and fixing more Web Platform Tests in Node.js core. Outside of core, we implemented <a href="https://github.com/nodejs/llnode/pull/206">the initial JavaScript API for llnode</a>, a Node.js/V8 plugin for the LLDB debugger.</p>

<h3 id="accessibility">Accessibility</h3>

<p>Igalia has continued its involvement at the W3C. We have achieved the following:</p>

<ul>
  <li><a href="https://www.w3.org/2018/11/aria-charter.html">The ARIA Working Group Charter</a> has been renewed</li>
  <li><a href="https://www.w3.org/TR/accname-1.1/">AccName 1.1</a>, <a href="https://www.w3.org/TR/graphics-aria-1.0/">Graphics ARIA 1.0</a> and <a href="https://www.w3.org/TR/graphics-aam-1.0/">Graphics AAM 1.0</a> became recommendations.</li>
  <li>A new version of the 1.2 suite (ARIA, Core-AAM, AccName and the Authoring Practices) is available. In particular, we published a first working draft for <a href="https://www.w3.org/TR/wai-aria-1.2/">ARIA 1.2</a> which will focus on role parity with HTML 5 elements. A working draft for <a href="https://w3c.github.io/core-aam/">Core-AAM 1.2</a> is also available.</li>
</ul>

<p>We are also collaborating with Google to implement ATK support in Chromium. This work will make it possible for users of the Orca screen reader to use Chrome/Chromium as their browser. During H2 we began implementing the foundational accessibility support. During H1 2019 we will continue this work. It is our hope that sufficient progress will be made during H2 2019 for users to begin using Chrome with Orca.</p>

<h3 id="web-platform-predictability">Web Platform Predictability</h3>

<p>On Web Platform Predictability, we’ve continued our collaboration with AMP to do bug fixes and implement new features in WebKit. You can read a review of the work done in 2018 on the <a href="https://amphtml.wordpress.com/2018/12/06/contributing-to-webkit-for-a-more-predictable-web-platform/">AMP blog post</a>.</p>

<p>We have worked on a lot of interoperability issues related to editing and selection thanks to financial support from Bloomberg. For example when <a href="https://github.com/w3c/editing/issues/163">deleting the last cell of a table</a> some browsers keep an empty table while others delete the whole table. The latter can be problematic, for example if users press backspace continuously to delete a long line, they can accidentally end up deleting the whole table. This was <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=731320">fixed in Chromium</a> and <a href="https://bugs.webkit.org/show_bug.cgi?id=173117">WebKit</a>.</p>

<p>Another issue is that style is lost when transforming some text into list items. When running <a href="https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand">execCommand()</a> with insertOrderedList/insertUnorderedList on some styled paragraph, the new list item loses the original text’s style. This behavior is not interoperable and <a href="https://github.com/w3c/editing/issues/179">we have proposed a fix</a>  so that Firefox, Edge, Safari and Chrome behave the same for this operation. We <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=149901">landed a patch for Chromium</a>. After discussion with Apple, it was decided not to implement this change in Safari as it would break some iOS rich text editor apps, mismatching the required platform behavior.</p>

<p>We have also been working on CSS Grid interoperability. We imported Web Platform Tests into WebKit (cf bugs <a href="https://bugs.webkit.org/show_bug.cgi?id=191515">191515</a> and <a href="https://bugs.webkit.org/show_bug.cgi?id=191369">191369</a> and at the same time completing the missing features and bug fixes so that browsers using WebKit are interoperable, passing 100% of the Grid test suite. For details, see <a href="https://bugs.webkit.org/show_bug.cgi?id=191358">191358</a>,
<a href="https://bugs.webkit.org/show_bug.cgi?id=189582">189582</a>, <a href="https://bugs.webkit.org/show_bug.cgi?id=189698">189698</a>, <a href="https://bugs.webkit.org/show_bug.cgi?id=191881">191881</a>, <a href="https://bugs.webkit.org/show_bug.cgi?id=191938">191938</a>, <a href="https://bugs.webkit.org/show_bug.cgi?id=170175">170175</a>, <a href="https://bugs.webkit.org/show_bug.cgi?id=191473">191473</a> and <a href="https://bugs.webkit.org/show_bug.cgi?id=191963">191963</a>. Last but not least, we are exporting more than 100 internal browser tests to the Web Platform test suite.</p>

<h3 id="css">CSS</h3>

<p>Bloomberg is supporting our work to develop new CSS features. One of the new exciting features we’ve been working on is CSS Containment. The goal is to improve the rendering performance of web pages by isolating a subtree from the rest of the document. You can read <a href="https://blogs.igalia.com/mrego/2019/01/11/an-introduction-to-css-containment/#wrap-up">details on Manuel Rego’s blog post</a>.</p>

<p>Regarding <a href="https://www.w3.org/TR/css-grid-2/">CSS Grid Layout</a> we’ve continued our maintenance duties, bug triage of the Chromium and WebKit bug trackers, and fixed the most severe bugs. One change with impact on end users was related to <a href="https://blogs.igalia.com/mrego/2018/08/10/changes-on-css-grid-layout-in-percentages-and-indefinite-height/">how percentages row tracks and gaps work in grid containers with indefinite size</a>, the last spec resolution was implemented in both Chromium and WebKit. We are finishing the level 1 of the specification with some missing/incomplete features. First we’ve been working on the new Baseline Alignment algorithm (cf. CSS WG issues <a href="https://github.com/w3c/csswg-drafts/issues/1039">1039</a>, <a href="https://github.com/w3c/csswg-drafts/issues/1365">1365</a> and <a href="https://github.com/w3c/csswg-drafts/issues/1409">1409</a>). We fixed related issues in <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=704713">Chromium</a> and <a href="https://bugs.webkit.org/show_bug.cgi?id=145566">WebKit</a>. Similarly, we’ve worked on Content Alignment logic (see CSS WG issue <a href="https://github.com/w3c/csswg-drafts/issues/2557">2557</a>) and resolved <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=844744">a bug in Chromium</a>. The new algorithm for baseline alignment caused an important performance regression for certain resizing use cases so we’ve fixed them with some performance optimization and <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=873452">that landed in Chromium</a>.</p>

<p>We have also worked on various topics related to <a href="https://www.w3.org/TR/css-text-3/">CSS Text 3</a>. We’ve fixed several bugs to increase the pass rate for the Web Platform test suite in Chromium such as bugs <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=854624">854624</a>, <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=900727">900727</a> and <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=768363">768363</a>. We are also working on a <a href="https://drafts.csswg.org/css-text-3/#white-space-property">new CSS value ‘break-spaces’ for the ‘white-space’ property</a>. For details, see the CSS WG discussions: <a href="https://github.com/w3c/csswg-drafts/issues/2465">issue 2465</a> and <a href="https://github.com/w3c/csswg-drafts/pull/2841">pull request</a>. We <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=767634">implemented this new property in Chromium</a> under a CSSText3BreakSpaces flag. Additionally, we are currently <a href="https://chromium-review.googlesource.com/c/chromium/src/+/1363971">porting this implementation to Chromium’s new layout engine ‘LayoutNG’</a>. We have plans to <a href="https://bugs.webkit.org/show_bug.cgi?id=177327">implement this feature</a> in WebKit during the second semester.</p>

<h3 id="multimedia">Multimedia</h3>

<ul>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API">WebRTC</a>: The libwebrtc branch is now upstreamed in WebKit and has been tested with popular servers.</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Media_Source_Extensions_API">Media Source Extensions</a>: WebM MSE support is upstreamed in WebKit.</li>
  <li>We implemented basic support for <code class="language-plaintext highlighter-rouge">&lt;video&gt;</code> and <code class="language-plaintext highlighter-rouge">&lt;audio&gt;</code> elements in Servo.</li>
</ul>

<h2 id="other-activities">Other activities</h2>

<h3 id="web-engines-hackfest-2018">Web Engines Hackfest 2018</h3>

<p>Last October, we organized the
<a href="https://webengineshackfest.org/2018/">Web Engines Hackfest</a> at our A Coruña
office. It was a great event with about 70 attendees from all the web engines,
thank you to all the participants! As usual, you can find more information on
the <a href="https://github.com/Igalia/webengineshackfest/wiki/2018">event wiki</a> including
link to slides and videos of speakers.</p>

<h3 id="tpac-2018">TPAC 2018</h3>

<p>Again in October, but this time in Lyon (France), 12 people from Igalia attended TPAC and participated in several discussions on the different meetings. Igalia had a booth there showcasing several demos of our last developments running on top of WPE (a WebKit port for embedded devices). Last, <a href="https://blogs.igalia.com/mrego/2019/02/11/summary-of-a-week-in-lyon-for-tpac-2018/">Manuel Rego gave a talk on the W3C Developers Meetup about how to contribute to CSS</a>.</p>

<h3 id="thisjavascript-state-of-browsers">This.Javascript: State of Browsers</h3>

<p>In December, we also participated with other browser developers to the online <a href="https://www.youtube.com/watch?v=lD5IhYNIKvk">This.Javascript: State of Browsers</a> event organized by <a href="https://www.thisdot.co/">ThisDot</a>. We talked more specifically about the current work in WebKit.</p>

<h3 id="new-igalians">New Igalians</h3>

<p>We are excited to announce that new Igalians are joining us to continue our Web platform effort:</p>

<ul>
  <li>
    <p><a href="https://www.igalia.com/igalia-247/igalian/item/cchen">Cathie Chen</a>, a Chinese engineer with about 10 years of experience working on browsers. Among other contributions to Chromium, she worked on the new LayoutNG code and added support for list markers.</p>
  </li>
  <li>
    <p><a href="https://www.igalia.com/igalia-247/igalian/item/clima/">Caio Lima</a> a Brazilian developer who recently graduated from the Federal University of Bahia. He participated to our coding experience program and notably worked on BigInt support in JSC.</p>
  </li>
  <li>
    <p><a href="https://www.igalia.com/igalia-247/igalian/item/obrufau/">Oriol Brufau</a> a recent graduate in math from Barcelona who is also involved in the CSSWG and the development of various browser engines. He participated to our coding experience program and implemented the CSS Logical Properties and Values in WebKit and Chromium.</p>
  </li>
</ul>

<h3 id="coding-experience-programs">Coding Experience Programs</h3>

<p>Last fall, <a href="https://sauleau.com/">Sven Sauleau</a> joined our coding experience program and started to work on various BigInt/WebAssembly improvements in V8.</p>

<h2 id="conclusion">Conclusion</h2>

<p>We are thrilled with the web platform achievements we made last semester and we look forward to more work on the web platform in 2019!</p>


{% endraw %}
