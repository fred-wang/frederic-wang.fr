---
layout: post
title: "Shelah’s PCF theory"
tags: maths
---

{% raw %}

  <div id="p1" class="ltx_para">
<p class="ltx_p">I have recently started to read a bit about Shelah’s theory of possible
cofinalities. It is a quite interesting topic in Set Theory that I have wanted
to study for a long time, but I did not really find time until now. I am
going to give an overview in this blog post for people who are interested but
also mostly to help me organizing my ideas and understanding of this subject.</p>
</div>
<div id="p2" class="ltx_para">
<p class="ltx_p">First, this theory originated from (infinite) cardinal arithmetics, which is
itself the Cantor’s invention that marked the birth of Set Theory. The
addition and multiplication of infinite cardinals are trivial, since we have</p>
</div>
<div id="p3" class="ltx_para">
<table id="S0.Ex1" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex1.m1" class="ltx_Math" alttext="\forall{κ,λ&gt;=ℵ_{0}},\,κ+λ=κ.λ=\max{\{κ,λ\}}" display="block"><semantics><mrow><mrow><mrow><mrow><mo>∀</mo><mi>κ</mi></mrow><mo>,</mo><mi>λ</mi></mrow><mo>≥</mo><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub></mrow><mo rspace="4.2pt">,</mo><mrow><mrow><mi>κ</mi><mo>+</mo><mi>λ</mi></mrow><mo>=</mo><mi>κ</mi></mrow><mo>.</mo><mrow><mi>λ</mi><mo>=</mo><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">{</mo><mi>κ</mi><mo>,</mo><mi>λ</mi><mo stretchy="false">}</mo></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall{κ,λ&gt;=ℵ_{0}},\,κ+λ=κ.λ=\max{\{κ,λ\}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p4" class="ltx_para">
<p class="ltx_p">The exponentiation is much more difficult (and interesting!). Here is Theorem
5.20 from Thomas Jech’s book "Set Theory":</p>
</div>
<div id="S0.Thmtheorem1" class="ltx_theorem ltx_theorem_theorem">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem"><span class="ltx_tag ltx_tag_theorem">Theorem 0.1</span></h6>
<div id="S0.Thmtheorem1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Let <math id="S0.Thmtheorem1.p1.m1" class="ltx_Math" alttext="λ" display="inline"><semantics><mi>λ</mi><annotation encoding="application/x-tex">λ</annotation></semantics></math> be an infinite cardinal. Then for all infinite cardinal <math id="S0.Thmtheorem1.p1.m2" class="ltx_Math" alttext="κ" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">κ</annotation></semantics></math>, the value
of <math id="S0.Thmtheorem1.p1.m3" class="ltx_Math" alttext="κ^{λ}" display="inline"><semantics><msup><mi>κ</mi><mi>λ</mi></msup><annotation encoding="application/x-tex">κ^{λ}</annotation></semantics></math> is computed as follows, by induction on <math id="S0.Thmtheorem1.p1.m4" class="ltx_Math" alttext="κ" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">κ</annotation></semantics></math>:</span></p>
</div>
<div id="S0.Thmtheorem1.p2" class="ltx_para">
<ol id="I1" class="ltx_enumerate">
<li id="I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">1.</span></span> 
<div id="I1.i1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">If </span><math id="I1.i1.p1.m1" class="ltx_Math" alttext="κ\leq λ" display="inline"><semantics><mrow><mi>κ</mi><mo>≤</mo><mi>λ</mi></mrow><annotation encoding="application/x-tex">κ\leq λ</annotation></semantics></math><span class="ltx_text ltx_font_italic"> then </span><math id="I1.i1.p1.m2" class="ltx_Math" alttext="κ^{λ}=2^{λ}" display="inline"><semantics><mrow><msup><mi>κ</mi><mi>λ</mi></msup><mo>=</mo><msup><mn>2</mn><mi>λ</mi></msup></mrow><annotation encoding="application/x-tex">κ^{λ}=2^{λ}</annotation></semantics></math><span class="ltx_text ltx_font_italic">.</span></p>
</div>
</li>
<li id="I1.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">2.</span></span> 
<div id="I1.i2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">If there exists some </span><math id="I1.i2.p1.m1" class="ltx_Math" alttext="\mu&lt;κ" display="inline"><semantics><mrow><mi>μ</mi><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu&lt;κ</annotation></semantics></math><span class="ltx_text ltx_font_italic"> such that </span><math id="I1.i2.p1.m2" class="ltx_Math" alttext="\mu^{λ}\geq κ" display="inline"><semantics><mrow><msup><mi>μ</mi><mi>λ</mi></msup><mo>≥</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu^{λ}\geq κ</annotation></semantics></math><span class="ltx_text ltx_font_italic">,
then </span><math id="I1.i2.p1.m3" class="ltx_Math" alttext="κ^{λ}=\mu^{λ}" display="inline"><semantics><mrow><msup><mi>κ</mi><mi>λ</mi></msup><mo>=</mo><msup><mi>μ</mi><mi>λ</mi></msup></mrow><annotation encoding="application/x-tex">κ^{λ}=\mu^{λ}</annotation></semantics></math><span class="ltx_text ltx_font_italic"></span></p>
</div>
</li>
<li id="I1.i3" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">3.</span></span> 
<div id="I1.i3.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">If </span><math id="I1.i3.p1.m1" class="ltx_Math" alttext="κ&gt;λ" display="inline"><semantics><mrow><mi>κ</mi><mo>&gt;</mo><mi>λ</mi></mrow><annotation encoding="application/x-tex">κ&gt;λ</annotation></semantics></math><span class="ltx_text ltx_font_italic"> and </span><math id="I1.i3.p1.m2" class="ltx_Math" alttext="\mu^{λ}&lt;κ" display="inline"><semantics><mrow><msup><mi>μ</mi><mi>λ</mi></msup><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu^{λ}&lt;κ</annotation></semantics></math><span class="ltx_text ltx_font_italic"> for all </span><math id="I1.i3.p1.m3" class="ltx_Math" alttext="\mu&lt;κ" display="inline"><semantics><mrow><mi>μ</mi><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu&lt;κ</annotation></semantics></math><span class="ltx_text ltx_font_italic">, then</span></p>
<ol id="I1.I1" class="ltx_enumerate">
<li id="I1.I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">(a)</span></span> 
<div id="I1.I1.i1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">if </span><math id="I1.I1.i1.p1.m1" class="ltx_Math" alttext="\operatorname{cf}(κ)&gt;λ" display="inline"><semantics><mrow><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>κ</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&gt;</mo><mi>λ</mi></mrow><annotation encoding="application/x-tex">\operatorname{cf}(κ)&gt;λ</annotation></semantics></math><span class="ltx_text ltx_font_italic">, then </span><math id="I1.I1.i1.p1.m2" class="ltx_Math" alttext="κ^{λ}=κ" display="inline"><semantics><mrow><msup><mi>κ</mi><mi>λ</mi></msup><mo>=</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">κ^{λ}=κ</annotation></semantics></math><span class="ltx_text ltx_font_italic">,</span></p>
</div>
</li>
<li id="I1.I1.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">(b)</span></span> 
<div id="I1.I1.i2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">if </span><math id="I1.I1.i2.p1.m1" class="ltx_Math" alttext="\operatorname{cf}(κ)\leq λ" display="inline"><semantics><mrow><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>κ</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mi>λ</mi></mrow><annotation encoding="application/x-tex">\operatorname{cf}(κ)\leq λ</annotation></semantics></math><span class="ltx_text ltx_font_italic">, then </span><math id="I1.I1.i2.p1.m2" class="ltx_Math" alttext="κ^{λ}=κ^{\operatorname{cf}κ}" display="inline"><semantics><mrow><msup><mi>κ</mi><mi>λ</mi></msup><mo>=</mo><msup><mi>κ</mi><mrow><mo>cf</mo><mo>⁡</mo><mi>κ</mi></mrow></msup></mrow><annotation encoding="application/x-tex">κ^{λ}=κ^{\operatorname{cf}κ}</annotation></semantics></math><span class="ltx_text ltx_font_italic"></span></p>
</div>
</li>
</ol>
</div>
</li>
</ol>
</div>
</div>
<div id="p5" class="ltx_para">
<p class="ltx_p">This theorem reduces the problem of exponentiation to the determination of the
continuum function <math id="p5.m1" class="ltx_Math" alttext="κ\mapsto 2^{κ}" display="inline"><semantics><mrow><mi>κ</mi><mo>↦</mo><msup><mn>2</mn><mi>κ</mi></msup></mrow><annotation encoding="application/x-tex">κ\mapsto 2^{κ}</annotation></semantics></math> and, on singular cardinals <math id="p5.m2" class="ltx_Math" alttext="κ" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">κ</annotation></semantics></math>, of the gimel
function <math id="p5.m3" class="ltx_Math" alttext="κ\mapsto\operatorname{\gimel}(κ)=κ^{\operatorname{cf}κ}" display="inline"><semantics><mrow><mi>κ</mi><mo>↦</mo><mrow><mo>ℷ</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>κ</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>κ</mi><mrow><mo>cf</mo><mo>⁡</mo><mi>κ</mi></mrow></msup></mrow><annotation encoding="application/x-tex">κ\mapsto\operatorname{\gimel}(κ)=κ^{\operatorname{cf}κ}</annotation></semantics></math> . There are
simular reductions of infinite sums and products to <math id="p5.m4" class="ltx_Math" alttext="\sup" display="inline"><semantics><mo>sup</mo><annotation encoding="application/x-tex">\sup</annotation></semantics></math> and exponentation
operations, so computing these two functions is the crucial point of
cardinal arithmetics.</p>
</div>
<div id="p6" class="ltx_para">
<p class="ltx_p">Set theorists proved by forcing that we can not really say more about the value
of the continuum for regular cardinals. Indeed, the only constraints are that
the function must be increasing and must satisfy some consequences of König’s
theorem (namely <math id="p6.m1" class="ltx_Math" alttext="2^{κ}&gt;κ" display="inline"><semantics><mrow><msup><mn>2</mn><mi>κ</mi></msup><mo>&gt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">2^{κ}&gt;κ</annotation></semantics></math> and <math id="p6.m2" class="ltx_Math" alttext="\operatorname{cf}(2^{κ})&gt;κ" display="inline"><semantics><mrow><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>κ</mi></msup><mo stretchy="false">)</mo></mrow></mrow><mo>&gt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\operatorname{cf}(2^{κ})&gt;κ</annotation></semantics></math>).</p>
</div>
<div id="p7" class="ltx_para">
<p class="ltx_p">At the opposite it turns out that more properties can be proved for the
singular case. For instance, we have the striking bound of <math id="p7.m1" class="ltx_Math" alttext="\operatorname{\gimel}(ℵ_{ω})" display="inline"><semantics><mrow><mo>ℷ</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\operatorname{\gimel}(ℵ_{ω})</annotation></semantics></math> mentioned
on Shelah’s Web Archive:</p>
</div>
<div id="S0.Thmtheorem2" class="ltx_theorem ltx_theorem_theorem">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem"><span class="ltx_tag ltx_tag_theorem">Theorem 0.2</span></h6>
<div id="S0.Thmtheorem2.p1" class="ltx_para">
<table id="S0.Ex2" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex2.m1" class="ltx_Math" alttext="\operatorname{\gimel}(ℵ_{ω})=ℵ_{ω}^{ℵ_{0}}\leq 2^{ℵ_{0}}+ℵ_{ω_{4}}" display="block"><semantics><mrow><mrow><mo>ℷ</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msubsup><mi mathvariant="normal">ℵ</mi><mi>ω</mi><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub></msubsup><mo>≤</mo><mrow><msup><mn>2</mn><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub></msup><mo>+</mo><msub><mi mathvariant="normal">ℵ</mi><msub><mi>ω</mi><mn>4</mn></msub></msub></mrow></mrow><annotation encoding="application/x-tex">\operatorname{\gimel}(ℵ_{ω})=ℵ_{ω}^{ℵ_{0}}\leq 2^{ℵ_{0}}+ℵ_{ω_{4}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</div>
<div id="p8" class="ltx_para">
<p class="ltx_p">Shelah developed his PCF theory in order to obtain these kinds of results. The
basic idea is to consider an "interval" of regular cardinals <math id="p8.m1" class="ltx_Math" alttext="A" display="inline"><semantics><mi>A</mi><annotation encoding="application/x-tex">A</annotation></semantics></math> i.e. with
the property that any regular cardinal between two elements of <math id="p8.m2" class="ltx_Math" alttext="A" display="inline"><semantics><mi>A</mi><annotation encoding="application/x-tex">A</annotation></semantics></math> is itself
an element of <math id="p8.m3" class="ltx_Math" alttext="A" display="inline"><semantics><mi>A</mi><annotation encoding="application/x-tex">A</annotation></semantics></math>. Then we define the set of possible cofinalities of
ultraproducts of <math id="p8.m4" class="ltx_Math" alttext="A" display="inline"><semantics><mi>A</mi><annotation encoding="application/x-tex">A</annotation></semantics></math>:</p>
</div>
<div id="p9" class="ltx_para">
<table id="S0.Ex3" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex3.m1" class="ltx_Math" alttext="\operatorname{pcf}(A)=\left\{\operatorname{cf}{\left(\prod A/U\right)}|U\text{
 is an ultrafilter on }A\right\}" display="block"><semantics><mrow><mrow><mo>pcf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mo>{</mo><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo>(</mo><mrow><mo largeop="true" movablelimits="false" symmetric="true">∏</mo><mrow><mi>A</mi><mo>/</mo><mi>U</mi></mrow></mrow><mo>)</mo></mrow></mrow><mo stretchy="false">|</mo><mrow><mi>U</mi><mo>⁢</mo><mtext> is an ultrafilter on </mtext><mo>⁢</mo><mi>A</mi></mrow><mo>}</mo></mrow></mrow><annotation encoding="application/x-tex">\operatorname{pcf}(A)=\left\{\operatorname{cf}{\left(\prod A/U\right)}|U\text{
 is an ultrafilter on }A\right\}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p10" class="ltx_para">
