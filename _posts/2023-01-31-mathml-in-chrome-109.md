---
layout: post
title: "MathML in Chrome 109"
tags: mathml chromium igalia
---

{% raw %}

  <p><em>2023/06/15: Most of this article was written in January 2023, but I only finished and published it in June. Hopefully, information is still up-to-date 😃</em></p>

<h2 id="tldr">TL;DR</h2>

<p>Igalia announced early this year that <a href="https://www.igalia.com/2023/01/10/Igalia-Brings-MathML-Back-to-Chromium.html">MathML is back to Chromium</a>. This is an excellent news, for those like me who read and write mathematics on the web. Native support for such a universal human language sounds uncontroversial but it has taken a quarter century to get MathML implemented in all web engines… I invite you to listen to the <a href="https://www.igalia.com/chats/mathml-release">corresponding episode of Igalia Chats</a> where you can find some rationale about why it took so long. In this blog post, I’ll try to elaborate a bit about technical challenges we were able to overcome, thanks to the introduction of <a href="https://w3c.github.io/mathml-core/">MathML Core</a>. To be honest, things are still not perfect, but at least we can now rely on a clean foundation and continue to iterate improvements and fix bugs!</p>

<h2 id="timeline">Timeline</h2>

<p>As a reference, I’m providing below a list of important events (based on <a href="https://people.igalia.com/fwang/mathml-in-browsers-web-engines-hackfest-2019/slides/history/index.html">this timeline</a> and <a href="https://people.igalia.com/fwang/2022-06-igalia-week-shipping-mathml-in-chromium/#/7">this slide</a>) for native MathML support in browsers:</p>

