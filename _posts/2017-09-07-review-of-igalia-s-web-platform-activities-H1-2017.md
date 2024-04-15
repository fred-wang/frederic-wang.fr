---
layout: post
title: "Review of Igalia's Web Platform activities (H1 2017)"
tags: igalia mathml
---

{% raw %}

  <h2 id="introduction">Introduction</h2>

<p>For many years <a href="http://igalia.com/">Igalia</a> has been committed to and dedicated efforts to the improvement of Web Platform in all open-source Web Engines (Chromium, WebKit, Servo, Gecko) and JavaScript implementations (V8, SpiderMonkey, ChakraCore, JSC). We have been working in the implementation and standardization of some important technologies (CSS Grid/Flexbox, ECMAScript, WebRTC, WebVR, ARIA, MathML, etc). This blog post contains a review of these activities performed during the first half (and a bit more) of 2017.</p>

<h2 id="projects">Projects</h2>

<h3 id="css">CSS</h3>

<p>A few years ago <a href="http://www.bloomberg.com/company/">Bloomberg</a> and Igalia started a collaboration to implement a new layout model for the Web Platform. Bloomberg had complex layout requirements and what the Web provided was not enough and caused performance issues. <a href="https://drafts.csswg.org/css-grid/">CSS Grid Layout</a> seemed to be the right choice, a feature that would provide such complex designs with more flexibility than the currently available methods.</p>

<p><a href="https://blogs.igalia.com/mrego/2017/03/16/css-grid-layout-is-here-to-stay/">We’ve been implementing CSS Grid Layout in Blink and WebKit</a>, initially behind some flags as an experimental feature. This year, after some coordination effort to ensure interoperability (talking to the different parties involved like browser vendors, the CSS Working Group and the web authors community), it has been shipped by default in Chrome 58 and Safari 10.1. This is a huge step for the layout on the web, and modern websites will benefit from this new model and enjoy all the features provided by CSS Grid Layout spec.</p>

<p>Since the CSS Grid Layout shared the same alignment properties as the CSS Flexible Box feature, a new spec has been defined to generalize alignment for all the layout models. We started implementing this new spec as part of our work on Grid, <a href="https://blogs.igalia.com/jfernandez/2017/05/03/can-i-use-css-box-alignment/">being Grid the first layout model supporting it</a>.</p>

<p>Finally, we worked on other minor CSS features in Blink such as <a href="https://blogs.igalia.com/mrego/2017/01/09/coloring-the-insertion-caret/">caret-color</a> or <a href="https://blogs.igalia.com/mrego/2017/05/03/adding-focus-within-selector-to-chromium/">:focus-within</a> and also several interoperability issues related to Editing and Selection.</p>

<h3 id="mathml">MathML</h3>

<p><a href="https://www.w3.org/Math/">MathML</a> is a W3C recommendation to represent mathematical formulae that has been included in many other standards such as ISO/IEC, HTML5, ebook and office formats. There are many tools available to handle it, including various assistive technologies as well as generators from the popular LaTeX typesetting system.</p>

<p>After the improvements we performed in <a href="https://webkit.org/blog/6803/improvements-in-mathml-rendering/">WebKit’s MathML implementation</a>, we have regularly been in contact with Google to see how we can implement MathML in Chromium. 
Early this year, we had several meetings with Google’s layout team to discuss this in further details. We agreed that MathML is an important feature to consider for users and that the right approach would be to rely on the new <a href="https://docs.google.com/document/d/1uxbDh4uONFQOiGuiumlJBLGgO4KDWB8ZEkp7Rd47fw4/">LayoutNG</a> model currently being implemented. We created a prototype for a <a href="https://github.com/emilio/chromium/commits/mathml-ng">small LayoutNG-based MathML implementation</a> as a proof-of-concept and as a basis for future technical discussions. We are <a href="https://twitter.com/regocas/status/869871891628126209">going to follow-up on this after the end of Q3</a>, once Chromium’s layout team has made more progress on LayoutNG.</p>

<h3 id="servo">Servo</h3>