<p class="ltx_p">where <math id="p10.m1" class="ltx_Math" alttext="\prod A/U" display="inline"><semantics><mrow><mo largeop="true" symmetric="true">∏</mo><mrow><mi>A</mi><mo>/</mo><mi>U</mi></mrow></mrow><annotation encoding="application/x-tex">\prod A/U</annotation></semantics></math> is a totally ordered set: an ordinal function is smaller
than another if it is smaller "almost everywhere" (i.e. on an element of the
ultrafilter <math id="p10.m2" class="ltx_Math" alttext="U" display="inline"><semantics><mi>U</mi><annotation encoding="application/x-tex">U</annotation></semantics></math>). The cofinality of such a totally ordered set is defined in a
similar way as for cardinals: it is shortest length of an unbounded sequence.</p>
</div>
<div id="p11" class="ltx_para">
<p class="ltx_p">Now, <math id="p11.m1" class="ltx_Math" alttext="\prod A/U" display="inline"><semantics><mrow><mo largeop="true" symmetric="true">∏</mo><mrow><mi>A</mi><mo>/</mo><mi>U</mi></mrow></mrow><annotation encoding="application/x-tex">\prod A/U</annotation></semantics></math> is a topological space (a basis is naturally given by the
open intervals with respect to the total order) and so we can use topological
methods to get information on it.
In particular, this provides information on <math id="p11.m2" class="ltx_Math" alttext="\prod A" display="inline"><semantics><mrow><mo largeop="true" symmetric="true">∏</mo><mi>A</mi></mrow><annotation encoding="application/x-tex">\prod A</annotation></semantics></math>, which in turn provides
infomation on <math id="p11.m3" class="ltx_Math" alttext="\left|\prod A\right|" display="inline"><semantics><mrow><mo>|</mo><mrow><mo largeop="true" symmetric="true">∏</mo><mi>A</mi></mrow><mo>|</mo></mrow><annotation encoding="application/x-tex">\left|\prod A\right|</annotation></semantics></math>, the infinite product of the (regular)
cardinals in <math id="p11.m4" class="ltx_Math" alttext="A" display="inline"><semantics><mi>A</mi><annotation encoding="application/x-tex">A</annotation></semantics></math>.</p>
</div>
<div id="p12" class="ltx_para">
<p class="ltx_p">For example, if <math id="p12.m1" class="ltx_Math" alttext="A={\left\{\aleph_{n}\right\}}_{n=0}^{\infty}" display="inline"><semantics><mrow><mi>A</mi><mo>=</mo><msubsup><mrow><mo>{</mo><msub><mi mathvariant="normal">ℵ</mi><mi>n</mi></msub><mo>}</mo></mrow><mrow><mi>n</mi><mo>=</mo><mn>0</mn></mrow><mi mathvariant="normal">∞</mi></msubsup></mrow><annotation encoding="application/x-tex">A={\left\{\aleph_{n}\right\}}_{n=0}^{\infty}</annotation></semantics></math> and if we
assume that <math id="p12.m2" class="ltx_Math" alttext="\aleph_{\omega}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub><annotation encoding="application/x-tex">\aleph_{\omega}</annotation></semantics></math> is strong limit then one can show that <math id="p12.m3" class="ltx_Math" alttext="\operatorname{pcf}(A)" display="inline"><semantics><mrow><mo>pcf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\operatorname{pcf}(A)</annotation></semantics></math> is
itself an interval of regular cardinals and has a maximum element which is
<math id="p12.m4" class="ltx_Math" alttext="2^{\aleph_{\omega}}" display="inline"><semantics><msup><mn>2</mn><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub></msup><annotation encoding="application/x-tex">2^{\aleph_{\omega}}</annotation></semantics></math>. So its elements are in the sequence of cardinals
</p>
</div>
<div id="p13" class="ltx_para">
<table id="S0.Ex4" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex4.m1" class="ltx_Math" alttext="\min{\operatorname{pcf}(A)}=\aleph_{\alpha},\aleph_{\alpha+1},\aleph_{\alpha+2
},\ldots,\aleph_{\alpha+\lambda}=\max{\operatorname{pcf}(A)}=2^{\aleph_{\omega}}" display="block"><semantics><mrow><mrow><mrow><mi>min</mi><mo>⁢</mo><mrow><mo>pcf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><mrow><msub><mi mathvariant="normal">ℵ</mi><mi>α</mi></msub><mo>,</mo><msub><mi mathvariant="normal">ℵ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>,</mo><msub><mi mathvariant="normal">ℵ</mi><mrow><mi>α</mi><mo>+</mo><mn>2</mn></mrow></msub><mo>,</mo><mi mathvariant="normal">…</mi></mrow></mrow><mo>,</mo><mrow><msub><mi mathvariant="normal">ℵ</mi><mrow><mi>α</mi><mo>+</mo><mi>λ</mi></mrow></msub><mo>=</mo><mrow><mi>max</mi><mo>⁢</mo><mrow><mo>pcf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><msup><mn>2</mn><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub></msup></mrow></mrow><annotation encoding="application/x-tex">\min{\operatorname{pcf}(A)}=\aleph_{\alpha},\aleph_{\alpha+1},\aleph_{\alpha+2
},\ldots,\aleph_{\alpha+\lambda}=\max{\operatorname{pcf}(A)}=2^{\aleph_{\omega}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p14" class="ltx_para">
<p class="ltx_p">and obviouly, <math id="p14.m1" class="ltx_Math" alttext="\alpha+\lambda\leq{\left|\operatorname{pcf}A\right|}" display="inline"><semantics><mrow><mrow><mi>α</mi><mo>+</mo><mi>λ</mi></mrow><mo>≤</mo><mrow><mo>|</mo><mrow><mo>pcf</mo><mo>⁡</mo><mi>A</mi></mrow><mo>|</mo></mrow></mrow><annotation encoding="application/x-tex">\alpha+\lambda\leq{\left|\operatorname{pcf}A\right|}</annotation></semantics></math>. But the size of
<math id="p14.m2" class="ltx_Math" alttext="\operatorname{pcf}A" display="inline"><semantics><mrow><mo>pcf</mo><mo>⁡</mo><mi>A</mi></mrow><annotation encoding="application/x-tex">\operatorname{pcf}A</annotation></semantics></math> is not greater than the number of ultrafilters of <math id="p14.m3" class="ltx_Math" alttext="A" display="inline"><semantics><mi>A</mi><annotation encoding="application/x-tex">A</annotation></semantics></math>, which are
sets of subsets of the countable set <math id="p14.m4" class="ltx_Math" alttext="A" display="inline"><semantics><mi>A</mi><annotation encoding="application/x-tex">A</annotation></semantics></math> i.e. there are at most <math id="p14.m5" class="ltx_Math" alttext="2^{2^{\aleph_{0}}}" display="inline"><semantics><msup><mn>2</mn><msup><mn>2</mn><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub></msup></msup><annotation encoding="application/x-tex">2^{2^{\aleph_{0}}}</annotation></semantics></math>
many of them. Since we assume that <math id="p14.m6" class="ltx_Math" alttext="\aleph_{\omega}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub><annotation encoding="application/x-tex">\aleph_{\omega}</annotation></semantics></math> is a strong limit cardinal,
we have <math id="p14.m7" class="ltx_Math" alttext="\alpha+\lambda\leq 2^{2^{\aleph_{0}}}&lt;\aleph_{\omega}" display="inline"><semantics><mrow><mrow><mi>α</mi><mo>+</mo><mi>λ</mi></mrow><mo>≤</mo><msup><mn>2</mn><msup><mn>2</mn><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub></msup></msup><mo>&lt;</mo><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub></mrow><annotation encoding="application/x-tex">\alpha+\lambda\leq 2^{2^{\aleph_{0}}}&lt;\aleph_{\omega}</annotation></semantics></math> and finally</p>
</div>
<div id="S0.Thmtheorem3" class="ltx_theorem ltx_theorem_theorem">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem"><span class="ltx_tag ltx_tag_theorem">Theorem 0.3</span></h6>
<div id="S0.Thmtheorem3.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">If <math id="S0.Thmtheorem3.p1.m1" class="ltx_Math" alttext="\aleph_{\omega}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub><annotation encoding="application/x-tex">\aleph_{\omega}</annotation></semantics></math> is a strong limit cardinal then</span></p>
<table id="S0.Ex5" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex5.m1" class="ltx_Math" alttext="2^{\aleph_{\omega}}&lt;\aleph_{\aleph_{\omega}}" display="block"><semantics><mrow><msup><mn>2</mn><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub></msup><mo>&lt;</mo><msub><mi mathvariant="normal">ℵ</mi><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub></msub></mrow><annotation encoding="application/x-tex">2^{\aleph_{\omega}}&lt;\aleph_{\aleph_{\omega}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</div>
<div id="p15" class="ltx_para">
<p class="ltx_p">These are of course just two examples of what we can say about the values of the
continuum and gimel functions at a singular cardinal (here for <math id="p15.m1" class="ltx_Math" alttext="\aleph_{\omega}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mi>ω</mi></msub><annotation encoding="application/x-tex">\aleph_{\omega}</annotation></semantics></math>,
the smallest infinite singular cardinal). Several other results are known and
the PCF theory also applies to other areas than cardinal arithmetics. Many
beautiful topics that I would like to learn about…</p>
</div>

{% endraw %}