<ul>
  <li>1993-1995: Early HTML specifications contained a <code class="language-plaintext highlighter-rouge">&lt;MATH&gt;</code> tag, which was experimented in <a href="https://en.wikipedia.org/wiki/Dave_Raggett">Dave Raggett</a>’s <a href="https://en.wikipedia.org/wiki/Arena_(web_browser)">Arena browser</a>.</li>
  <li>1998-2003: Initial specifications of MathML were published. Volunteer contributor <a href="https://math.ua.edu/people/roger-b-sidje/">Roger Sidje</a> added support in <a href="https://en.wikipedia.org/wiki/Gecko_(software)">Gecko</a> for XHTML documents and that was released in Mozilla 1.0.</li>
  <li>2006-2013:
    <ul>
      <li>MathML was integrated in HTML5. <a href="https://chavchanidze.com/">George Chavchanidze</a> created a <a href="https://www.w3.org/TR/mathml-for-css/">CSS-based implementation</a> and shipped it in Opera. Support was implemented in all Open Source browsers thanks to the effort of volunteer contributors (including Roger Sidje, François Sausset, <a href="https://twitter.com/alexmilowski">Alex Miłowski</a>, <a href="https://mathscribe.com/about-us.html">Dave Barton</a> and myself). However, <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=152430#c32">MathML was removed from Chrome</a> shortly after.</li>
      <li>Apple engineers, notably Chris Fleizach and <a href="https://www.linkedin.com/in/jamescraig">James Craig</a>, implemented <a href="https://developer.apple.com/documentation/appkit/nsaccessibility">NSAccessibility</a> support for <a href="https://en.wikipedia.org/wiki/WebKit">WebKit</a> and <a href="https://en.wikipedia.org/wiki/VoiceOver">VoiceOver</a>.</li>
    </ul>
  </li>
  <li>2014-2016:
    <ul>
      <li>I published an <a href="https://mathml.igalia.com/MathMLinHTML5/">implementation note</a> with extra rendering rules based on <a href="https://en.wikipedia.org/wiki/Donald_Knuth">Donald Knuth</a>’s T<sub>E</sub>XBook and Microsoft’s <a href="https://learn.microsoft.com/en-us/typography/opentype/spec/math">OpenType MATH table</a>. I implemented these rules in Gecko and WebKit via a <a href="https://www.ulule.com/mathematics-ebooks/">crowdfunding project</a>.</li>
      <li>During a few codecamps and hackfests, <a href="https://www.igalia.com/team/jdiggs">Joanmarie Diggs</a> (Igalia), <a href="https://www.igalia.com/team/asurkov">Alexander Surkov</a> (at that time at Mozilla) and I (who just joined the <a href="https://www.researchgate.net/publication/262240672_AcceSciTech_A_Global_Approach_to_Make_Scientific_and_Technical_Literature_Accessible">AcceSciTech project</a>) worked on <a href="https://en.wikipedia.org/wiki/Accessibility_Toolkit">ATK</a> and NSAccessibility support for Gecko, WebKit and <a href="https://help.gnome.org/users/orca/">Orca</a>.</li>
      <li><a href="https://twitter.com/jcsteh">Jamie Teh</a> and <a href="https://www.linkedin.com/in/neil-soiffer-1807b76">Neil Soiffer</a> added MathML accessibility support for Gecko and Chromium by exposing the raw source code via a dedicated <a href="https://en.wikipedia.org/wiki/Microsoft_Active_Accessibility">MSAA</a> API.</li>
      <li>Igalia performed a <a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring">big refactoring of WebKit’s implementation</a>. Initially done by <a href="https://www.igalia.com/team/alex">Alejandro García</a> in 2015, I took over the work when I joined the company the following year.</li>
    </ul>
  </li>
  <li>2019-2023:
    <ul>
      <li>Igalia launched the <a href="https://mathml.igalia.com/">“MathML in Chromium” project</a> with the support of various sponsors. <a href="https://www.igalia.com/team/rbuis">Rob Buis</a> and I worked on a brand new implementation in Chromium. <a href="https://www.igalia.com/team/bkardell">Brian Kardell</a> also joined Igalia at the beginning of the project and has been instrumental in communication, advocacy and standardization efforts.</li>
      <li>A new <a href="https://w3c.github.io/mathml-core/">MathML Core</a> specification became the reference for browser implementations and was shipped in Chromium 109.</li>
      <li>Alexander Surkov joined Igalia and helped with the <a href="https://w3c.github.io/mathml-aam/">MathML AAM</a> specification, which we used to implement ATK and NSAccessibility support in Chromium.</li>
      <li>I’ve regularly presented our results in conferences. For completeness, here are the talks I gave:
        <ul>
          <li>November 2022: <a href="https://people.igalia.com/fwang/blink-on-17/">Shipping MathML in Chrome 109</a> at BlinkOn 17 - <a href="https://www.youtube.com/watch?v=s3i02Yh3F9s">video</a>.</li>
          <li>June 2022: <a href="https://people.igalia.com/fwang/2022-06-igalia-week-shipping-mathml-in-chromium">Shipping MathML in Chrome</a> at the Web Engines Hackfest.</li>
          <li>May 2022: <a href="https://people.igalia.com/fwang/blink-on-16/">Remainder estimate for MathML integration</a> - <a href="https://www.youtube.com/watch?v=n9lX5RLWwGs">video</a>.</li>
          <li>November 2021: <a href="https://people.igalia.com/fwang/blink-on-15/">MathML, onde estamos?</a> - <a href="https://www.youtube.com/watch?v=H-7kG2lEKQ8">video</a>.</li>
          <li>November 2019: <a href="https://people.igalia.com/fwang/blink-on-11/slides">MathML Core</a> at BlinkOn 11.</li>
          <li>October 2019: <a href="https://people.igalia.com/fwang/mathml-in-browsers-web-engines-hackfest-2019/slides">MathML in Browsers</a> at the Web Engines Hackfest - <a href="https://youtu.be/Q8Z1D2i61j8?list=PL4sEzdAGvRgDCN6qACHWs04mQQTWBkdGq">video</a>.</li>
          <li>April 2019: <a href="https://people.igalia.com/fwang/blink-on-10/slides">MathML in LayoutNG</a> at BlinkOn 10.</li>
        </ul>
      </li>
    </ul>
  </li>
</ul>

<h2 id="a-simple-fraction">A simple fraction</h2>

<p>One of the first thing you can notice is that a significant portion of the work was done by volunteer contributors at the time when the set of requirements to ship a feature or integrate it in the specification was very small. Let’s consider some basic MathML formula to illustrate that:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&lt;math style="font: 32pt STIX Two Math;"&gt;
  &lt;mfrac&gt;
    &lt;mspace width="2em" height="1em" depth=".5em" style="background: red"/&gt;
    &lt;mspace width="2em" height=".5em" depth="1em" style="background: blue"/&gt;
  &lt;/mfrac&gt;
&lt;/math&gt;
</code></pre></div></div>