<p><a href="https://servo.org/">Servo</a> is Mozilla’s next-generation web content engine based on Rust, a language that guarantees memory safety. Servo relies on a Rust project called WebRender which replaces the typical rasterizer and compositor duo in the web browser stack. WebRender makes extensive use of GPU batching to achieve very exciting performance improvements in common web pages. Mozilla has decided to make WebRender part of the <a href="https://wiki.mozilla.org/Platform/GFX/Quantum_Render">Quantum Render</a> project.</p>

<p>We’ve had the opportunity to collaborate with Mozilla for a few years now, focusing on the graphics stack. Our work has focused on bringing full support for CSS stacking and clipping to WebRender, so that it will be available in both Servo and Gecko. This has involved creating a data structure similar to what WebKit calls the “scroll tree” in WebRender. The scroll tree divides the scene into independently scrolled elements, clipped elements, and various transformation spaces defined by CSS transforms. The tree allows WebRender to handle page interaction independently of page layout, allowing maximum performance and responsiveness.</p>

<h3 id="webrtc">WebRTC</h3>

<p><a href="https://webrtc.org/">WebRTC</a> is a collection of communications protocols and APIs that enable real-time communication over peer-to-peer connections. Typical use cases include video conferencing, file transfer, chat, or desktop sharing. Igalia has been working on the WebRTC implementation in WebKit and this development is currently sponsored by <a href="https://www.metrological.com/index.html">Metrological</a>.</p>

<p>This year we have continued the implementation effort in WebKit for the <a href="https://webkitgtk.org/">WebKitGTK</a> and <a href="https://www.igalia.com/wpe/">WebKit WPE</a> ports, as well as the maintenance of two test servers for WebRTC: Ericsson’s p2p and Google’s <a href="https://github.com/webrtc/apprtc">apprtc</a>. Finally, a lot of progress has been done to add support for <a href="https://jitsi.org/">Jitsi</a> using the existing OpenWebRTC backend.</p>

<p>Since OpenWebRTC development is not an active project anymore and given libwebrtc is gaining traction in both Blink and the WebRTC implementation of WebKit for Apple software, we are taking the first steps to replace the original WebRTC implementation in WebKitGTK based on OpenWebRTC, with a new one based on libwebrtc. Hopefully, this way we will share more code between platforms and get more robust support of WebRTC for the end users. GStreamer integration in this new implementation is an issue we will have to study, as it’s not built in libwebrtc. libwebrtc offers many services, but not every WebRTC implementation uses all of them. This seems to be the case for the Apple WebRTC implementation, and it may become our case too if we need tighter integration with GStreamer or hardware decoding.</p>

<h3 id="webvr">WebVR</h3>

<p><a href="https://w3c.github.io/webvr/">WebVR</a> is an API that provides support for virtual reality devices in Web engines. Implementation and devices are currently actively developed by browser vendors and it looks like it is going to be a huge thing. Igalia has started to investigate on that topic to see how we can join that effort. This year, we have been in discussions with Mozilla, Google and Apple to see how we could help in the implementation of WebVR on Linux. We decided to start experimenting an implementation within WebKitGTK. We <a href="https://lists.webkit.org/pipermail/webkit-dev/2017-August/029372.html">announced our intention on the webkit-dev mailing list</a> and got encouraging feedback from Apple and the WebKit community.</p>

<h3 id="aria">ARIA</h3>

