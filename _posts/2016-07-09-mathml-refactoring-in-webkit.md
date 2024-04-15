---
layout: post
title: "MathML Refactoring in WebKit"
tags: mathml webkit
---

{% raw %}

  <h2 id="introduction">Introduction</h2>

<p>If you follow WebKit developments, you are certainly aware that
<a href="http://igalia.com/">Igalia</a> has been working on WebKit’s
MathML implementation for some time. More recently, effort has been made to
<a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring">write a clean implementation</a>
addressing issues reported by WebKit reviewers in the past.
After joining Igalia in March, I have been in charge of
getting this work reviewed and merged into WebKit’s development branch.
In the past four months, we have been successful in upstreaming the
<a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring#Phase1">first phase</a>
of the refactoring and the work accomplished is described in this blog post.</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;" id="safari9VSrefactoring">
  <a href="https://frederic-wang.fr/images/safari9-vs-refactoring-latin-modern-math.png"><img width="500" src="https://frederic-wang.fr/images/safari9-vs-refactoring-latin-modern-math.png" alt="Screenshot from Mozilla's MathML torture test using Safari 9.1.1 or the the current refactoring" /></a><br />
  <small><a href="https://developer.mozilla.org/en-US/docs/Mozilla_MathML_Project/MathML_Torture_Test">MathML torture tests</a> with the <a href="http://www.gust.org.pl/projects/e-foundry/lm-math">Latin Modern Math font</a><br />
  Left: Safari 9.1.1. Right: Current MathML branch.</small>
</div>

<p>Note that the focus was on code refactoring so the improvement may not be obvious
for non-developers. Nevertheless many issues have already been fixed as a
consequence of that work: math italic, position of scripts,
stretchy and large operators, rendering update and more.
More importantly, this preliminary step opens the way for
<a href="http://www.mathml-association.org/MathMLinHTML5/">beautiful math rendering based on TeX rules and the OpenType MATH table</a>. Rendering improvements and
implementation of new features have already started in the
<a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring#Phase2">next phase</a>
of the refactoring, so stay tuned…</p>

<h2 id="design-issues">Design Issues</h2>

<p>As explained in a <a href="https://frederic-wang.fr/mathml-at-the-web-engines-hackfest-2015.html">previous report</a>, the main design issues in the
flexbox-based implementation released in 2013
can essentially be summarized in three points:</p>

<ol>
  <li>WebKit’s code to stretch operator was not efficient at all and was limited to some basic fences buildable via Unicode characters.</li>
  <li>WebKit’s MathML code violated many layout invariants, making the code unreliable.</li>
  <li>WebKit’s MathML code relied heavily on the C++ renderer classes for flexboxes and had to manage too many anonymous renderers.</li>
</ol>

<p>For the first point, the performance issue had been fixed by Igalia developers
right after the initial feedback from WebKit developers and
<a href="https://bugs.webkit.org/show_bug.cgi?id=155434">we improved that again</a>
during our refactoring.
Partial support for the OpenType MATH table was added during
<a href="http://www.ulule.com/mathematics-ebooks/">my crowdfunding project</a> and allowed
to stretch more operators with the help of math fonts. For the second point,
<a href="https://bugs.webkit.org/show_bug.cgi?id=107613">the main issue</a> was also
fixed right after the initial feedback. However one could still have some
doubts regarding the layout steps, given the complexity implied by the third
point. That last issue was still problematic so far and addressing it was the
main achievement of our refactoring.</p>

<p>Technically, the dependence on flexbox is unnecessary and the implementation
actually only used a limited set of flexbox features. Thus executing the whole
flexbox code was overkill. It can also be a burden for
people working on other places of the layout code. For example
<a href="https://www.igalia.com/nc/igalia-247/igalian/item/jfernandez/">Javi Fernández</a> has worked on improving the
<a href="http://blogs.igalia.com/jfernandez/2015/01/12/box-alignment-and-grid-layout-ii/">box alignments</a> in the past
and he had hard time fixing the <a href="https://bugs.webkit.org/show_bug.cgi?id=138095">MathML code impacted by his changes</a>. This is probably the cause of the
<a href="https://webkit.org/b/151916">bad position of the summation symbol</a>
that can be seen in the <a href="#safari9VSrefactoring">screenshot above</a>.</p>

