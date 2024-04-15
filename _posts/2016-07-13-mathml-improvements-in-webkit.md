---
layout: post
title: "MathML Improvements in WebKit"
tags: mathml webkit
---

{% raw %}

  <p>In a <a href="https://frederic-wang.fr/mathml-refactoring-in-webkit.html">previous blog post</a>, I explained the work made by <a href="http://igalia.com/">Igalia</a>’s
web platform team to refactor WebKit’s
MathML layout classes. I stated that although some rendering improvements were
a nice side effect, the main goal of <a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring#Phase1">the first phase</a> was really to clean the code up so
that it is easier for developers to work on MathML in the future. Indeed this
<em>really</em> made things easier to review: Quite unexpectedly to me,
<a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring#Phase2">the second phase</a>
only took 4 days to be upstreamed… Kudos to
<a href="http://whtconstruct.blogspot.fr/">Brent Fulgham</a> for having reviewed so many
patches in such a short period of time!</p>

<p>In this blog post, I am going to give an overview of the improvements made
during these two first phases taking <a href="https://trac.webkit.org/changeset/203109">changeset r203109</a> as a reference. The changes will be available in <a href="https://webkitgtk.org/">WebKitGTK+ 2.14</a> in September and are likely to be included this month in the next <a href="https://developer.apple.com/safari/technology-preview/">Safari Technology Preview</a>.
It definitely remains more work to do such as
<a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring#Phase3">the third phase</a> or other rendering improvements, but I believe we have already made a big
step forward!</p>

<h3 id="mathematical-fonts">Mathematical Fonts</h3>

<p>Two years ago, basic support for operator stretching via the OpenType MATH
table was added to WebKit. During the refactoring, we improved that support
and also made use of more parameters to improve the math layout (see section
about OpenType MATH parameters below). While
<a href="http://www.gust.org.pl/projects/e-foundry/lm-math">Latin Modern Math</a> will be used in most screenshots, the following one shows that you can
use any <a href="http://trac.webkit.org/wiki/MathML/Fonts">math fonts</a>. By default
WebKit will try and use one of these fonts but if none are available or if you
force a non-math <code class="language-plaintext highlighter-rouge">font-family</code> then the rendering quality may not be good.</p>

<p>The following screenshot gives the rendering for various fonts.
For the last one
we used the value <code class="language-plaintext highlighter-rouge">sans-serif</code> to illustrate issues with non-math fonts
(displaystyle integral too small, mathvariant italic glyphs taken from another
font, missing italic correction etc).</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/webkitgtk-r203109-fonts.png"><img width="500" src="https://frederic-wang.fr/images/webkitgtk-r203109-fonts.png" alt="Screenshots of a formula with various fonts" /></a>
  <small>
  Integral obtained by <a href="https://en.wikipedia.org/wiki/Methods_of_contour_integration">contour integration</a><br />
  WebKitGTK+ r203109 with various font-family values.<br />
  From top to bottom:
  <a href="http://www.gust.org.pl/projects/e-foundry/tg-math/download/index_html#Schola_Math">TeX Gyre Schola</a>, <a href="http://www.gust.org.pl/projects/e-foundry/lm-math">Latin Modern</a>, <a href="https://github.com/dejavu-fonts/dejavu-fonts">DejaVu Math</a>, <a href="http://stixfonts.org/">STIX</a>,
and <code>sans-serif</code>.</small>
</div>

<h3 id="the-href-attribute">The <code class="language-plaintext highlighter-rouge">href</code> Attribute</h3>

<p>This new feature is obvious: You can now create a hyperlink for any part
of a mathematical formula! Here is a screenshot of the MathML Torture Test 21
with additional links, as displayed in WebKit r203109. Click the image to load
the test case in your browser and test it.</p>

<div style="text-align: center; width: 378px; margin-left: auto; margin-right: auto;">
  <a href="https://bug-85733-attachments.webkit.org/attachment.cgi?id=274756"><img width="378" src="https://frederic-wang.fr/images/r203109-latin-modern-math-href.png" alt="Screenshot of MathML Torture test 21 with hyperlinks" /></a>
</div>

<h3 id="the-mathvariant-attribute">The <code class="language-plaintext highlighter-rouge">mathvariant</code> Attribute</h3>