<p><a href="https://www.w3.org/WAI/intro/aria">ARIA</a> defines a way to make Web content and Web applications more accessible to people with disabilities. Igalia strengthened its ongoing committment to the W3C: Joanmarie Diggs joined Richard Schwerdtfeger as a co-Chair of the W3C’s <a href="https://www.w3.org/WAI/ARIA/">ARIA working group</a>, and became editor of the <a href="https://w3c.github.io/aria/core-aam/core-aam.html">Core Accessibility API Mappings</a>, [Digital Publishing Accessibility API Mappings] (https://w3c.github.io/aria/dpub-aam/dpub-aam.html), and <a href="https://w3c.github.io/aria/accname-aam/accname-aam.html">Accessible Name and Description: Computation and API Mappings</a> specifications. Her main focus over the past six months has been to get <a href="https://w3c.github.io/aria/aria/aria.html">ARIA 1.1</a> transitioned to Proposed Recommendation through a combination of implementation and bugfixing in WebKit and Gecko, creation of automated testing tools to verify platform accessibility API exposure in GNU/Linux and macOS, and working with fellow Working Group members to ensure the platform mappings stated in the various “AAM” specs are complete and accurate. We will provide more information about these activities after ARIA 1.1 and the related AAM specs are further along on their respective REC tracks.</p>

<h3 id="web-platform-predictability-for-webkit">Web Platform Predictability for WebKit</h3>

<p><a href="https://www.ampproject.org/">The AMP Project</a> has recently sponsored Igalia to improve WebKit’s implementation of the Web platform. We have worked on many issues, the main ones being:</p>

<ul>
  <li>Frame sandboxing: Implementing sandbox values to allow trusted third-party resources to open unsandboxed popups or restrict unsafe operations of malicious ones.</li>
  <li>Frame scrolling on iOS: Addressing issues with scrollable nodes; trying to move to a more standard and interoperable approach with scrollable iframes.</li>
  <li>Root scroller: Finding a solution to the old interoperability issue about how to scroll the main frame; considering a new rootScroller API.</li>
</ul>

<p>This project aligns with <a href="https://www.chromium.org/blink/platform-predictability">Web Platform Predictability</a> which aims at making the Web more predictable for developers by improving interoperability, ensuring version compatibility and reducing footguns. It has been a good opportunity to collaborate with Google and Apple on improving the Web. You can find further details in <a href="https://frederic-wang.fr/amp-and-igalia-working-together-to-improve-the-web-platform.html">this blog post</a>.</p>

<h3 id="javascript">JavaScript</h3>

<p>Igalia has been involved in design, standardization and implementation of several JavaScript features in collaboration
with Bloomberg and Mozilla.</p>

<p>In implementation, Bloomberg has been sponsoring implementation of modern JavaScript features in V8, SpiderMonkey, JSC and ChakraCore, in collaboration with the open source community:</p>

<ul>
  <li>Implementation of many ES6 features in V8, such as <a href="https://wingolog.org/archives/2013/05/08/generators-in-v8">generators</a>, destructuring binding and arrow functions</li>
  <li><a href="https://blogs.igalia.com/compilers/2016/05/23/awaiting-the-future-of-javascript-in-v8/">Async/await</a> and <a href="https://jakearchibald.com/2017/async-iterators-and-generators/">async iterators and generators</a> in V8 and some work in JSC</li>
  <li>Optimizing SpiderMonkey generators</li>
  <li>Ongoing implementation of <a href="https://github.com/tc39/proposal-bigint">BigInt</a> in SpiderMonkey and class field declarations in JSC</li>
</ul>

<p>On the design/standardization side, Igalia is active in TC39 and with Bloomberg’s support</p>

<ul>
  <li>Arbitrary precision integers (BigInt)</li>
  <li><a href="https://github.com/tc39/proposal-class-fields">Class field declarations</a>, <a href="http://github.com/tc39/proposal-private-methods">private methods</a> and decorators</li>
  <li>New RegExp features such as <a href="https://github.com/tc39/proposal-regexp-named-groups/">named capture groups</a></li>
</ul>

<p>In partnership with Mozilla, Igalia has been involved in the specification of various JavaScript standard library features for internationalization, in specification, implementation in V8, code reviews in other JavaScript engines,
as well as working with the underlying ICU library.</p>

<h2 id="other-activities">Other activities</h2>

<h3 id="preparation-of-web-engines-hackfest-2017">Preparation of Web Engines Hackfest 2017</h3>

<p>Igalia has been organizing and hosting the <a href="https://webengineshackfest.org/">Web Engines Hackfest</a> since 2009. This event under an unconference format has been a great opportunity for Web Engines developers to meet, discuss and work together on the web platform and on web engines in general. We announced <a href="https://blogs.igalia.com/mrego/2017/04/05/announcing-a-new-edition-of-the-web-engines-hackfest/">the 2017 edition</a> and <a href="https://webengineshackfest.org/#attendees">many developers already confirmed their attendance</a>. We would like to thank <a href="https://webengineshackfest.org/#sponsors">our sponsors</a> for supporting this event and we are looking forward to seeing you in October!</p>

<h3 id="coding-experience">Coding Experience</h3>

<p><a href="http://emiliocobos.me/about/">Emilio Cobos</a> has completed his <a href="https://www.igalia.com/about-us/coding-experience">coding experience program</a> on implementation of web standards. He has been working in the implementation of “display: contents” in <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=657748">Blink</a> but some work is pending due to unresolved CSS WG issues. He also started the corresponding work in WebKit but implementation is still very partial. It has been a pleasure to mentor a skilled hacker like Emilio and we wish him the best for his future projects!</p>

<h3 id="new-igalians">New Igalians</h3>

<p>During this semester we have been glad to welcome new igalians who will help us to pursue Web platform developments:</p>

<ul>
  <li><a href="https://www.igalia.com/nc/igalia-247/igalian/item/dehrenberg/">Daniel Ehrenberg</a> joined Igalia in January. He is an active contributor to the V8 JavaScript engine and has been representing Igalia at the ECMAScript TC39 meetings.</li>
  <li><a href="https://www.igalia.com/nc/igalia-247/igalian/item/aboya/">Alicia Boya</a> joined Igalia in March. She has experience in many areas of computing, including web development, computer graphics, networks, security, and software design with performance which we believe will be valuable for our Web platform activities.</li>
  <li><a href="https://www.igalia.com/nc/igalia-247/igalian/item/ms2ger/">Ms2ger</a> joined Igalia in July. He is a well-known hacker of the Mozilla community and has wide experience in both Gecko and Servo. He has noticeably worked in DOM implementation and web platform test automation.</li>
</ul>

<h1 id="conclusion">Conclusion</h1>

<p>Igalia has been involved in a wide range of Web Platform technologies going from Javascript and layout engines to accessibility or multimedia features. Efforts have been made in all parts of the process:</p>

<ul>
  <li>Participation to standardization bodies (<a href="https://www.w3.org/Consortium/Member/Testimonial/#t1506">W3C</a>, <a href="https://www.ecma-international.org/memento/TC39.htm">TC39</a>).</li>
  <li>Elaboration of conformance tests (<a href="https://github.com/w3c/web-platform-tests">web-platform-tests</a> <a href="https://github.com/tc39/test262">test262</a>).</li>
  <li>Implementation and bug fixes in all open source web engines.</li>
  <li>Discussion with users, browser vendors and other companies.</li>
</ul>

<p>Although, some of this work has been sponsored by Google or Mozilla, it is important to highlight how external companies (other than browser vendors) can make good contributions to the Web Platform, playing an important role on its evolution. <a href="https://twitter.com/alanstearns">Alan Stearns</a> already pointed out the <a href="https://www.youtube.com/watch?v=4ggNcqdwT-Y">responsibility of the Web Plaform users on the evolution of CSS</a> while <a href="https://rachelandrew.co.uk/">Rachel Andrew</a> emphasized <a href="https://rachelandrew.co.uk/speaking/event/cssconfeu-2017">how any company or web author can effectively contribute to the W3C in many ways</a>.</p>

<p>As mentioned in this blog post, <a href="http://www.bloomberg.com/company/">Bloomberg</a> is an important contributor of <a href="https://www.techatbloomberg.com/blog/bloombergs-2016-open-source-contributions-5-top-projects/">several open source projects</a> and they’ve been a key player in the development of CSS Grid Layout or Javascript. Similarly, <a href="https://www.metrological.com/index.html">Metrological</a>’s support has been instrumental for the implementation of WebRTC in WebKit. We believe others could follow their examples and we are looking forward to seeing more companies sponsoring Web Platform developments!</p>

{% endraw %}