<p>From the layout perspective, most of the rendering logic was
implemented in the flexbox classes and the MathML “renderer” classes were really
just managing the creation and update of anonymous nodes and style.
Although this sounds good code
reuse it actually made impossible to understand how and when layout steps
happen or to add more advanced features.
The new implementation replaced this manipulation of the render tree with
simple arithmetic calculations on box metrics which is safer and more reliable.
Also, complex renderers such as
<code class="language-plaintext highlighter-rouge">RenderMathMLScripts</code> or <code class="language-plaintext highlighter-rouge">RenderMathMLRoot</code>
actually achieve better rendering quality with less code!</p>

<p>As an example of the complexity, <code class="language-plaintext highlighter-rouge">RenderMathMLUnderOver</code> can behave as a
<code class="language-plaintext highlighter-rouge">RenderMathMLScripts</code>
in some situation so we really want the former class to reuse the
latter class. As we will see below the old implementation of the two renderers
were quite different: <code class="language-plaintext highlighter-rouge">RenderMathMLUnderOver</code> only relied on setting column
direction in the user agent stylesheet while <code class="language-plaintext highlighter-rouge">RenderMathMLScripts</code> created
a complex render tree structures with anonymous style. Hence it seemed difficult
to share the two cases or to handle DOM changes causing to move from one
case to the other one. With our new implementation, this is simply reduced to
<a href="https://bugs.webkit.org/show_bug.cgi?id=155542">simple C++ inheritance</a>.</p>

<p>When I started to work on WebKit some years ago,
I made the mistake of continuing with
the existing approach. The implementation of <a href="https://bugs.webkit.org/show_bug.cgi?id=99618">multiscripts</a> or <a href="https://bugs.webkit.org/show_bug.cgi?id=44208">automatic italic mathvariant</a> added more anonymous objects
and made the situation even worse. After the end of my crowdfunding project,
<a href="https://www.igalia.com/nc/igalia-247/igalian/item/alex/">Alex Castro</a>
did more cleanup and tried to implement important features such as
<a href="https://bugs.webkit.org/show_bug.cgi?id=133845">displaystyle</a>
but he also soon realized that it was too hard to work with the current code
base…</p>

<h2 id="layout-refactoring">Layout Refactoring</h2>

<p>In order to solve the issues discussed in the previous section,
Javi and Alex worked on a new MathML branch where the first step was to remove
the inheritance on the flexbox layout classes.
During the Web Engines Hackfest 2015, I collaborated with the Igalia’s
web platform team
team to continue the work on this branch. In a second step, we rewrote many
MathML renderer functions so that they stop creating anonymous nodes or style.
We obtained very encouraging results: The implementation looked much
simpler and much more understandable!</p>

<p><a href="https://lists.webkit.org/pipermail/webkit-dev/2015-December/027840.html">Alex announced the initial plan on the webkit-dev mailing list</a>. He started opening bugs
and attaching patches to merge the first step.
However, that step still required many of the flexbox logic and so made code
hard to understand for reviewers. Hence when I joined Igalia four months ago
Alex asked me to try and see how to reorganize patches so that the two initial
steps can be submitted in one go.
This corresponds to the first phase mentioned in the introduction. As indicated
on the <a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring">wiki page</a>,
the layout refactoring consisted in rewriting the following member functions
of each renderer class:</p>

<ul>
  <li>computePreferredLogicalWidths: calculate preferred widths, based on the
preferred widths of child renderers.</li>
  <li>layoutBlock: set final position and size of child renderers.</li>
  <li>firstLineBaseLine: calculate the ascent of the renderer.</li>
  <li>paint (optional): perform special painting such as fraction bars.</li>
</ul>

<p>Refactored renderers no longer rely on any flexbox code nor anonymous
renderers and the functions mentioned above essentially perform arithmetic
computations. By reading the code, one can be sure that we follow
standard layout rules and that we do not perform unnecessary reflow.
Moreover, the <a href="http://www.mathml-association.org/MathMLinHTML5/S3.html">rules specific to math rendering</a> are only located in the MathML renderers and can be
better understood. Details for each class are provided in the next subsections.
After all the layout functions were rewritten and the code managing the
render tree structure removed, we were able to make the
<code class="language-plaintext highlighter-rouge">RenderMathMLBlock</code> class
inherit from <code class="language-plaintext highlighter-rouge">RenderBlock</code> instead of <code class="language-plaintext highlighter-rouge">RenderFlexibleBox</code>.
Many of the bugs could
then be immediately closed or otherwise fixed with small follow-up patches.</p>