<p>The <code class="language-plaintext highlighter-rouge">&lt;math&gt;</code> element is the root container for a new MathML formula. The <code class="language-plaintext highlighter-rouge">&lt;mfrac&gt;</code> element describes a fraction with two <code class="language-plaintext highlighter-rouge">&lt;mspace/&gt;</code> children corresponding respectively to its numerator and denominator. These <code class="language-plaintext highlighter-rouge">&lt;mspace/&gt;</code> elements are boxes of specified width, ascent and descent, as described by their width, height and depth attributes (using <a href="https://tex.stackexchange.com/questions/40977/confused-with-tex-terminology-height-depth-width">T<sub>E</sub>X terminology</a>). Finally, the <code class="language-plaintext highlighter-rouge">style</code> attribute attaches inline style to MathML elements.</p>

<p>MathML 3 describes <a href="https://www.w3.org/TR/MathML3/chapter3.html#presm.mspace">how to interpret the attributes</a> of the <code class="language-plaintext highlighter-rouge">&lt;mspace&gt;</code> element. In general, it does not really define interaction with other web technologies and the behavior of the <a href="https://www.w3.org/TR/MathML3/chapter2.html#fund.globatt">style attribute “is not specified”</a>. However, browser implementers can safely assume it has the same syntax and semantic as HTML and that’s basically <a href="https://w3c.github.io/mathml-core/#attributes-common-to-html-and-mathml-elements">what MathML Core says</a>. So we know the <code class="language-plaintext highlighter-rouge">&lt;math&gt;</code> element uses the font family <code class="language-plaintext highlighter-rouge">STIX Two Math</code> and font size of 32pt, while the <code class="language-plaintext highlighter-rouge">&lt;mspace&gt;</code> elements have red and blue background.</p>

<p>But how should we layout the <code class="language-plaintext highlighter-rouge">&lt;mfrac&gt;</code> element?</p>

<h2 id="tex-based-layout">T<sub>E</sub>X-based layout</h2>

<p><a href="https://www.w3.org/TR/MathML3/chapter3.html#presm.mfrac">MathML 3 does not really say much more</a> than the semantic “used for fractions” and the syntax <code class="language-plaintext highlighter-rouge">&lt;mfrac&gt; numerator denominator &lt;/mfrac&gt;</code>. For the fraction bar, “the exact thickness of these is left up to the rendering agent”. MathML Core has a <a href="https://w3c.github.io/mathml-core/#dfn-mfrac">more detailed description</a> involving vertical position and thickness of the fraction bar, minimal gaps between numerator/denominator and fraction bar as well as minimal shifts of the numerator/denominator’s baseline with respect to the baseline, horizontal centering of the numerator/denominator and more.</p>

<p>One of the essential part is that many of these parameters are taken from STIX Two Math’s <a href="https://learn.microsoft.com/en-us/typography/opentype/spec/math">Open Type MATH table</a> such as <code class="language-plaintext highlighter-rouge">fractionNumeratorShiftUp</code>, <code class="language-plaintext highlighter-rouge">fractionDenominatorGapMin</code> etc and are generalizing the rules from the T<sub>E</sub>XBook. You may notice parameters like <code class="language-plaintext highlighter-rouge">fractionNumeratorDisplayStyleShiftUp</code>, <code class="language-plaintext highlighter-rouge">fractionDenomDisplayStyleGapMin</code> etc which are variants based on the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/math-style">math-style</a> we will explain below.</p>

<p>In any case, as long as they follow the layout algorithm described in MathML Core, all browsers should now render the fraction example the same, right?</p>

<h2 id="exposing-mathml-magic">Exposing MathML magic</h2>

<p>Assuming STIX Two Math is available or provided as a web font, Chrome and Firefox renders the previous example that way:</p>

<p><img style="margin-left: auto; margin-right: auto; " width="75" height="129" src="https://frederic-wang.fr/images/2023-mathml-core-mfrac-example.png" alt="Screenshot of the example in Chromium 109" /></p>

<p>You can notice that the size of the numerator/denominator is different from what you get in Safari. Indeed, the web inspector shows that the <code class="language-plaintext highlighter-rouge">&lt;mspace&gt;</code> elements has a smaller <code class="language-plaintext highlighter-rouge">font-size</code> than the one of the <code class="language-plaintext highlighter-rouge">&lt;math&gt;</code> or <code class="language-plaintext highlighter-rouge">&lt;mfrac&gt;</code> elements. This magic is suggested by the remaining part of the <a href="https://www.w3.org/TR/MathML3/chapter3.html#presm.mfrac">description of MathML 3</a> we have ignored so far:</p>

