---
layout: post
title: "OpenType MATH in HarfBuzz"
tags: mathml igalia
---

{% raw %}

  

<div id="p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text">TL;DR:</span></p>
<ul id="I1" class="ltx_itemize">
<li id="I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_itemize"><span class="ltx_text">•</span></span> 
<div id="I1.i1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text">Work is in progress to add OpenType MATH support in
HarfBuzz and will be instrumental for many math rendering engines relying
on that library, including browsers.</span></p>
</div>
</li>
<li id="I1.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_itemize"><span class="ltx_text">•</span></span> 
<div id="I1.i2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text">For stretchy operators, an efficient way to determine the required number
of glyphs and their overlaps has been implemented and is described here.</span></p>
</div>
</li>
</ul>
</div>
<div id="p2" class="ltx_para">
<p class="ltx_p">In the context of <a href="http://www.igalia.com/webkit/" title="" class="ltx_ref">Igalia browser team</a>
effort to implement
<a href="http://www.mathml-association.org/MathMLinHTML5/" title="" class="ltx_ref">MathML support using TeX rules and OpenType features</a>,
I have started implementation of
<a href="https://github.com/behdad/HarfBuzz/issues/235" title="" class="ltx_ref">OpenType MATH support in HarfBuzz</a>. This table <a href="https://blogs.msdn.microsoft.com/murrays/2014/04/27/opentype-math-tables/" title="" class="ltx_ref">from the OpenType standard</a> is made of three subtables:</p>
</div>
<div id="p3" class="ltx_para">
<ul id="I2" class="ltx_itemize">
<li id="I2.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_itemize">•</span> 
<div id="I2.i1.p1" class="ltx_para">
<p class="ltx_p">The <span class="ltx_text ltx_font_typewriter">MathConstants</span> table, which contains layout constants. For example, the thickness of the fraction bar of <math id="I2.i1.p1.m1" class="ltx_Math" alttext="\frac{a}{b}" display="inline"><semantics><mfrac><mi>a</mi><mi>b</mi></mfrac><annotation encoding="application/x-tex">\frac{a}{b}</annotation></semantics></math>.</p>
</div>
</li>
<li id="I2.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_itemize">•</span> 
<div id="I2.i2.p1" class="ltx_para">
<p class="ltx_p">The <span class="ltx_text ltx_font_typewriter">MathGlyphInfo</span> table, which contains glyph properties. For instance, the italic correction indicating how slanted an integral is e.g. to properly place the subscript in <math id="I2.i2.p1.m1" class="ltx_Math" alttext="\displaystyle\displaystyle\int_{D}" display="inline"><semantics><mstyle displaystyle="true"><msub><mo largeop="true" symmetric="true">∫</mo><mi>D</mi></msub></mstyle><annotation encoding="application/x-tex">\displaystyle\displaystyle\int_{D}</annotation></semantics></math>.</p>
</div>
</li>
<li id="I2.i3" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_itemize">•</span> 
<div id="I2.i3.p1" class="ltx_para">
<p class="ltx_p">The <span class="ltx_text ltx_font_typewriter">MathVariants</span> table, which provides larger size variants for a base glyph or data to build a glyph assembly. For example, either a larger parenthesis or a assembly of U+239B, U+239C, U+239D to write something like:</p>
<table id="S0.Ex1" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex1.m1" class="ltx_Math" alttext="\left(\frac{\frac{\frac{a}{b}}{\frac{c}{d}}}{\frac{\frac{e}{f}}{\frac{g}{h}}}\right." display="block"><semantics><mrow><mo>(</mo><mfrac><mfrac><mfrac><mi>a</mi><mi>b</mi></mfrac><mfrac><mi>c</mi><mi>d</mi></mfrac></mfrac><mfrac><mfrac><mi>e</mi><mi>f</mi></mfrac><mfrac><mi>g</mi><mi>h</mi></mfrac></mfrac></mfrac></mrow><annotation encoding="application/x-tex">\left(\frac{\frac{\frac{a}{b}}{\frac{c}{d}}}{\frac{\frac{e}{f}}{\frac{g}{h}}}\right.</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</li>
</ul>
</div>
<div id="p4" class="ltx_para">
<p class="ltx_p">Code to parse this table was added to Gecko and WebKit two years ago. The
existing code to build glyph assembly in these Web engines was adapted
to use the <span class="ltx_text ltx_font_typewriter">MathVariants</span> data instead of only private tables. However, as
we will see below the <span class="ltx_text ltx_font_typewriter">MathVariants</span> data to build glyph assembly is more
general, with arbitrary number of glyphs or with additional constraints on
glyph overlaps. Also
there are various fallback mechanisms
for old fonts and other bugs that I think we could get rid of
when we move to OpenType MATH fonts only.</p>
</div>
<div id="p5" class="ltx_para">
<p class="ltx_p">In order to add MathML support in Blink, it is very easy to
<a href="https://github.com/fred-wang/chromium.src/compare/master...fred-wang:MATH" title="" class="ltx_ref">import the OpenType MATH parsing code from WebKit</a>. However, after discussions
with some Google developers,
it seems that the best option is to directly add support
for this table in HarfBuzz. Since this library is used by Gecko, by WebKit
(at least the GTK port) and by many other applications such as Servo, XeTeX or
LibreOffice it make senses to share the implementation to improve math rendering
everywhere.</p>
</div>
<div id="p6" class="ltx_para">
<p class="ltx_p">The idea for HarfBuzz is to add an API to</p>
<ol id="I3" class="ltx_enumerate">
<li id="I3.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">1.</span> 
<div id="I3.i1.p1" class="ltx_para">
<p class="ltx_p">Expose data from the <span class="ltx_text ltx_font_typewriter">MathConstants</span> and <span class="ltx_text ltx_font_typewriter">MathGlyphInfo</span>.</p>
</div>
</li>
<li id="I3.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">2.</span> 
<div id="I3.i2.p1" class="ltx_para">
<p class="ltx_p">Shape stretchy operators to some target size with the help of the
<span class="ltx_text ltx_font_typewriter">MathVariants</span>.</p>
</div>
</li>
</ol>
<p class="ltx_p">It is then up to a higher-level math rendering engine
(e.g. TeX or MathML rendering engines) to beautifully display mathematical
formulas using this API. The design choice for exposing <span class="ltx_text ltx_font_typewriter">MathConstants</span> and
<span class="ltx_text ltx_font_typewriter">MathGlyphInfo</span> is almost obvious from the reading of the MATH table
specification. The choice for the shaping API is a bit more complex and
discussions is still in progress. For example because we want to accept
stretching after glyph-level mirroring (e.g. to draw RTL clockwise integrals) we
should accept any glyph and not just an input Unicode strings as it is the case
for other HarfBuzz shaping functions. This shaping also depends on a stretching
direction (horizontal/vertical) or on a target size (and Gecko even currently
has various ways to approximate that target size). Finally,
we should also have a way to expose italic correction for a glyph assembly
or to approximate preferred width for Web rendering engines.</p>
</div>
<div id="p7" class="ltx_para">
<p class="ltx_p">As I mentioned at the beginning, the data and algorithm to build glyph assembly
is the most complex part of the OpenType MATH and deserves a special interest.
The idea is that you have a list of <math id="p7.m1" class="ltx_Math" alttext="n\geq 1" display="inline"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n\geq 1</annotation></semantics></math> glyphs available to build
the assembly. For each
<math id="p7.m2" class="ltx_Math" alttext="0\leq i\leq n-1" display="inline"><semantics><mrow><mn>0</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">0\leq i\leq n-1</annotation></semantics></math>,
the glyph <math id="p7.m3" class="ltx_Math" alttext="g_{i}" display="inline"><semantics><msub><mi>g</mi><mi>i</mi></msub><annotation encoding="application/x-tex">g_{i}</annotation></semantics></math> has advance <math id="p7.m4" class="ltx_Math" alttext="a_{i}" display="inline"><semantics><msub><mi>a</mi><mi>i</mi></msub><annotation encoding="application/x-tex">a_{i}</annotation></semantics></math> in the stretch direction. Each <math id="p7.m5" class="ltx_Math" alttext="g_{i}" display="inline"><semantics><msub><mi>g</mi><mi>i</mi></msub><annotation encoding="application/x-tex">g_{i}</annotation></semantics></math> has
straight connector part at its start (of length <math id="p7.m6" class="ltx_Math" alttext="s_{i}" display="inline"><semantics><msub><mi>s</mi><mi>i</mi></msub><annotation encoding="application/x-tex">s_{i}</annotation></semantics></math>) and at its end
(of length <math id="p7.m7" class="ltx_Math" alttext="e_{i}" display="inline"><semantics><msub><mi>e</mi><mi>i</mi></msub><annotation encoding="application/x-tex">e_{i}</annotation></semantics></math>) so that we can align the glyphs on the stretch axis and glue
them together. Also, some of the glyphs are “extenders” which means that
they can be repeated 0, 1 or more times to make the assembly as large as
possible. Finally,
the end/start connectors of consecutive glyphs must overlap by at least a fixed
value <math id="p7.m8" class="ltx_Math" alttext="o_{\mathrm{min}}" display="inline"><semantics><msub><mi>o</mi><mi>min</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{min}}</annotation></semantics></math> to avoid gaps at some resolutions but of course without
exceeding the length of the corresponding connectors. This gives some
flexibility to adjust the size of the assembly and get closer to the target
size <math id="p7.m9" class="ltx_Math" alttext="t" display="inline"><semantics><mi>t</mi><annotation encoding="application/x-tex">t</annotation></semantics></math>.</p>
</div>
<figure id="S0.F1" class="ltx_figure"><svg id="S0.F1.pic1" class="ltx_picture ltx_centering" height="294.73" overflow="visible" version="1.1" viewBox="-4.43 -232.91 450.39 294.73" width="450.39"><g transform="matrix(1 0 0 -1 0 -171.09)"><g stroke="#000000"><g fill="#000000"><g stroke-width="0.4pt" color="#000000"><g stroke="#0000FF"><g fill="#0000FF"><g stroke="#E6E6FF" color="#0000FF"><g fill="#E6E6FF"><path d="M 59.06 59.06 L 177.17 59.06 L 177.17 -59.06 L 59.06 -59.06 Z M 0 2.95 L 59.06 2.95 L 59.06 -2.95 L 0 -2.95 Z M 177.17 2.95 L 236.22 2.95 L 236.22 -2.95 L 177.17 -2.95 Z" style="stroke:none"></path></g></g><path d="M 118.11 0" style="fill:none"></path><g transform="matrix(1 0 0 1 110.02 -2.71)" color="#0000FF"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#0000FF" height="100%" overflow="visible" width="16.19">
<p class="ltx_p"><math id="S0.F1.pic1.m1" class="ltx_Math" alttext="g_{i}" display="inline"><semantics><msub><mi>g</mi><mi>i</mi></msub><annotation encoding="application/x-tex">g_{i}</annotation></semantics></math></p></foreignObject></switch></g></g><g stroke-width="0.32pt" color="#0000FF"><g stroke-dasharray="none" stroke-dashoffset="0.0pt"><g stroke-linecap="round"><g stroke-linejoin="round"></g></g></g></g><path d="M 0.64 -88.58 L 29.53 -88.58 L 58.42 -88.58" style="fill:none"></path><g transform="matrix(-1 0 0 -1 0.64 -88.58)" color="#0000FF"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 58.42 -88.58)" color="#0000FF"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 21.43 -103.16)" color="#0000FF"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#0000FF" height="100%" overflow="visible" width="16.19">
<p class="ltx_p"><math id="S0.F1.pic1.m2" class="ltx_Math" alttext="s_{i}" display="inline"><semantics><msub><mi>s</mi><mi>i</mi></msub><annotation encoding="application/x-tex">s_{i}</annotation></semantics></math></p></foreignObject></switch></g></g><path d="M 177.8 -88.58 L 206.69 -88.58 L 235.58 -88.58" style="fill:none"></path><g transform="matrix(-1 0 0 -1 177.8 -88.58)" color="#0000FF"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 235.58 -88.58)" color="#0000FF"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 198.6 -103.16)" color="#0000FF"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#0000FF" height="100%" overflow="visible" width="16.19">
<p class="ltx_p"><math id="S0.F1.pic1.m3" class="ltx_Math" alttext="e_{i}" display="inline"><semantics><msub><mi>e</mi><mi>i</mi></msub><annotation encoding="application/x-tex">e_{i}</annotation></semantics></math></p></foreignObject></switch></g></g><path d="M 0.64 -177.17 L 118.11 -177.17 L 235.58 -177.17" style="fill:none"></path><g transform="matrix(-1 0 0 -1 0.64 -177.17)" color="#0000FF"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 235.58 -177.17)" color="#0000FF"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 110.02 -191.74)" color="#0000FF"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#0000FF" height="100%" overflow="visible" width="16.19">
<p class="ltx_p"><math id="S0.F1.pic1.m4" class="ltx_Math" alttext="a_{i}" display="inline"><semantics><msub><mi>a</mi><mi>i</mi></msub><annotation encoding="application/x-tex">a_{i}</annotation></semantics></math></p></foreignObject></switch></g></g></g></g><g stroke="#FF0000"><g fill="#FF0000"><g stroke="#FFE6E6" color="#FF0000"><g fill="#FFE6E6"><path d="M 265.75 29.53 L 383.86 29.53 L 383.86 -88.58 L 265.75 -88.58 Z M 206.69 -26.57 L 265.75 -26.57 L 265.75 -32.48 L 206.69 -32.48 Z M 383.86 -26.57 L 442.91 -26.57 L 442.91 -32.48 L 383.86 -32.48 Z" style="stroke:none"></path></g></g><path d="M 324.8 -29.53" style="fill:none"></path><g transform="matrix(1 0 0 1 310.9 -32.24)" color="#FF0000"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#FF0000" height="100%" overflow="visible" width="27.81">
<p class="ltx_p"><math id="S0.F1.pic1.m5" class="ltx_Math" alttext="g_{i+1}" display="inline"><semantics><msub><mi>g</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">g_{i+1}</annotation></semantics></math></p></foreignObject></switch></g></g><path d="M 207.33 -118.11 L 236.22 -118.11 L 265.11 -118.11" style="fill:none"></path><g transform="matrix(-1 0 0 -1 207.33 -118.11)" color="#FF0000"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 265.11 -118.11)" color="#FF0000"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 222.31 -132.68)" color="#FF0000"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#FF0000" height="100%" overflow="visible" width="27.81">
<p class="ltx_p"><math id="S0.F1.pic1.m6" class="ltx_Math" alttext="s_{i+1}" display="inline"><semantics><msub><mi>s</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">s_{i+1}</annotation></semantics></math></p></foreignObject></switch></g></g><path d="M 384.49 -118.11 L 413.39 -118.11 L 442.28 -118.11" style="fill:none"></path><g transform="matrix(-1 0 0 -1 384.49 -118.11)" color="#FF0000"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 442.28 -118.11)" color="#FF0000"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 399.48 -132.68)" color="#FF0000"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#FF0000" height="100%" overflow="visible" width="27.81">
<p class="ltx_p"><math id="S0.F1.pic1.m7" class="ltx_Math" alttext="e_{i+1}" display="inline"><semantics><msub><mi>e</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">e_{i+1}</annotation></semantics></math></p></foreignObject></switch></g></g><path d="M 207.33 -206.69 L 324.8 -206.69 L 442.28 -206.69" style="fill:none"></path><g transform="matrix(-1 0 0 -1 207.33 -206.69)" color="#FF0000"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 442.28 -206.69)" color="#FF0000"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 310.9 -221.27)" color="#FF0000"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#FF0000" height="100%" overflow="visible" width="27.81">
<p class="ltx_p"><math id="S0.F1.pic1.m8" class="ltx_Math" alttext="a_{i+1}" display="inline"><semantics><msub><mi>a</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">a_{i+1}</annotation></semantics></math></p></foreignObject></switch></g></g></g></g><path d="M 207.33 -14.76 L 221.46 -14.76 L 235.58 -14.76" style="fill:none"></path><g transform="matrix(-1 0 0 -1 207.33 -14.76)"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 235.58 -14.76)"><path d="M -1.66 2.21 C -1.52 1.38 0 0.14 0.42 0 C 0 -0.14 -1.52 -1.38 -1.66 -2.21" style="fill:none"></path></g><g transform="matrix(1 0 0 1 201.74 -29.34)"><g class="ltx_svg_fog" transform="matrix(1 0 0 -1 0 12.45)"><switch><foreignObject color="#000000" height="100%" overflow="visible" width="39.43">
<p class="ltx_p"><math id="S0.F1.pic1.m9" class="ltx_Math" alttext="o_{i,i+1}" display="inline"><semantics><msub><mi>o</mi><mrow><mi>i</mi><mo>,</mo><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></mrow></msub><annotation encoding="application/x-tex">o_{i,i+1}</annotation></semantics></math></p></foreignObject></switch></g></g></g></g></g></g></svg>
<figcaption class="ltx_caption ltx_centering"><span class="ltx_tag ltx_tag_figure">Figure 1: </span>Two adjacent glyphs in an assembly</figcaption>
</figure>
<div id="p8" class="ltx_para">
<p class="ltx_p">To ensure that the width/height is distributed equally and the symmetry of the
shape is preserved, the MATH table specification suggests the following iterative
algorithm to determine the number of extenders and the connector overlaps
to reach a minimal target size <math id="p8.m1" class="ltx_Math" alttext="t" display="inline"><semantics><mi>t</mi><annotation encoding="application/x-tex">t</annotation></semantics></math>:</p>
</div>
<div id="p9" class="ltx_para">
<ol id="I4" class="ltx_enumerate">
<li id="I4.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">1.</span></span> 
<div id="I4.i1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Assemble all parts by overlapping connectors by maximum amount, and
removing all extenders. This gives the smallest possible result.</span></p>
</div>
</li>
<li id="I4.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">2.</span></span> 
<div id="I4.i2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Determine how much extra width/height can be distributed into all
connections between neighboring parts. If that is enough to achieve the size
goal, extend each connection equally by changing overlaps of connectors to
finish the job.</span></p>
</div>
</li>
<li id="I4.i3" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">3.</span></span> 
<div id="I4.i3.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">If all connections have been extended to minimum overlap and further
growth is needed, add one of each extender, and repeat the process from the
first step.</span></p>
</div>
</li>
</ol>
</div>
<div id="p10" class="ltx_para">
<p class="ltx_p">We note that at each step, each extender is repeated the same number of times
<math id="p10.m1" class="ltx_Math" alttext="r\geq 0" display="inline"><semantics><mrow><mi>r</mi><mo>≥</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">r\geq 0</annotation></semantics></math>. So if <math id="p10.m2" class="ltx_Math" alttext="I_{\mathrm{Ext}}" display="inline"><semantics><msub><mi>I</mi><mi>Ext</mi></msub><annotation encoding="application/x-tex">I_{\mathrm{Ext}}</annotation></semantics></math> (respectively <math id="p10.m3" class="ltx_Math" alttext="I_{\mathrm{NonExt}}" display="inline"><semantics><msub><mi>I</mi><mi>NonExt</mi></msub><annotation encoding="application/x-tex">I_{\mathrm{NonExt}}</annotation></semantics></math>) is the set of
indices <math id="p10.m4" class="ltx_Math" alttext="0\leq i\leq n-1" display="inline"><semantics><mrow><mn>0</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">0\leq i\leq n-1</annotation></semantics></math> such that <math id="p10.m5" class="ltx_Math" alttext="g_{i}" display="inline"><semantics><msub><mi>g</mi><mi>i</mi></msub><annotation encoding="application/x-tex">g_{i}</annotation></semantics></math> is an extender
(respectively is not
an extender) we have <math id="p10.m6" class="ltx_Math" alttext="r_{i}=r" display="inline"><semantics><mrow><msub><mi>r</mi><mi>i</mi></msub><mo>=</mo><mi>r</mi></mrow><annotation encoding="application/x-tex">r_{i}=r</annotation></semantics></math> (respectively <math id="p10.m7" class="ltx_Math" alttext="r_{i}=1" display="inline"><semantics><mrow><msub><mi>r</mi><mi>i</mi></msub><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">r_{i}=1</annotation></semantics></math>). The size we can reach
at step <math id="p10.m8" class="ltx_Math" alttext="r" display="inline"><semantics><mi>r</mi><annotation encoding="application/x-tex">r</annotation></semantics></math> is at most the one obtained with the minimal connector overlap
<math id="p10.m9" class="ltx_Math" alttext="o_{\mathrm{min}}" display="inline"><semantics><msub><mi>o</mi><mi>min</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{min}}</annotation></semantics></math> that is
</p>
<table id="S0.Ex2" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex2.m1" class="ltx_Math" alttext="\sum_{i=0}^{N-1}\left(\sum_{j=1}^{r_{i}}{a_{i}-o_{\mathrm{min}}}\right)+o_{
\mathrm{min}}=\left(\sum_{i\in I_{\mathrm{NonExt}}}{a_{i}-o_{\mathrm{min}}}
\right)+\left(\sum_{i\in I_{\mathrm{Ext}}}r{(a_{i}-o_{\mathrm{min}})}\right)+o%
_{\mathrm{min}}" display="block"><semantics><mrow><mrow><mrow><munderover><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>i</mi><mo>=</mo><mn>0</mn></mrow><mrow><mi>N</mi><mo>-</mo><mn>1</mn></mrow></munderover><mrow><mo>(</mo><mrow><mrow><munderover><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>j</mi><mo>=</mo><mn>1</mn></mrow><msub><mi>r</mi><mi>i</mi></msub></munderover><msub><mi>a</mi><mi>i</mi></msub></mrow><mo>-</mo><msub><mi>o</mi><mi>min</mi></msub></mrow><mo>)</mo></mrow></mrow><mo>+</mo><msub><mi>o</mi><mi>min</mi></msub></mrow><mo>=</mo><mrow><mrow><mo>(</mo><mrow><mrow><munder><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>i</mi><mo>∈</mo><msub><mi>I</mi><mi>NonExt</mi></msub></mrow></munder><msub><mi>a</mi><mi>i</mi></msub></mrow><mo>-</mo><msub><mi>o</mi><mi>min</mi></msub></mrow><mo>)</mo></mrow><mo>+</mo><mrow><mo>(</mo><mrow><munder><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>i</mi><mo>∈</mo><msub><mi>I</mi><mi>Ext</mi></msub></mrow></munder><mrow><mi>r</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><msub><mi>a</mi><mi>i</mi></msub><mo>-</mo><msub><mi>o</mi><mi>min</mi></msub></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>)</mo></mrow><mo>+</mo><msub><mi>o</mi><mi>min</mi></msub></mrow></mrow><annotation encoding="application/x-tex">\sum_{i=0}^{N-1}\left(\sum_{j=1}^{r_{i}}{a_{i}-o_{\mathrm{min}}}\right)+o_{
\mathrm{min}}=\left(\sum_{i\in I_{\mathrm{NonExt}}}{a_{i}-o_{\mathrm{min}}}
\right)+\left(\sum_{i\in I_{\mathrm{Ext}}}r{(a_{i}-o_{\mathrm{min}})}\right)+o%
_{\mathrm{min}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p11" class="ltx_para">
<p class="ltx_p">We let <math id="p11.m1" class="ltx_Math" alttext="N_{\mathrm{Ext}}={|I_{\mathrm{Ext}}|}" display="inline"><semantics><mrow><msub><mi>N</mi><mi>Ext</mi></msub><mo>=</mo><mrow><mo stretchy="false">|</mo><msub><mi>I</mi><mi>Ext</mi></msub><mo stretchy="false">|</mo></mrow></mrow><annotation encoding="application/x-tex">N_{\mathrm{Ext}}={|I_{\mathrm{Ext}}|}</annotation></semantics></math> and
<math id="p11.m2" class="ltx_Math" alttext="N_{\mathrm{NonExt}}={|I_{\mathrm{NonExt}}|}" display="inline"><semantics><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>=</mo><mrow><mo stretchy="false">|</mo><msub><mi>I</mi><mi>NonExt</mi></msub><mo stretchy="false">|</mo></mrow></mrow><annotation encoding="application/x-tex">N_{\mathrm{NonExt}}={|I_{\mathrm{NonExt}}|}</annotation></semantics></math> be the number of extenders and
non-extenders. We also let
<math id="p11.m3" class="ltx_Math" alttext="S_{\mathrm{Ext}}=\sum_{i\in I_{\mathrm{Ext}}}a_{i}" display="inline"><semantics><mrow><msub><mi>S</mi><mi>Ext</mi></msub><mo>=</mo><mrow><msub><mo largeop="true" symmetric="true">∑</mo><mrow><mi>i</mi><mo>∈</mo><msub><mi>I</mi><mi>Ext</mi></msub></mrow></msub><msub><mi>a</mi><mi>i</mi></msub></mrow></mrow><annotation encoding="application/x-tex">S_{\mathrm{Ext}}=\sum_{i\in I_{\mathrm{Ext}}}a_{i}</annotation></semantics></math> and
<math id="p11.m4" class="ltx_Math" alttext="S_{\mathrm{NonExt}}=\sum_{i\in I_{\mathrm{NonExt}}}a_{i}" display="inline"><semantics><mrow><msub><mi>S</mi><mi>NonExt</mi></msub><mo>=</mo><mrow><msub><mo largeop="true" symmetric="true">∑</mo><mrow><mi>i</mi><mo>∈</mo><msub><mi>I</mi><mi>NonExt</mi></msub></mrow></msub><msub><mi>a</mi><mi>i</mi></msub></mrow></mrow><annotation encoding="application/x-tex">S_{\mathrm{NonExt}}=\sum_{i\in I_{\mathrm{NonExt}}}a_{i}</annotation></semantics></math> be the sum of advances
for extenders and non-extenders. If we want the advance of the glyph assembly
to reach the minimal size <math id="p11.m5" class="ltx_Math" alttext="t" display="inline"><semantics><mi>t</mi><annotation encoding="application/x-tex">t</annotation></semantics></math> then
</p>
<table id="S0.Ex3" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex3.m1" class="ltx_Math" alttext="{S_{\mathrm{NonExt}}-o_{\mathrm{min}}\left(N_{\mathrm{NonExt}}-1\right)}+{r%
\left(S_{\mathrm{Ext}}-o_{\mathrm{min}}N_{\mathrm{Ext}}\right)}\geq t" display="block"><semantics><mrow><mrow><mrow><msub><mi>S</mi><mi>NonExt</mi></msub><mo>-</mo><mrow><msub><mi>o</mi><mi>min</mi></msub><mo>⁢</mo><mrow><mo>(</mo><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>-</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow></mrow><mo>+</mo><mrow><mi>r</mi><mo>⁢</mo><mrow><mo>(</mo><mrow><msub><mi>S</mi><mi>Ext</mi></msub><mo>-</mo><mrow><msub><mi>o</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>)</mo></mrow></mrow></mrow><mo>≥</mo><mi>t</mi></mrow><annotation encoding="application/x-tex">{S_{\mathrm{NonExt}}-o_{\mathrm{min}}\left(N_{\mathrm{NonExt}}-1\right)}+{r%
\left(S_{\mathrm{Ext}}-o_{\mathrm{min}}N_{\mathrm{Ext}}\right)}\geq t</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p12" class="ltx_para">
<p class="ltx_p">We can assume <math id="p12.m1" class="ltx_Math" alttext="S_{\mathrm{Ext}}-o_{\mathrm{min}}N_{\mathrm{Ext}}&gt;0" display="inline"><semantics><mrow><mrow><msub><mi>S</mi><mi>Ext</mi></msub><mo>-</mo><mrow><msub><mi>o</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>&gt;</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">S_{\mathrm{Ext}}-o_{\mathrm{min}}N_{\mathrm{Ext}}&gt;0</annotation></semantics></math> or otherwise we
would have the extreme case where the overlap takes at least the full
advance of each extender. Then we obtain
</p>
<table id="S0.Ex4" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex4.m1" class="ltx_Math" alttext="r\geq r_{\mathrm{min}}=\max\left(0,\left\lceil\frac{t-{S_{\mathrm{NonExt}}+o_{
\mathrm{min}}\left(N_{\mathrm{NonExt}}-1\right)}}{S_{\mathrm{Ext}}-o_{\mathrm{
min}}N_{\mathrm{Ext}}}\right\rceil\right)" display="block"><semantics><mrow><mi>r</mi><mo>≥</mo><msub><mi>r</mi><mi>min</mi></msub><mo>=</mo><mrow><mi>max</mi><mo>⁡</mo><mrow><mo>(</mo><mn>0</mn><mo>,</mo><mrow><mo>⌈</mo><mfrac><mrow><mrow><mi>t</mi><mo>-</mo><msub><mi>S</mi><mi>NonExt</mi></msub></mrow><mo>+</mo><mrow><msub><mi>o</mi><mi>min</mi></msub><mo>⁢</mo><mrow><mo>(</mo><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>-</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow></mrow><mrow><msub><mi>S</mi><mi>Ext</mi></msub><mo>-</mo><mrow><msub><mi>o</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow></mfrac><mo>⌉</mo></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">r\geq r_{\mathrm{min}}=\max\left(0,\left\lceil\frac{t-{S_{\mathrm{NonExt}}+o_{
\mathrm{min}}\left(N_{\mathrm{NonExt}}-1\right)}}{S_{\mathrm{Ext}}-o_{\mathrm{
min}}N_{\mathrm{Ext}}}\right\rceil\right)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p13" class="ltx_para">
<p class="ltx_p">This provides a first simplification of the algorithm sketched in the
MATH table specification:
Directly start iteration at step <math id="p13.m1" class="ltx_Math" alttext="r_{\mathrm{min}}" display="inline"><semantics><msub><mi>r</mi><mi>min</mi></msub><annotation encoding="application/x-tex">r_{\mathrm{min}}</annotation></semantics></math>. Note that at each step we
start at <em class="ltx_emph">possibly different</em> maximum overlaps and decrease all of them
by a same value. It is not clear what to do when one of the overlap reaches
<math id="p13.m2" class="ltx_Math" alttext="o_{\mathrm{min}}" display="inline"><semantics><msub><mi>o</mi><mi>min</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{min}}</annotation></semantics></math> while others can still be decreased. However, the sketched
algorithm says all the connectors should reach minimum overlap before
the next increment of <math id="p13.m3" class="ltx_Math" alttext="r" display="inline"><semantics><mi>r</mi><annotation encoding="application/x-tex">r</annotation></semantics></math>,
which means the target size will indeed be reached at step <math id="p13.m4" class="ltx_Math" alttext="r_{\mathrm{min}}" display="inline"><semantics><msub><mi>r</mi><mi>min</mi></msub><annotation encoding="application/x-tex">r_{\mathrm{min}}</annotation></semantics></math>.</p>
</div>
<div id="p14" class="ltx_para">
<p class="ltx_p">One possible interpretation is to stop overlap decreasing for the adjacent
connectors that reached minimum overlap
and to continue uniform decreasing for the others until
all the connectors reach minimum overlap. In that case we may lose equal
distribution or symmetry. In practice, this should probably not matter much.
So we propose instead the dual option which should behave more or less the
same in most cases: Start with all overlaps set to <math id="p14.m1" class="ltx_Math" alttext="o_{\mathrm{min}}" display="inline"><semantics><msub><mi>o</mi><mi>min</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{min}}</annotation></semantics></math> and increase
them evenly to reach a same value <math id="p14.m2" class="ltx_Math" alttext="o" display="inline"><semantics><mi>o</mi><annotation encoding="application/x-tex">o</annotation></semantics></math>. By the same reasoning as above we want
the inequality
</p>
<table id="S0.Ex5" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex5.m1" class="ltx_Math" alttext="{S_{\mathrm{NonExt}}-o\left(N_{\mathrm{NonExt}}-1\right)}+{r_{\mathrm{min}}
\left(S_{\mathrm{Ext}}-oN_{\mathrm{Ext}}\right)}\geq t" display="block"><semantics><mrow><mrow><mrow><msub><mi>S</mi><mi>NonExt</mi></msub><mo>-</mo><mrow><mi>o</mi><mo>⁢</mo><mrow><mo>(</mo><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>-</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow></mrow><mo>+</mo><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>⁢</mo><mrow><mo>(</mo><mrow><msub><mi>S</mi><mi>Ext</mi></msub><mo>-</mo><mrow><mi>o</mi><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>)</mo></mrow></mrow></mrow><mo>≥</mo><mi>t</mi></mrow><annotation encoding="application/x-tex">{S_{\mathrm{NonExt}}-o\left(N_{\mathrm{NonExt}}-1\right)}+{r_{\mathrm{min}}
\left(S_{\mathrm{Ext}}-oN_{\mathrm{Ext}}\right)}\geq t</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">which can be rewritten
</p>
<table id="S0.Ex6" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex6.m1" class="ltx_Math" alttext="S_{\mathrm{NonExt}}+r_{\mathrm{min}}S_{\mathrm{Ext}}-{o\left(N_{\mathrm{NonExt%
}}+{r_{\mathrm{min}}N_{\mathrm{Ext}}}-1\right)}\geq t" display="block"><semantics><mrow><mrow><mrow><msub><mi>S</mi><mi>NonExt</mi></msub><mo>+</mo><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>S</mi><mi>Ext</mi></msub></mrow></mrow><mo>-</mo><mrow><mi>o</mi><mo>⁢</mo><mrow><mo>(</mo><mrow><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>+</mo><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>-</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow></mrow><mo>≥</mo><mi>t</mi></mrow><annotation encoding="application/x-tex">S_{\mathrm{NonExt}}+r_{\mathrm{min}}S_{\mathrm{Ext}}-{o\left(N_{\mathrm{NonExt%
}}+{r_{\mathrm{min}}N_{\mathrm{Ext}}}-1\right)}\geq t</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p15" class="ltx_para">
<p class="ltx_p">We note that <math id="p15.m1" class="ltx_Math" alttext="N=N_{\mathrm{NonExt}}+{r_{\mathrm{min}}N_{\mathrm{Ext}}}" display="inline"><semantics><mrow><mi>N</mi><mo>=</mo><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>+</mo><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow></mrow><annotation encoding="application/x-tex">N=N_{\mathrm{NonExt}}+{r_{\mathrm{min}}N_{\mathrm{Ext}}}</annotation></semantics></math> is just the exact
number of glyphs used in the assembly. If there is only a single glyph, then the
overlap value is irrelevant so we can assume
<math id="p15.m2" class="ltx_Math" alttext="N_{\mathrm{NonExt}}+{rN_{\mathrm{Ext}}}-1=N-1\geq 1" display="inline"><semantics><mrow><mrow><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>+</mo><mrow><mi>r</mi><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>-</mo><mn>1</mn></mrow><mo>=</mo><mrow><mi>N</mi><mo>-</mo><mn>1</mn></mrow><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">N_{\mathrm{NonExt}}+{rN_{\mathrm{Ext}}}-1=N-1\geq 1</annotation></semantics></math>. This provides the
greatest theorical value for the overlap <math id="p15.m3" class="ltx_Math" alttext="o" display="inline"><semantics><mi>o</mi><annotation encoding="application/x-tex">o</annotation></semantics></math>:
</p>
<table id="S0.Ex7" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex7.m1" class="ltx_Math" alttext="o_{\mathrm{min}}\leq o\leq o_{\mathrm{max}}^{\mathrm{theorical}}=\frac{S_{
\mathrm{NonExt}}+r_{\mathrm{min}}S_{\mathrm{Ext}}-t}{N_{\mathrm{NonExt}}+{r_{
\mathrm{min}}N_{\mathrm{Ext}}}-1}" display="block"><semantics><mrow><msub><mi>o</mi><mi>min</mi></msub><mo>≤</mo><mi>o</mi><mo>≤</mo><msubsup><mi>o</mi><mi>max</mi><mi>theorical</mi></msubsup><mo>=</mo><mfrac><mrow><mrow><msub><mi>S</mi><mi>NonExt</mi></msub><mo>+</mo><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>S</mi><mi>Ext</mi></msub></mrow></mrow><mo>-</mo><mi>t</mi></mrow><mrow><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>+</mo><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>-</mo><mn>1</mn></mrow></mfrac></mrow><annotation encoding="application/x-tex">o_{\mathrm{min}}\leq o\leq o_{\mathrm{max}}^{\mathrm{theorical}}=\frac{S_{
\mathrm{NonExt}}+r_{\mathrm{min}}S_{\mathrm{Ext}}-t}{N_{\mathrm{NonExt}}+{r_{
\mathrm{min}}N_{\mathrm{Ext}}}-1}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p16" class="ltx_para">
<p class="ltx_p">Of course, we also have to take into account the limit imposed by the start and
end connector lengths. So <math id="p16.m1" class="ltx_Math" alttext="o_{\mathrm{max}}" display="inline"><semantics><msub><mi>o</mi><mi>max</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{max}}</annotation></semantics></math> must also be at most
<math id="p16.m2" class="ltx_Math" alttext="\min{(e_{i},s_{i+1})}" display="inline"><semantics><mrow><mi>min</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>e</mi><mi>i</mi></msub><mo>,</mo><msub><mi>s</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\min{(e_{i},s_{i+1})}</annotation></semantics></math> for <math id="p16.m3" class="ltx_Math" alttext="0\leq i\leq n-2" display="inline"><semantics><mrow><mn>0</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mrow><mi>n</mi><mo>-</mo><mn>2</mn></mrow></mrow><annotation encoding="application/x-tex">0\leq i\leq n-2</annotation></semantics></math>. But if <math id="p16.m4" class="ltx_Math" alttext="r_{\mathrm{min}}\geq 2" display="inline"><semantics><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>≥</mo><mn>2</mn></mrow><annotation encoding="application/x-tex">r_{\mathrm{min}}\geq 2</annotation></semantics></math>
then extender copies are connected and so <math id="p16.m5" class="ltx_Math" alttext="o_{\mathrm{max}}" display="inline"><semantics><msub><mi>o</mi><mi>max</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{max}}</annotation></semantics></math> must also be at most
<math id="p16.m6" class="ltx_Math" alttext="\min{(e_{i},s_{i})}" display="inline"><semantics><mrow><mi>min</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>e</mi><mi>i</mi></msub><mo>,</mo><msub><mi>s</mi><mi>i</mi></msub><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\min{(e_{i},s_{i})}</annotation></semantics></math> for <math id="p16.m7" class="ltx_Math" alttext="i\in I_{\mathrm{Ext}}" display="inline"><semantics><mrow><mi>i</mi><mo>∈</mo><msub><mi>I</mi><mi>Ext</mi></msub></mrow><annotation encoding="application/x-tex">i\in I_{\mathrm{Ext}}</annotation></semantics></math>. To summarize, <math id="p16.m8" class="ltx_Math" alttext="o_{\mathrm{max}}" display="inline"><semantics><msub><mi>o</mi><mi>max</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{max}}</annotation></semantics></math> is
the minimum of <math id="p16.m9" class="ltx_Math" alttext="o_{\mathrm{max}}^{\mathrm{theorical}}" display="inline"><semantics><msubsup><mi>o</mi><mi>max</mi><mi>theorical</mi></msubsup><annotation encoding="application/x-tex">o_{\mathrm{max}}^{\mathrm{theorical}}</annotation></semantics></math>, of <math id="p16.m10" class="ltx_Math" alttext="e_{i}" display="inline"><semantics><msub><mi>e</mi><mi>i</mi></msub><annotation encoding="application/x-tex">e_{i}</annotation></semantics></math> for <math id="p16.m11" class="ltx_Math" alttext="0\leq i\leq n-2" display="inline"><semantics><mrow><mn>0</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mrow><mi>n</mi><mo>-</mo><mn>2</mn></mrow></mrow><annotation encoding="application/x-tex">0\leq i\leq n-2</annotation></semantics></math>,
of <math id="p16.m12" class="ltx_Math" alttext="s_{i}" display="inline"><semantics><msub><mi>s</mi><mi>i</mi></msub><annotation encoding="application/x-tex">s_{i}</annotation></semantics></math> <math id="p16.m13" class="ltx_Math" alttext="1\leq i\leq n-1" display="inline"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">1\leq i\leq n-1</annotation></semantics></math> and possibly of <math id="p16.m14" class="ltx_Math" alttext="e_{0}" display="inline"><semantics><msub><mi>e</mi><mn>0</mn></msub><annotation encoding="application/x-tex">e_{0}</annotation></semantics></math> (if <math id="p16.m15" class="ltx_Math" alttext="0\in I_{\mathrm{Ext}}" display="inline"><semantics><mrow><mn>0</mn><mo>∈</mo><msub><mi>I</mi><mi>Ext</mi></msub></mrow><annotation encoding="application/x-tex">0\in I_{\mathrm{Ext}}</annotation></semantics></math>)
and of of <math id="p16.m16" class="ltx_Math" alttext="s_{n-1}" display="inline"><semantics><msub><mi>s</mi><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">s_{n-1}</annotation></semantics></math> (if <math id="p16.m17" class="ltx_Math" alttext="{n-1}\in I_{\mathrm{Ext}}" display="inline"><semantics><mrow><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><mo>∈</mo><msub><mi>I</mi><mi>Ext</mi></msub></mrow><annotation encoding="application/x-tex">{n-1}\in I_{\mathrm{Ext}}</annotation></semantics></math>).</p>
</div>
<div id="p17" class="ltx_para">
<p class="ltx_p">With the algorithm described above
<math id="p17.m1" class="ltx_Math" alttext="N_{\mathrm{Ext}}" display="inline"><semantics><msub><mi>N</mi><mi>Ext</mi></msub><annotation encoding="application/x-tex">N_{\mathrm{Ext}}</annotation></semantics></math>, <math id="p17.m2" class="ltx_Math" alttext="N_{\mathrm{NonExt}}" display="inline"><semantics><msub><mi>N</mi><mi>NonExt</mi></msub><annotation encoding="application/x-tex">N_{\mathrm{NonExt}}</annotation></semantics></math>, <math id="p17.m3" class="ltx_Math" alttext="S_{\mathrm{Ext}}" display="inline"><semantics><msub><mi>S</mi><mi>Ext</mi></msub><annotation encoding="application/x-tex">S_{\mathrm{Ext}}</annotation></semantics></math>, <math id="p17.m4" class="ltx_Math" alttext="S_{\mathrm{NonExt}}" display="inline"><semantics><msub><mi>S</mi><mi>NonExt</mi></msub><annotation encoding="application/x-tex">S_{\mathrm{NonExt}}</annotation></semantics></math>
and <math id="p17.m5" class="ltx_Math" alttext="r_{\mathrm{min}}" display="inline"><semantics><msub><mi>r</mi><mi>min</mi></msub><annotation encoding="application/x-tex">r_{\mathrm{min}}</annotation></semantics></math> and <math id="p17.m6" class="ltx_Math" alttext="o_{\mathrm{max}}" display="inline"><semantics><msub><mi>o</mi><mi>max</mi></msub><annotation encoding="application/x-tex">o_{\mathrm{max}}</annotation></semantics></math> can all be obtained using simple loops
on the glyphs <math id="p17.m7" class="ltx_Math" alttext="g_{i}" display="inline"><semantics><msub><mi>g</mi><mi>i</mi></msub><annotation encoding="application/x-tex">g_{i}</annotation></semantics></math>
and so the complexity is <math id="p17.m8" class="ltx_Math" alttext="O(n)" display="inline"><semantics><mrow><mi>O</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">O(n)</annotation></semantics></math>. In practice <math id="p17.m9" class="ltx_Math" alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math> is small: For
existing fonts, assemblies are made of at most three non-extenders and two extenders that is
<math id="p17.m10" class="ltx_Math" alttext="n\leq 5" display="inline"><semantics><mrow><mi>n</mi><mo>≤</mo><mn>5</mn></mrow><annotation encoding="application/x-tex">n\leq 5</annotation></semantics></math> (incidentally, Gecko and WebKit do not currently support larger values of <math id="p17.m11" class="ltx_Math" alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math>).
This means that all the operations described above can be considered to have
constant complexity. This is much better than a naive implementation of the
iterative algorithm sketched in the OpenType MATH table specification which
seems to require at worst
</p>
<table id="S0.Ex8" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex8.m1" class="ltx_Math" alttext="\sum_{r=0}^{r_{\mathrm{min}}-1}{N_{\mathrm{NonExt}}+rN_{\mathrm{Ext}}}=N_{
\mathrm{NonExt}}r_{\mathrm{min}}+\frac{r_{\mathrm{min}}\left(r_{\mathrm{min}}-%
1\right)}{2}N_{\mathrm{Ext}}={O(n\times r_{\mathrm{min}}^{2})}" display="block"><semantics><mrow><mrow><mrow><munderover><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>r</mi><mo>=</mo><mn>0</mn></mrow><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>-</mo><mn>1</mn></mrow></munderover><msub><mi>N</mi><mi>NonExt</mi></msub></mrow><mo>+</mo><mrow><mi>r</mi><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>=</mo><mrow><mrow><msub><mi>N</mi><mi>NonExt</mi></msub><mo>⁢</mo><msub><mi>r</mi><mi>min</mi></msub></mrow><mo>+</mo><mrow><mfrac><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>⁢</mo><mrow><mo>(</mo><mrow><msub><mi>r</mi><mi>min</mi></msub><mo>-</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow><mn>2</mn></mfrac><mo>⁢</mo><msub><mi>N</mi><mi>Ext</mi></msub></mrow></mrow><mo>=</mo><mrow><mi>O</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>×</mo><msubsup><mi>r</mi><mi>min</mi><mn>2</mn></msubsup></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\sum_{r=0}^{r_{\mathrm{min}}-1}{N_{\mathrm{NonExt}}+rN_{\mathrm{Ext}}}=N_{
\mathrm{NonExt}}r_{\mathrm{min}}+\frac{r_{\mathrm{min}}\left(r_{\mathrm{min}}-%
1\right)}{2}N_{\mathrm{Ext}}={O(n\times r_{\mathrm{min}}^{2})}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">and at least <math id="p17.m12" class="ltx_Math" alttext="\Omega(r_{\mathrm{min}})" display="inline"><semantics><mrow><mi mathvariant="normal">Ω</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msub><mi>r</mi><mi>min</mi></msub><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\Omega(r_{\mathrm{min}})</annotation></semantics></math>.</p>
</div>
<div id="p18" class="ltx_para">
<p class="ltx_p">One of issue is that the number of extender repetitions <math id="p18.m1" class="ltx_Math" alttext="r_{\mathrm{min}}" display="inline"><semantics><msub><mi>r</mi><mi>min</mi></msub><annotation encoding="application/x-tex">r_{\mathrm{min}}</annotation></semantics></math> and
the number of glyphs in the assembly <math id="p18.m2" class="ltx_Math" alttext="N" display="inline"><semantics><mi>N</mi><annotation encoding="application/x-tex">N</annotation></semantics></math> can
become arbitrary large since the target size <math id="p18.m3" class="ltx_Math" alttext="t" display="inline"><semantics><mi>t</mi><annotation encoding="application/x-tex">t</annotation></semantics></math> can take large values
e.g. if one writes
<span class="ltx_text ltx_font_typewriter">\underbrace{\hspace{65535em}}</span>
in LaTeX. The improvement proposed here does not solve that issue since setting
the coordinates of each glyph in the assembly and painting them
require <math id="p18.m4" class="ltx_Math" alttext="\Theta(N)" display="inline"><semantics><mrow><mi mathvariant="normal">Θ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\Theta(N)</annotation></semantics></math> operations as well as
(in the case of HarfBuzz) a glyph buffer of size
<math id="p18.m5" class="ltx_Math" alttext="N" display="inline"><semantics><mi>N</mi><annotation encoding="application/x-tex">N</annotation></semantics></math>. However, such large stretchy operators do not
happen in real-life mathematical formulas. Hence to avoid possible hangs in
Web engines a solution is to impose a maximum limit <math id="p18.m6" class="ltx_Math" alttext="N_{\mathrm{max}}" display="inline"><semantics><msub><mi>N</mi><mi>max</mi></msub><annotation encoding="application/x-tex">N_{\mathrm{max}}</annotation></semantics></math> for the
number of glyph in the assembly so that the complexity is limited by the
size of the DOM tree. Currently, the proposal for HarfBuzz is
<math id="p18.m7" class="ltx_Math" alttext="N_{\mathrm{max}}=128" display="inline"><semantics><mrow><msub><mi>N</mi><mi>max</mi></msub><mo>=</mo><mn>128</mn></mrow><annotation encoding="application/x-tex">N_{\mathrm{max}}=128</annotation></semantics></math>. This means that if each assembly glyph is 1em large
you won’t be able to draw stretchy operators of size more than 128em, which
sounds a quite reasonable bound.
With the above proposal, <math id="p18.m8" class="ltx_Math" alttext="r_{\mathrm{min}}" display="inline"><semantics><msub><mi>r</mi><mi>min</mi></msub><annotation encoding="application/x-tex">r_{\mathrm{min}}</annotation></semantics></math> and so
<math id="p18.m9" class="ltx_Math" alttext="N" display="inline"><semantics><mi>N</mi><annotation encoding="application/x-tex">N</annotation></semantics></math> can be determined very quickly and the cases <math id="p18.m10" class="ltx_Math" alttext="N\geq N_{\mathrm{max}}" display="inline"><semantics><mrow><mi>N</mi><mo>≥</mo><msub><mi>N</mi><mi>max</mi></msub></mrow><annotation encoding="application/x-tex">N\geq N_{\mathrm{max}}</annotation></semantics></math> rejected, so that we avoid losing time with such edge cases…</p>
</div>
<div id="p19" class="ltx_para">
<p class="ltx_p">Finally, because in our proposal we use the same overlap <math id="p19.m1" class="ltx_Math" alttext="o" display="inline"><semantics><mi>o</mi><annotation encoding="application/x-tex">o</annotation></semantics></math> everywhere
an alternative for HarfBuzz would be to set the output buffer size to
<math id="p19.m2" class="ltx_Math" alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math> (i.e. ignore <math id="p19.m3" class="ltx_Math" alttext="r-1" display="inline"><semantics><mrow><mi>r</mi><mo>-</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">r-1</annotation></semantics></math> copies of each extender and only keep the first one).
This will leave gaps that the client can fix by repeating extenders
as long as <math id="p19.m4" class="ltx_Math" alttext="o" display="inline"><semantics><mi>o</mi><annotation encoding="application/x-tex">o</annotation></semantics></math> is also provided. Then HarfBuzz math shaping can be done
with a complexity in time and space of just <math id="p19.m5" class="ltx_Math" alttext="O(n)" display="inline"><semantics><mrow><mi>O</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">O(n)</annotation></semantics></math> and it will be up to the
client to optimize or limit the painting of extenders for large values of <math id="p19.m6" class="ltx_Math" alttext="N" display="inline"><semantics><mi>N</mi><annotation encoding="application/x-tex">N</annotation></semantics></math>…</p>
</div>



{% endraw %}