<h3 id="spacing">Spacing</h3>

<p><code class="language-plaintext highlighter-rouge">RenderMathMLSpace</code> is a simple class inserting blank boxes for adjusting
  spacing of math formulas.
  Obviously, we do not need any of the complexity of flexbox so it was
  straightforward to write the layout functions.</p>

<div style="text-align: center">
     <math display="block"><mn>3</mn><mspace width="3em" /><mi>x</mi></math>
     <small>Large space between 3 and x.</small>
  </div>

<h3 id="grouping">Grouping</h3>

<p><code class="language-plaintext highlighter-rouge">RenderMathMLRow</code> performs rendering of a row of math items.
  Since WebKit does not support linebreaking in MathML at the
  moment, this is just putting child boxes on a same baseline.
  One specificity is that some operators can be stretched vertically and so
  <a href="https://wikimedia.org/api/rest_v1/media/math/render/svg/5d166c08a30ad598edc84d0bbe0223be8bcc5a6d">their width may depend on their height</a>.</p>

<div style="text-align: center">
     <math display="block">
       <mrow>
         <mo>{</mo>
         <mfrac><mn>2</mn><mi>x</mi></mfrac>
         <msup>
           <mi>x</mi>
           <mn>3</mn>
         </msup>
       </mrow>
     </math>
     <small>Row containing a stretched brace, a fraction and a scripted element.</small>
  </div>

<p>Again, flexbox features are useless here. With the old code, it was
  not clear whether we were violating the CSS invariant with preferred and
  logical widths and which kind of relayout or render tree changes would happen
  when doing the stretch call. By properly implementing the layout functions
  previously mentioned all of this became much more trustable.</p>

<h3 id="fractions">Fractions</h3>

<p><code class="language-plaintext highlighter-rouge">RenderMathMLFraction</code> draws a fraction with numerator and denominator.</p>

<div style="text-align: center">
     <math display="block"><mfrac><mrow><mi>x</mi><mo>+</mo><mn>1</mn></mrow><mrow><mi>y</mi><mo>+</mo><mn>2</mn></mrow></mfrac></math>
     <small>Simple fraction.</small>
  </div>

<p>This used to be implemented using a column direction for the fraction element.
  Numerator and denominator were wrapped into anonymous nodes with additional
  style to leave space for the fraction bar and to adjust the horizontal
  alignments.</p>

<pre>RenderMathMLFraction (flexbox with column direction)
  RenderMathMLBlock (anonymous flexbox)
    RenderMathMLRow (numerator)
      ...
  RenderMathMLBlock (anonymous flexbox)
    RenderMathMLRow (denominator)
      ...
</pre>

<p>It was relatively easy to implement this without any anonymous nodes and again
  the use of flexbox did not sound justified.
  For example, to calculate the preferred width we just take the maximum
  of the preferred widths of the numerator and denominator.
  For the layout, the calculation of the logical width is similar and we
  calculate the horizontal coordinates of numerator and denominator so that
  their centers are aligned. Vertical metrics are similarly calculated
  from the vertical metrics of the numerator and denominator.
  During that step, we also fixed some bugs with the <code class="language-plaintext highlighter-rouge">linethickness</code> attribute and
  added support for some OpenType MATH table constants.</p>

<h3 id="scripts-above-and-below">Scripts above and below</h3>

<p><code class="language-plaintext highlighter-rouge">RenderMathMLUnderOver</code> is used to attach some scripts above and below a base.
  Each child can itself be a horizontal stretchy operator.</p>

<div style="text-align: center">
     <math display="block"><mover><mtext>base</mtext><mo>→</mo></mover></math>
     <small>Base with stretchy arrow over it.</small>
  </div>

<p>This was implemented in the user agent stylesheet by using
  flexboxes with column direction for the corresponding MathML elements and
  the C++ class had
  additional rules to fire the stretching. So the problems and solutions for
  this class were essentially a mixed of the cases of
  <code class="language-plaintext highlighter-rouge">RenderMathMLFraction</code> and <code class="language-plaintext highlighter-rouge">RenderMathMLRow</code> we just discussed.</p>

<h3 id="subscripts-and-superscripts">Subscripts and Superscripts</h3>

<p><code class="language-plaintext highlighter-rouge">RenderMathMLScripts</code> is used for a base with some arbitrary number of scripts.
  All the scripts can have different positions (pre, post, sub, super) and
  metrics (width, ascent and descent). We must avoid collisions and take care
  of horizontal and vertical alignements.</p>

<div style="text-align: center">
     <math display="block">
       <mmultiscripts>
         <mtext>base</mtext>
         <mi>a</mi>
         <mi>b</mi>
         <mi>c</mi>
         <none />
         <mprescripts />
         <none />
         <mi>d</mi>
         <mi>e</mi>
         <mi>f</mi>
       </mmultiscripts>
     </math>
     <small>Base with pre and post scripts.</small>
  </div>

<p>The old code used a complex render tree with additional style to achieve the
  best possible result.
  However, the quality was still bad as you can see for the script
  attached to
  the integral in the <a href="#safari9VSrefactoring">screenshot above</a>.
  Managing the render tree was a nightmare: Just to give the idea, additional
  anonymous node and style were used to allow horizontal and vertical
  adjustments (similar to <code class="language-plaintext highlighter-rouge">RenderMathMLFraction</code> above) and prescripts had
  negative order property so that they were positioned before the base.</p>

<pre>RenderMathMLScripts
    Base Wrapper (anonymous flexbox)
      RenderMathMLRow (base)
        ...
    SubSupPair Wrapper (anonymous flexbox with column direction)
      RenderMathMLRow (post-subscript)
        ...
      RenderMathMLRow (subperscript)
        ...
    SubSupPair Wrapper (anonymous flexbox with column direction)
      RenderMathMLRow (post-subscript)
        ...
      RenderMathMLRow (post-superscript)
        ...
    ... (more postscripts)
    RenderMathMLBlock (prescripts separator)
    SubSupPair Wrapper (anonymous flexbox with column direction and order -1)
      RenderMathMLRow (pre-subscript)
        ...
      RenderMathMLRow (pre-subperscript)
        ...
    SubSupPair Wrapper (anonymous flexbox with column direction and order -1)
      RenderMathMLRow (pre-subscript)
        ...
      RenderMathMLRow (pre-superscript)
        ...
    ... (more prescripts)
</pre>

<p>Rules from TeX and the OpenType MATH table are
  relatively complex and we decided to implement them directly in the new
  refactoring as otherwise it was impossible to get decent quality. The code is
  still complex but we now have clear rules, we only perform simple
  calculations and the render tree structure matches the DOM tree.</p>

<h3 id="enclosing-notations">“Enclosing” Notations</h3>

<p><code class="language-plaintext highlighter-rouge">RenderMathMLMenclose</code> is a row of math items with some additional notations.
  <a href="https://bugs.webkit.org/show_bug.cgi?id=85729">Gurpreet Kaur implemented this element two years ago</a>
  but she followed the same approch, combining anonymous nodes and style for
  some simple notations and special painting for others.</p>

<div style="text-align: center">
     <math display="block">
       <menclose notation="circle updiagonalstrike">
         <mi>x</mi><mo>+</mo><mn>1</mn>
       </menclose>
     </math>
     <small>circle and strike notations</small>
  </div>

<p>During the refactoring, the code has been completely
  rewritten so that <code class="language-plaintext highlighter-rouge">RenderMathMLMenclose</code> is now essentially a derived class
  of <code class="language-plaintext highlighter-rouge">RenderMathMLRow</code>
  with the measuring and painting functions adjusted to take into account the
  additional notations. During that refactoring, we also
  <a href="https://lists.webkit.org/pipermail/webkit-dev/2016-March/028064.html">removed support for unused radical notation</a>, which was implemented using an anonymous
  <code class="language-plaintext highlighter-rouge">RenderMathMLSquareRoot</code> (see Radicals section below).</p>

<h3 id="helper-classes-for-operators">Helper Classes for Operators</h3>

<p>The <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> class is used for math operators.
  It was quite complex class and we decided to extract from it two features that
  are unrelated to layout:</p>

<ul>
  <li>
    <p>The <a href="https://www.w3.org/TR/MathML3/appendixc.html">MathML operator dictionary</a> and corresponding search functions have been moved into a
  <code class="language-plaintext highlighter-rouge">MathOperatorDictionary</code> class.</p>
  </li>
  <li>
    <p>Selection, measuring and drawing of stretchy operators have been moved into a
<code class="language-plaintext highlighter-rouge">MathOperator</code> class. This is essentially
the <a href="https://frederic-wang.fr/opentype-math-in-harfbuzz.html">low-level text shaping being implemented in HarfBuzz</a>.</p>
  </li>
</ul>

<p>The remaining code was indeed the real layout part but the mess with
  anonymous node and style was only removed later (see Text Classes below).
  Although it seems we just needed to move the code out of <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code>
  into those new classes, the case of <code class="language-plaintext highlighter-rouge">MathOperator</code> was particularly difficult.
  We had to split the effort into several small steps to make review possible
  and also fixed many issues due to the entanglement and confusion of these
  three different features of the <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> class…
  The work done for <code class="language-plaintext highlighter-rouge">MathOperator</code> actually improved the rendering
  of stretchy operators as you can see for the horizontal braces in the
  <a href="#safari9VSrefactoring">screenshot above</a>.</p>

<h3 id="radicals">Radicals</h3>

<p><code class="language-plaintext highlighter-rouge">RenderMathMLRoot</code> is used for square root or arbitrary N-th root.
  Many of the TeX and OpenType MATH table rules
  were already used by the old implementation with anonymous
  nodes and style. However, there were bugs difficult to fix related to
  <a href="https://bugs.webkit.org/show_bug.cgi?id=143397">zooming</a>,
  <a href="https://bugs.webkit.org/show_bug.cgi?id=134018">child removal</a> or
  <a href="https://bugs.webkit.org/show_bug.cgi?id=134020">style change</a> due to the
  management of the anonymous <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> to draw the radical sign.</p>

<div style="text-align: center">
     <math display="block">
       <msqrt>
         <mi>x</mi><mo>+</mo><mn>1</mn>
       </msqrt>
       <mo>+</mo>
       <mroot>
         <mrow><mi>x</mi><mo>+</mo><mn>1</mn></mrow>
         <mn>3</mn>
       </mroot>
     </math>
     <small>square and cube roots</small>
  </div>

<p>The old implementation actually had two classes for the square and general
  cases (<code class="language-plaintext highlighter-rouge">RenderMathMLSquareRoot</code> and <code class="language-plaintext highlighter-rouge">RenderMathMLRoot</code>). The usual
  technique
  with various anonymous wrappers and style was used.
  After the refactoring, we were able to merge everything in a single
  <code class="language-plaintext highlighter-rouge">RenderMathMLRoot</code>
  class. Because the square root behaves as an <code class="language-plaintext highlighter-rouge">mrow</code>, we also made that class
  derive from <code class="language-plaintext highlighter-rouge">RenderMathMLRow</code> to reuse as much code as possible.
  Here is are how the render trees used to look like:</p>

<pre>RenderMathMLSquareRoot
  RenderMathMLBlock (anonymous used for metric adjustements)
    RenderMathMLRadicalOperator (anonymous used for the radical symbol)
      ...
  RenderMathMLRootWrapper (anonymous used for the children)
    RenderMathMLRow (child 1)
      ...
    RenderMathMLRow (child 2)
      ...
    ...
    RenderMathMLRow (child N)
      ...

RenderMathMLRoot
  RenderMathMLRootWrapper (anonymous for the index)
    ...
  RenderMathMLBlock (anonymous used for metric adjustements)
     RenderMathMLRadicalOperator (anonymous used for the radical symbol)
       ...
  RenderMathMLRootWrapper (anonymous for the base)
    ...
</pre>

<p>Again, we rewrote the implementation using only simple box positioning.
  The difficult part was to get rid of the anonymous
  <code class="language-plaintext highlighter-rouge">RenderMathMLRadicalOperator</code> to draw the radical symbol. This class was
  derived from <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> and extended it with some fallback drawing
  when math fonts were not available. After having extracted stretchy operator
  shaping from <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> it became possible to use the
  <code class="language-plaintext highlighter-rouge">MathOperator</code>
  helper class to draw the radical symbol. We implemented the fallback for
  missing math fonts the same as Gecko: Use a scale transform to stretch
  the base glyph for U+221A SQUARE ROOT. As a bonus, we used such transform to
  implement glyph mirroring, as required to draw right-to-left radicals in
  some Arabic mathematical notations.</p>

<h3 id="text-classes">Text Classes</h3>

<p>These classes are containers for math text such as variables or
  operators. There is a generic <code class="language-plaintext highlighter-rouge">RenderMathMLToken</code> class and
  a derived class <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> adding features
  specific to operators such as spacing, dictionary property, stretching…
  Anonymous wrappers and style were used to implement
  <a href="https://bugs.webkit.org/show_bug.cgi?id=44208">automatic italic mathvariant</a>
  or <a href="https://bugs.webkit.org/show_bug.cgi?id=115787">operator spacing</a>. The <code class="language-plaintext highlighter-rouge">RenderText</code> child
  of <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> was (re)built as an anonymous text node
  so that is was possible to
  convert U+002D HYPHEN-MINUS into U+2212 MINUS SIGN
  or to provide some text for anonymous operators created by
  <code class="language-plaintext highlighter-rouge">RenderMathMLFenced</code> (see Unchanged Classes section).</p>

<pre>RenderMathMLToken (e.g. mi element)
  RenderMathMLBlock (anonymous flexbox used to apply CSS italic)
    RenderBlock (anonymous created elsewhere to honor CSS rules)
      RenderText
        text run "x"

RenderMathMLOperator (mo element)
   RenderMathMLBlock (anonymous flexbox used for spacing)
    RenderBlock (anonymous created elsewhere to honor CSS rules)
      RenderText (anonymous destroyed and built again)
         text run "−"
</pre>

<p>We did a big refactoring to remove all the anonymous nodes
  created by the MathML renderer classes.
  Just like for <code class="language-plaintext highlighter-rouge">MathOperator</code>, we had to be careful and submit
  various small pieces as the text rendering was quite sensible to code change.</p>

<p>The simplified operator spacing that was supported by WebKit was easy to
  implement with the new approach.
  To do automatic italic mathvariant, we modified the paint function to use
  <a href="https://en.wikipedia.org/wiki/Mathematical_Alphanumeric_Symbols">Mathematical Alphanumeric Symbols</a> instead of CSS italic as you can notice for the
  variables displayed in the
  <a href="#safari9VSrefactoring">screenshot above</a>. Hence we could
  remove the <code class="language-plaintext highlighter-rouge">RenderMathMLBlock</code> anonymous wrapper.</p>

<p>The use of an anonymous node for the text prevented it to appear in the dumped
  render tree of layout tests and also
  required some hacks in the accessibility code
  to expose that text. In order to address the cases of
  the minus sign and of mfenced operators,
  we decided to use our new <code class="language-plaintext highlighter-rouge">MathOperator</code> class again.
  Indeed <code class="language-plaintext highlighter-rouge">MathOperator</code> is actually also able to draw unstretched operators
  made of a single character and this works for the minus sign and for mfenced
  operators used in practice.</p>

<h3 id="unchanged-classes">Unchanged Classes</h3>

<p>Two classes have not been modified but such modifications were not needed to
  remove the dependency on <code class="language-plaintext highlighter-rouge">RenderFlexibleBox</code>:</p>

<ul>
  <li>
    <p><code class="language-plaintext highlighter-rouge">RenderMathMLFenced</code> is used for an mrow-like element that is
<a href="https://www.w3.org/TR/MathML/chapter3.html#presm.mfenced">defined in the MathML specification</a> as strictly equivalent
   to constructions with rows and operators.
   It is implemented as a derived class
   of <code class="language-plaintext highlighter-rouge">RenderMathMLRow</code> and creates anonymous <code class="language-plaintext highlighter-rouge">RenderMathMLOperators</code>. This is the
   only remaining class that modifies the render tree structure. Note that
   prominent MathML websites and generators do not use the mfenced element,
   so it is not a big concern.</p>
  </li>
  <li>
    <p><code class="language-plaintext highlighter-rouge">RenderMathMLTable</code> is used for table layout. It is just derived from
<code class="language-plaintext highlighter-rouge">RenderTable</code>, not <code class="language-plaintext highlighter-rouge">RenderFlexibleBox</code>. We did not change anything for now
but we considered creating our own
implementation in order to make our code independent from HTML table,
to support MathML-specific table features and to make it better integrated
with the rest of the MathML code.</p>
  </li>
</ul>

<h2 id="accessibility">Accessibility</h2>

<p>Even if our main focus was on rendering, the changes we made also had impact on
the MathML accessibility code. Indeed, the accessibility tree is generated
from the MathML renderer classes: Since we changed the latter during the
refactoring, we also had to adjust the accessibility code. Fortunately,
we are lucky to have <a href="https://www.igalia.com/nc/igalia-247/igalian/item/jdiggs/">Joanmarie Diggs</a> in our team and she was able to provide some help here.</p>

<p>First, the accessibility code exposes the <code class="language-plaintext highlighter-rouge">linethickness</code> of fractions to
implement Apple’s <code class="language-plaintext highlighter-rouge">AXMathLineThickness</code> attribute. In practice, this is really
necessary to know whether the <code class="language-plaintext highlighter-rouge">linethickness</code> is null or not
(e.g.
<a href="https://en.wikipedia.org/wiki/Binomial_coefficient">binomial coefficient</a> VS
the <a href="https://en.wikipedia.org/wiki/Legendre_symbol">Legendre symbol</a>).
Apple’s unit test seemed to expose the ratio between the actual thickness and
the default thickness but the accessibility code really just reads the actual
thickness calculated by <code class="language-plaintext highlighter-rouge">RenderMathMLFraction</code>.
Our fix and improvement for <code class="language-plaintext highlighter-rouge">linethickness</code> made the Apple’s unit test fail so we
had to adjust <code class="language-plaintext highlighter-rouge">RenderMathMLFraction</code> to expose the value expected by that test.</p>

<p>In general, the accessibility code does not care about anonymous nodes
created for layout purpose and there was some code to avoid exposing
them in the accessibility tree. So removing all the anonymous during the
layout refactoring was actually a good and safe thing to do. There were some
helper functions to implement Apple’s <code class="language-plaintext highlighter-rouge">AXMathRootRadicand</code> and
<code class="language-plaintext highlighter-rouge">AXMathRootIndex</code> attributes that had to be adjusted, though. These functions
used to do some work to skip the anonymous wrappers and we were actually able
to simplify them.</p>

<p>There was also some specific code for the <code class="language-plaintext highlighter-rouge">RenderMathMLOperators</code> and their
anonymous <code class="language-plaintext highlighter-rouge">RenderText</code> that were necessary to expose the text content.
Actually, there was an <a href="https://bugs.webkit.org/show_bug.cgi?id=139582">old bug</a>
in the accessibility code and the anonymous
<code class="language-plaintext highlighter-rouge">RenderMathMLOperators</code> created by mfenced were not correctly exposed. The
unit test
we had for mfenced operators was only checking the text content but it was still
passing and so the regression had never been detected before. After
the layout refactoring we removed the anonymous <code class="language-plaintext highlighter-rouge">RenderText</code> of mfenced
operators and so broke that test…
We thus spent some time to fix the <code class="language-plaintext highlighter-rouge">RenderMathMLOperator</code> code. Essentially,
we removed all the old hacks and only left a specific handling for mfenced
operators. We also used this opportunity to improve and extend our MathML
accessibility tests.</p>

<p>Finally, the MathML accessibility code was directly implemented into a generic
<code class="language-plaintext highlighter-rouge">AccessibilityRenderObject</code> class. There was some functions to access
math nodes and properties but also specific cases scattered all over the code
(anonymous boxes, mfenced operators, math roles etc). In order to
facilitate future work and maintenance we decided to move all the
MathML code into a new <code class="language-plaintext highlighter-rouge">AccessibilityMathMLElement</code> class. Hence the work implied
by the layout refactoring actually encouraged us to improve the organization and
testing of our accessibility code!</p>

<h2 id="conclusion">Conclusion</h2>

<p>In the past four months, Igalia’s web platform team has successfully upstreamed
the refactoring of WebKit’s MathML renderer classes and we are now very confident
about the quality of the layout code.
In addition to the people mentioned above I would personally like to thank
everybody who helped with this work.
More specifically, I am very grateful to other people from Igalia
(<a href="https://www.igalia.com/nc/igalia-247/igalian/item/mrobinson/">Martin Robinson</a>,
<a href="https://www.igalia.com/nc/igalia-247/igalian/item/svillar/">Sergio Villar</a> and
<a href="https://www.igalia.com/nc/igalia-247/igalian/item/mrego/">Manuel Rego</a>)
or Apple (<a href="http://whtconstruct.blogspot.fr/">Brent Fulgham</a>
and <a href="https://en.wikipedia.org/wiki/Darin_Adler">Darin Adler</a>) who have
spent some time to review patches.
As a nice side effect of this work,
mathematical formulas look better and the accessibility code has been improved.
More is happenning in the
<a href="https://trac.webkit.org/wiki/MathML/Early_2016_Refactoring">next two phases</a>.
We are looking forward to continuing
implementation of Web standards and collaboration with browser vendors
at the next <a href="http://www.webengineshackfest.org/">Web Engines Hackfest</a>!</p>

{% endraw %}