<blockquote>
  <p>The mfrac element sets displaystyle to “false”, or if it was already false increments scriptlevel by 1, within numerator and denominator.</p>
</blockquote>

<p>Let’s try to explain this a bit more. The <code class="language-plaintext highlighter-rouge">displaystyle</code> and <code class="language-plaintext highlighter-rouge">scriptlevel</code> properties are concepts from MathML 3 which are themselves generalizing T<sub>E</sub>X. Imagine many nested superscripts: the font size is scaled down each time you enter a superscript, and becomes smaller and smaller. Here, the <code class="language-plaintext highlighter-rouge">scriptlevel</code> corresponds to the nesting level and it affects the font size. Regarding  <code class="language-plaintext highlighter-rouge">displaystyle=false</code>, this is typically used when you want to render the formula with more compact height e.g. for formulas rendered inline within a paragraph of text.</p>

<p>So the MathML 3 spec essentially says that the subformulas numerator/denominator should be rendered with compact height, and if we are already in such a mode we should even scale down the font size within these subformulas. The only problem is that this behavior is not specified at all by CSS!</p>

<p>In order to solve that, we introduced the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/math-style">math-style</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/math-depth">math-depth</a> CSS properties, explaining how they affect <code class="language-plaintext highlighter-rouge">font-size</code> in the cascade. That way the behavior can be completely handled by the CSS engines. Then <a href="https://w3c.github.io/mathml-core/#the-displaystyle-and-scriptlevel-attributes">MathML Core</a> describes how <code class="language-plaintext highlighter-rouge">displaystyle</code>/<code class="language-plaintext highlighter-rouge">scriptlevel</code> attributes are treated as presentational hints together with appropriate rules in the <a href="https://w3c.github.io/mathml-core/#user-agent-stylesheet">User Agent stylesheet</a>. At the end everything is well-specified and Safari’s behavior is <a href="https://bugs.webkit.org/show_bug.cgi?id=202303">a bug</a>.</p>

<h2 id="integration-with-the-web-platform">Integration with the web platform</h2>

<p>The previous paragraphs described how we integrated T<sub>E</sub>X-based math layout inside the web platform. MathML 3 already started that by defined a SGML tree and HTML5 / MathML Core went further by defining the parsing rules, a <a href="https://w3c.github.io/mathml-core/#dom-and-javascript">WebIDL</a> or <a href="https://w3c.github.io/mathml-core/#html-and-svg">integration with HTML and SVG</a>.</p>

<p>The integration problem can also be seen on the other side: how do we interpret CSS features for math layout? For example what happens if one specifies a CSS <code class="language-plaintext highlighter-rouge">width</code> on the <code class="language-plaintext highlighter-rouge">&lt;mfrac&gt;</code> element? Or a <code class="language-plaintext highlighter-rouge">padding</code>? What would be the CSS layout if there are less or more children than just the numerator/denominator? What happen if <code class="language-plaintext highlighter-rouge">float: left</code> or <code class="language-plaintext highlighter-rouge">position: absolute</code> are specified on a child? Probably math authors don’t care too much but that’s still something that needs to be defined in the spec and implemented in a cross-compatible way.</p>

<p>Answering these questions were also useful for many reasons. Just to list a few examples off the top of my head:</p>
<ul>
  <li>In order to make things manageable, MathML Core focuses on a susbet of MathML 3 and some people are interested in writing polyfills for legacy or future features, which is something that can often be done by CSS.</li>
  <li>Using a terminology that takes into account direction/writing-mode facilitates the implementation of right-to-left math and could allow vertical math in the future.</li>
  <li>To avoid visual confusion between the fraction bar and another adjacent items (e.g. minus sign or another fraction’s bar), a default 1-pixel space is added around the element. This can be easily done by setting the padding in the <a href="https://w3c.github.io/mathml-core/#user-agent-stylesheet">User Agent stylesheet</a>… as long as it’s supported!</li>
  <li>Bypassing MathML layout in invalid subtrees (e.g. <code class="language-plaintext highlighter-rouge">&lt;mfrac&gt;</code> with three children) as was done in old implementations are making things harder for fuzzers and testcase reducers. Additionally these fuzzers often find issues happening with exotic CSS features, so better if the spec says how to handle them.</li>
</ul>

<h2 id="web-platform-tests">Web Platform tests</h2>