<p>Unicode contains <a href="https://en.wikipedia.org/wiki/Mathematical_Alphanumeric_Symbols">Mathematical Alphanumeric Symbols</a> to convey special meaning such as <a href="https://en.wikipedia.org/wiki/Blackboard_bold">double-struck</a> or specific <a href="https://www.w3.org/TR/arabic-math/#N10951">Arabic styles</a>. Characters for these symbols are generally provided by
<a href="http://fred-wang.github.io/MathFonts/">math fonts</a>.
In MathML, mathematical variables are automatically rendered using the
italic characters from this Unicode block. One can also access these characters
via the <code class="language-plaintext highlighter-rouge">mathvariant</code> attribute and that attribute is actually used by many
LaTeX-to-MathML converters.</p>

<p>In the following screenshot, you can see that the letters f, x and y are now
drawn with this special mathematical italic glyphs and that WebKit uses the
conventional fraktur style for the Lie algebra g. Note that the prime is still too
small because WebKit does not make use of the <a href="https://www.microsoft.com/typography/otspec/features_pt.htm#ssty">ssty feature</a> yet.</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-lie-algebra-mathvariant.png"><img width="500" src="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-lie-algebra-mathvariant.png" alt="Screenshot of Wikipedia article on Lie Algebra" /></a>
  <small>Homomorphism of <a href="https://en.wikipedia.org/wiki/Lie_algebra">Lie algebra</a><br />
  Top: Safari 9.1.1. Bottom: Safari r203109.</small>
</div>

<h3 id="operators-and-spacing">Operators and Spacing</h3>

<p>As said in my previous blog post, the rendering of large and stretchy operators
have been rewritten a lot and as a consequence the rendering has improved.
Also, I mentioned that <a href="https://wikimedia.org/api/rest_v1/media/math/render/svg/5d166c08a30ad598edc84d0bbe0223be8bcc5a6d">the width of operators may depend on their height</a>. This may cause accumulated approximations
during the computation of preferred widths. The old flexbox-based implementation
<a href="https://bugs.webkit.org/show_bug.cgi?id=107613">incorrectly forced layout during preferred computation</a> to avoid that but a quick
workaround for that security concern caused the approximate
preferred widths to be used for the logical widths. With our new implementation,
the logical width is now correctly calculated.
Finally, we added partial support for the <code class="language-plaintext highlighter-rouge">mpadded</code> element
which is often used to tweak spacing in mathematical formulas.</p>

<p>The screenshot below illustrates the fix for a
<a href="https://bugs.webkit.org/show_bug.cgi?id=151916">serious regression with large operator</a> (summation symbol) as well as improvements in the rendering of
stretchy operators (horizontal braces). Note that the formula has a hack with
a zero-width <code class="language-plaintext highlighter-rouge">mpadded</code> element which used to cause improper spacing
(large gap between the group of a’s and the group of b’s).</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-torture-test-operator-and-spacing.png"><img width="500" src="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-torture-test-operator-and-spacing.png" alt="Screenshot from Mozilla's MathML torture test using Safari 9.1.1 or the the current refactoring" /></a>
  <small>Tests 21 and 22 from the <a href="https://developer.mozilla.org/en-US/docs/Mozilla_MathML_Project/MathML_Torture_Test">MathML torture test</a><br />
  Left: Safari 9.1.1. Right: Safari r203109.</small>
</div>

<p>The following screenshot shows how incorrect width computations used to cause
excessive spacing after the stretchy radical and slash symbols:</p>

<div style="text-align: center; width: 484px; margin-left: auto; margin-right: auto;">
<a href="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-trigonometric-functions-width.png"><img width="484" src="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-trigonometric-functions-width.png" alt="Screenshot of Wikipedia article on Trigonometric Functions" /></a>
  <small><a href="https://en.wikipedia.org/wiki/Trigonometric_functions">Sine of 1 degree</a><br />
  Top: Safari 9.1.1. Bottom: Safari r203109.</small>
</div>

<h3 id="the-displaystyle-property">The <code class="language-plaintext highlighter-rouge">displaystyle</code> Property</h3>

<p>Mathematical formulas can be integrated inside a paragraph of text (inline math
in TeX terminology) or displayed in its own horizontally centered paragraph
(display math in TeX terminology). In the latter case, the formula is in
<code class="language-plaintext highlighter-rouge">displaystyle</code> and does not have any restrictions on vertical spacing.
In the former case, the layout of the mathematical formula is modified a bit to
optimize this vertical spacing and to better integrate within the surrounding text.
The <code class="language-plaintext highlighter-rouge">displaystyle</code> property can also be set using the corresponding attribute or
can change automatically in subformulas (e.g. in fractions).</p>