<p>We’ve seen some examples on how to improve the MathML specification. This leads to the topic of <a href="https://web-platform-tests.org/">Web Platform tests</a>, which are very important to verify conformance with that specification and ensure browser interoperability. That’s a good tool and motivation for implementers and they may also prevent regressions since they are run regularly, at least each time a change is made in the browser repository.</p>

<p>However, MathML 3 was using <a href="https://www.w3.org/Math/testsuite/build/main/overview.html">manual tests</a> where one has to visually compare the rendering of the 1675 testcases in a browser against a sample rendering and decide whether it passes or not. That’s a quite tedious and not very robust way of testing!</p>

<p>Fortunately, this has changed with MathML Core with <a href="https://wpt.fyi/results/?label=master&amp;label=experimental&amp;aligned&amp;view=subtest&amp;q=math%20%20not%28path%3A%2Fjs%29%20not%28path%3A%2Fhtml%29">around 3000 tests</a> following the format of <a href="https://web-platform-tests.org/">Web Platform tests</a>! Trying to <a href="https://people.igalia.com/fwang/blink-on-17/#/19">analyze that a bit</a>, Chrome has an excellent pass rate except for things that need to be clarified in the spec. Firefox and Safari are also doing good job but failing on tests for new behavior or features that got clarified by MathML Core.</p>

<p>A complementary metrics for interoperability is MDN’s <a href="https://github.com/mdn/browser-compat-data">browser-compat-data</a>. You can find these compatibility data at the bottom of MDN pages, for example for the <a href="https://developer.mozilla.org/en-US/docs/Web/MathML#browser_compatibility">MathML article</a>. Again, a <a href="https://people.igalia.com/fwang/blink-on-17/#/20">quick analysis</a> confirms that browsers are quite interoperable for MathML Core, possibly mixed with other web technologies, but not for new CSS features (implemented in Chromium) or legacy MathML features (remaining in Firefox and Safari).</p>

<h2 id="accessibility">Accessibility</h2>

<p><a href="https://en.wikipedia.org/wiki/Abraham_Nemeth">Abraham Nemeth</a> who developed Braille code for mathematical notations, presented his view on math accessibility in the book Braille into the next millenium (2000):</p>

<blockquote>
  <p>The Principle of Meaning Versus Notation: In my view, it is the transcriber’s function to supply only notation, not meaning in an accessible form (speech or braille). It is the reader’s function to extract the meaning from the notation the transcriber supplies. Consider the common notation (x,y). That notation can mean many things: the ordered pair whose first component is x and second component is y ; the point in the cartesian coordinate with abscissa x and ordinate y; the open interval on the real line with left endpoint x and right endpoint y; or the greatest common divisor of x and y. The transcriber’s function, however, is only to convey this five-symbol expression to the reader. It is the reader’s function to extract whatever meaning his experience and the context of the text permit.</p>
</blockquote>

<p>However, for people with different need, or for various uses cases, it is often important to provide more semantic. This is something various members from the MathML WG have worked on and many discussions are currently happening.</p>

<p>In any case, for native MathML implementation in browsers we are limited to what was called “presentation MathML” in legacy specifications, which gives a very small amount of information: an <code class="language-plaintext highlighter-rouge">&lt;mfrac&gt;</code> can be fraction, binomial coefficient etc ; an <code class="language-plaintext highlighter-rouge">&lt;msup&gt;</code> can be used to denote a power, a derivative, an index etc ; an <code class="language-plaintext highlighter-rouge">&lt;mtable&gt;</code> can be used for matrices, to perform table layout etc</p>

<p>As explained above, some effort was done to implement native accessibility support for MathML in WebKit/Gecko for various assistive technologies in Linux, macOS or Windows. For the present project, we didn’t try to do more than what currently exists. We only documented existing support in the <a href="https://w3c.github.io/mathml-aam/">MathML AAM</a> specification and implemented it in Chromium. This is the bare minimum we can do to ensure the reader can follow Nemeth’s approach.</p>

<h2 id="conclusion">Conclusion</h2>

<p>As the main person who has led this effort, this is great personal achievement and I’d like to thank all the people who supported it, including my colleagues at Igalia, members of the MathML community, standardization groups, browser developers, web developers, sponsors and contributors to the <a href="https://opencollective.com/mathml-core-support">Open Collective</a>. Finally we made it! 🎉</p>

{% endraw %}