<p>In the following screenshot the fix for the large operator regression is
obvious but you can also notice that the summation is now slightly different
for the definition of a Bézier curve (top) and for the one of
a rational Bézier curve
(bottom). For example, to save some vertical space in the fractions, the
sigma symbol is drawn smaller and the scripts attached to it are moved on
its right. However, the script size could still be improved when we implement
the <a href="https://bugs.webkit.org/show_bug.cgi?id=151916">scriptlevel</a> property.</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-bezier-displaystyle.png"><img width="500" src="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-bezier-displaystyle.png" alt="Screenshot of Wikipedia article on Bézier Curves" /></a>
  <small><a href="https://en.wikipedia.org/wiki/B%C3%A9zier_curve">Definitions of Bézier Curve</a><br />
  Left: Safari 9.1.1. Right: Safari r203109.</small>
</div>

<h3 id="opentype-math-parameters">OpenType MATH Parameters</h3>

<p>Many new <a href="https://trac.webkit.org/wiki/MathML/Fonts#OpenFontFormatfeatures">OpenType MATH features</a> have been implemented following the
<a href="http://www.mathml-association.org/MathMLinHTML5/">MathML in HTML5 Implementation Note</a>:</p>

<ul>
  <li>Use of the <code class="language-plaintext highlighter-rouge">AxisHeight</code> parameter to set vertical position of fractions,
tables and symmetric operators.</li>
  <li>Use of layout constants for radicals (some of them were already used),
scripts and fractions. This improves math spacing and positioning and allows
to adjust them according to value of the <code class="language-plaintext highlighter-rouge">displaystyle</code> property discussed
in the previous section.</li>
  <li>Use of the italic correction of large operator glyph to set the position of
subscripts.</li>
</ul>

<p>The screenshots below illustrate some of these improvements. For the first one,
the use of <code class="language-plaintext highlighter-rouge">AxisHeight</code> allows to better align the fraction bar with the plus
sign. For the second one, the use of layout constants for scripts as well
as the italic correction of the integral improves the placement of limits.</p>

<div style="text-align: center; width: 498px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-continued-fraction-axis-height.png"><img width="498" src="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-continued-fraction-axis-height.png" alt="Screenshot of Wikipedia article on the Continued Fractions" /></a>
  <small><a href="https://en.wikipedia.org/wiki/Generalized_continued_fraction">Generalized Continued Fraction</a><br />
  Top: Safari 9.1.1. Bottom: Safari r203109.</small>
</div>

<div style="text-align: center; width: 378px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-gamma-function-scripts.png"><img width="378" src="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-gamma-function-scripts.png" alt="Screenshot of Wikipedia article on the Gamma Function" /></a>
  <small><a href="https://en.wikipedia.org/wiki/Gamma_function">Definition of the Gamma Function</a><br />
  Top: Safari 9.1.1. Bottom: Safari r203109.</small>
</div>

<h3 id="right-to-left-radicals">Right-to-left radicals</h3>

<p>One of the advantage of the old flexbox-based implementation is that
right-to-left layout was available for free. This support has of course been
preserved in the new implementation. We also added a simple workaround to mirror
radicals using a scale transform
as shown in the screenshot below. However, general
<a href="https://bugs.webkit.org/show_bug.cgi?id=130840">glyph-level mirroring</a> is still
missing.</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-torture-test-rtl.png"><img width="500" src="https://frederic-wang.fr/images/safari9-vs-r203109-latin-modern-math-torture-test-rtl.png" alt="Screenshot of Wikipedia article on Lie Algebra" /></a>
  <small>Test 13 from the <a href="https://developer.mozilla.org/en-US/docs/Mozilla_MathML_Project/MathML_Torture_Test">MathML torture test (Machrek Style)</a><br />
  Top: Safari 9.1.1. Bottom: Safari r203109.</small>
</div>

<h3 id="conclusion">Conclusion</h3>

<p>Igalia’s web platform team has been able to follow the
<a href="http://www.mathml-association.org/MathMLinHTML5/">MathML in HTML5 Implementation Note</a> in order to significantly improve the rendering of mathematical
expressions in WebKit. More work remains to do but
we will definitely appreciate any feedback that can
help improving native MathML support in web engines.
We are also excited to continue work and collaboration at the next
<a href="http://www.webengineshackfest.org/">Web Engines Hackfest</a>!</p>

{% endraw %}
