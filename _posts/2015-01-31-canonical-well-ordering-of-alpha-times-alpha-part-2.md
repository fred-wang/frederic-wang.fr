---
layout: post
title: "The canonical well-ordering of α×α (part 2)"
tags: maths
---

{% raw %}

  

<div id="p1" class="ltx_para">
<p class="ltx_p">In a my previous blog post, I discussed the canonical well-ordering on
<math id="p1.m1" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo>×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math> and stated theorem <a href="#S0.Thmtheorem5" title="Theorem 0.5. ‣ The canonical well-ordering of ×αα (part 2)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.5</span></a> below to calculate its
order-type <math id="p1.m2" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math>. Subsequent corollaries provided a bound for
<math id="p1.m3" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math>, its fixed points and a proof that infinite cardinals were
among these fixed points (and so that cardinal addition and multiplication
is trivial).
In this second part, I’m going to provide the proof of this theorem.</p>
</div>
<div id="p2" class="ltx_para">
<p class="ltx_p">First, we note that for all <math id="p2.m1" class="ltx_Math" alttext="n&lt;\omega" display="inline"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">n&lt;\omega</annotation></semantics></math>, there is only one order-type for
<math id="p2.m2" class="ltx_Math" alttext="n\times n" display="inline"><semantics><mrow><mi>n</mi><mo>×</mo><mi>n</mi></mrow><annotation encoding="application/x-tex">n\times n</annotation></semantics></math>, since
the notion of cardinal and ordinal is the same for finite sets.
So indeed
</p>
<table id="S0.Ex1" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex1.m1" class="ltx_Math" alttext="\forall n&lt;\omega,\gamma(n)={|n\times n|}=n^{2}" display="block"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>n</mi></mrow><mo>&lt;</mo><mi>ω</mi></mrow><mo>,</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mo stretchy="false">|</mo><mrow><mi>n</mi><mo>×</mo><mi>n</mi></mrow><mo stretchy="false">|</mo></mrow><mo>=</mo><msup><mi>n</mi><mn>2</mn></msup></mrow></mrow><annotation encoding="application/x-tex">\forall n&lt;\omega,\gamma(n)={|n\times n|}=n^{2}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">and taking the limit, we get our first infinite fixed point:</p>
<table id="S0.Ex2" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex2.m1" class="ltx_Math" alttext="\gamma(\omega)=\sup_{n&lt;\omega}{\gamma(n)}=\omega" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>ω</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><munder><mo movablelimits="false">sup</mo><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></munder><mo>⁡</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\gamma(\omega)=\sup_{n&lt;\omega}{\gamma(n)}=\omega</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p3" class="ltx_para">
<p class="ltx_p">For all <math id="p3.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> the ordering on
<math id="p3.m2" class="ltx_Math" alttext="{(\alpha+1)}\times{(\alpha+1)}" display="inline"><semantics><mrow><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow><mo>×</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">{(\alpha+1)}\times{(\alpha+1)}</annotation></semantics></math> is as follows: first the
elements of <math id="p3.m3" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo>×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math> ordered as <math id="p3.m4" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math>, followed by
the elements <math id="p3.m5" class="ltx_Math" alttext="(\xi,\alpha)" display="inline"><semantics><mrow><mo stretchy="false">(</mo><mi>ξ</mi><mo>,</mo><mi>α</mi><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">(\xi,\alpha)</annotation></semantics></math> for <math id="p3.m6" class="ltx_Math" alttext="0\leq\xi&lt;\alpha" display="inline"><semantics><mrow><mn>0</mn><mo>≤</mo><mi>ξ</mi><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">0\leq\xi&lt;\alpha</annotation></semantics></math>, followed by
the elements <math id="p3.m7" class="ltx_Math" alttext="(\alpha,\xi)" display="inline"><semantics><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>,</mo><mi>ξ</mi><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">(\alpha,\xi)</annotation></semantics></math> for <math id="p3.m8" class="ltx_Math" alttext="0\leq\xi\leq\alpha" display="inline"><semantics><mrow><mn>0</mn><mo>≤</mo><mi>ξ</mi><mo>≤</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">0\leq\xi\leq\alpha</annotation></semantics></math>. Hence</p>
<table id="S0.Ex3" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex3.m1" class="ltx_Math" alttext="\forall\alpha,{\gamma(\alpha+1)}={\gamma(\alpha)}+\alpha\cdot 2+1" display="block"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha,{\gamma(\alpha+1)}={\gamma(\alpha)}+\alpha\cdot 2+1</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p4" class="ltx_para">
<p class="ltx_p">From this, we can try to calculate the next values of <math id="p4.m1" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> after <math id="p4.m2" class="ltx_Math" alttext="\omega" display="inline"><semantics><mi>ω</mi><annotation encoding="application/x-tex">\omega</annotation></semantics></math>:</p>
<table id="S0.Ex4" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex4.m1" class="ltx_Math" alttext="{\gamma(\omega+1)}=\omega+{\omega\cdot 2}+1={\omega\cdot 3}+1" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>ω</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>ω</mi><mo>+</mo><mrow><mi>ω</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mn>1</mn></mrow><mo>=</mo><mrow><mrow><mi>ω</mi><mo>⋅</mo><mn>3</mn></mrow><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega+1)}=\omega+{\omega\cdot 2}+1={\omega\cdot 3}+1</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<table id="S0.Ex5" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex5.m1" class="ltx_Math" alttext="{\gamma(\omega+2)}={\omega\cdot 3+1}+\omega+1+\omega+1+1={\omega\cdot 5}+2" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>ω</mi><mo>+</mo><mn>2</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>ω</mi><mo>⋅</mo><mn>3</mn></mrow><mo>+</mo><mn>1</mn><mo>+</mo><mi>ω</mi><mo>+</mo><mn>1</mn><mo>+</mo><mi>ω</mi><mo>+</mo><mn>1</mn><mo>+</mo><mn>1</mn></mrow><mo>=</mo><mrow><mrow><mi>ω</mi><mo>⋅</mo><mn>5</mn></mrow><mo>+</mo><mn>2</mn></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega+2)}={\omega\cdot 3+1}+\omega+1+\omega+1+1={\omega\cdot 5}+2</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">The important point is <math id="p4.m3" class="ltx_Math" alttext="1+\omega=\omega" display="inline"><semantics><mrow><mrow><mn>1</mn><mo>+</mo><mi>ω</mi></mrow><mo>=</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">1+\omega=\omega</annotation></semantics></math> ; in general we will use
several times the property
<math id="p4.m4" class="ltx_Math" alttext="\alpha+\omega^{\beta}=\omega^{\beta}" display="inline"><semantics><mrow><mrow><mi>α</mi><mo>+</mo><msup><mi>ω</mi><mi>β</mi></msup></mrow><mo>=</mo><msup><mi>ω</mi><mi>β</mi></msup></mrow><annotation encoding="application/x-tex">\alpha+\omega^{\beta}=\omega^{\beta}</annotation></semantics></math> if <math id="p4.m5" class="ltx_Math" alttext="\alpha&lt;\omega^{\beta}" display="inline"><semantics><mrow><mi>α</mi><mo>&lt;</mo><msup><mi>ω</mi><mi>β</mi></msup></mrow><annotation encoding="application/x-tex">\alpha&lt;\omega^{\beta}</annotation></semantics></math>.
By a simple recurrence (see proposition <a href="#S0.Thmtheorem1" title="Proposition 0.1. ‣ The canonical well-ordering of ×αα (part 2)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.1</span></a>),
we can generalize the expression to arbitrary <math id="p4.m6" class="ltx_Math" alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math>:</p>
<table id="S0.Ex6" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex6.m1" class="ltx_Math" alttext="{\gamma(\omega+n)}=\omega\left(2n+1\right)+n" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>ω</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>ω</mi><mo>⁢</mo><mrow><mo>(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega+n)}=\omega\left(2n+1\right)+n</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">and so taking the limit</p>
<table id="S0.Ex7" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex7.m1" class="ltx_Math" alttext="{\gamma(\omega\cdot 2)}=\omega^{2}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>ω</mi><mo>⋅</mo><mn>2</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mn>2</mn></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega\cdot 2)}=\omega^{2}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">which is a limit ordinal not fixed by <math id="p4.m7" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>.
We note another point that will be used later: taking the limit
“eliminates” the smallest terms.
More generally, we can perform the same calculation, starting from any
arbitrary <math id="p4.m8" class="ltx_Math" alttext="\alpha\geq\omega" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\alpha\geq\omega</annotation></semantics></math>:</p>
</div>
<div id="S0.Thmtheorem1" class="ltx_theorem ltx_theorem_proposition">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Proposition 0.1</span>.</h6>
<div id="S0.Thmtheorem1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">For any limit ordinal <math id="S0.Thmtheorem1.p1.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> and <math id="S0.Thmtheorem1.p1.m2" class="ltx_Math" alttext="1\leq n&lt;\omega" display="inline"><semantics><mrow><mn mathvariant="normal">1</mn><mo mathvariant="normal">≤</mo><mi>n</mi><mo mathvariant="normal">&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">1\leq n&lt;\omega</annotation></semantics></math> we have</span></p>
<table id="S0.Ex8" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex8.m1" class="ltx_Math" alttext="\gamma(\alpha+n)=\gamma(\alpha)+{\alpha\cdot{2n}}+n" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+n)=\gamma(\alpha)+{\alpha\cdot{2n}}+n</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p5" class="ltx_para">
<p class="ltx_p">For <math id="p5.m1" class="ltx_Math" alttext="n=1" display="inline"><semantics><mrow><mi>n</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n=1</annotation></semantics></math> this is the relation for <math id="p5.m2" class="ltx_Math" alttext="\gamma(\alpha+1)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+1)</annotation></semantics></math> explained
above. If the relation is true for <math id="p5.m3" class="ltx_Math" alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math> then</p>
<table id="S0.Ex9" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex9.m1" class="ltx_Math" alttext="\gamma(\alpha+n+1)=\gamma(\alpha+n)+{\left(\alpha+n\right)\cdot 2}+1" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mo>(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo>)</mo></mrow><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+n+1)=\gamma(\alpha+n)+{\left(\alpha+n\right)\cdot 2}+1</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<table id="S0.Ex10" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex10.m1" class="ltx_Math" alttext="\gamma(\alpha+n+1)=\gamma(\alpha)+{\alpha\cdot{2n}}+n+\alpha+n+\alpha+n+1" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi>n</mi><mo>+</mo><mi>α</mi><mo>+</mo><mi>n</mi><mo>+</mo><mi>α</mi><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+n+1)=\gamma(\alpha)+{\alpha\cdot{2n}}+n+\alpha+n+\alpha+n+1</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">and since <math id="p5.m4" class="ltx_Math" alttext="\alpha\geq\omega" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\alpha\geq\omega</annotation></semantics></math> we have <math id="p5.m5" class="ltx_Math" alttext="n+\alpha=\alpha" display="inline"><semantics><mrow><mrow><mi>n</mi><mo>+</mo><mi>α</mi></mrow><mo>=</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">n+\alpha=\alpha</annotation></semantics></math> and so</p>
<table id="S0.Ex11" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex11.m1" class="ltx_Math" alttext="\gamma(\alpha+n+1)=\gamma(\alpha)+{\alpha\cdot{(2n+1)}}+n+1" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mi>α</mi><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+n+1)=\gamma(\alpha)+{\alpha\cdot{(2n+1)}}+n+1</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">Which shows the result at step <math id="p5.m6" class="ltx_Math" alttext="n+1" display="inline"><semantics><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n+1</annotation></semantics></math>.
∎</p>
</div>
</div>
<div id="p6" class="ltx_para">
<p class="ltx_p">As above, we can take the limit and say
<math id="p6.m1" class="ltx_Math" alttext="{\gamma(\alpha+\omega)}=\sup_{n&lt;\omega}{\gamma(\alpha+n)}=\gamma(\alpha)+%
\alpha\cdot\omega" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>ω</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msub><mo>sup</mo><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></msub><mo>⁡</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mi>α</mi><mo>⋅</mo><mi>ω</mi></mrow></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha+\omega)}=\sup_{n&lt;\omega}{\gamma(\alpha+n)}=\gamma(\alpha)+%
\alpha\cdot\omega</annotation></semantics></math> which is consistent with
<math id="p6.m2" class="ltx_Math" alttext="{\gamma(\omega\cdot 2)}=\omega+\omega^{2}=\omega^{2}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>ω</mi><mo>⋅</mo><mn>2</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>ω</mi><mo>+</mo><msup><mi>ω</mi><mn>2</mn></msup></mrow><mo>=</mo><msup><mi>ω</mi><mn>2</mn></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega\cdot 2)}=\omega+\omega^{2}=\omega^{2}</annotation></semantics></math>. However, if we
consider the Cantor Normal Form
<math id="p6.m3" class="ltx_Math" alttext="\alpha=\omega^{\beta_{1}}n_{1}+...+\omega^{\beta_{k}}n_{k}" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><msub><mi>n</mi><mn>1</mn></msub></mrow><mo>+</mo><mi mathvariant="normal">…</mi><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mi>k</mi></msub></msup><mo>⁢</mo><msub><mi>n</mi><mi>k</mi></msub></mrow></mrow></mrow><annotation encoding="application/x-tex">\alpha=\omega^{\beta_{1}}n_{1}+...+\omega^{\beta_{k}}n_{k}</annotation></semantics></math>,
then for all <math id="p6.m4" class="ltx_Math" alttext="n&lt;\omega" display="inline"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">n&lt;\omega</annotation></semantics></math> we have can use the fact that “<math id="p6.m5" class="ltx_Math" alttext="\omega^{\beta_{1}}" display="inline"><semantics><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><annotation encoding="application/x-tex">\omega^{\beta_{1}}</annotation></semantics></math> will
eliminate smaller terms on its left” that is
<math id="p6.m6" class="ltx_Math" alttext="\alpha\cdot n=\omega^{\beta_{1}}{(n_{1}n)}+\omega^{\beta_{2}}n_{2}+...+\omega^%
{\beta_{k}}n_{k}" display="inline"><semantics><mrow><mrow><mi>α</mi><mo>⋅</mo><mi>n</mi></mrow><mo>=</mo><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><msub><mi>n</mi><mn>1</mn></msub><mo>⁢</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>2</mn></msub></msup><mo>⁢</mo><msub><mi>n</mi><mn>2</mn></msub></mrow><mo>+</mo><mi mathvariant="normal">…</mi><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mi>k</mi></msub></msup><mo>⁢</mo><msub><mi>n</mi><mi>k</mi></msub></mrow></mrow></mrow><annotation encoding="application/x-tex">\alpha\cdot n=\omega^{\beta_{1}}{(n_{1}n)}+\omega^{\beta_{2}}n_{2}+...+\omega^%
{\beta_{k}}n_{k}</annotation></semantics></math>. Then using the
fact that “taking the limit eliminates the smallest terms” we get
<math id="p6.m7" class="ltx_Math" alttext="\alpha\cdot\omega=\sup_{n&lt;\omega}\alpha\cdot n=\omega^{\beta_{1}+1}" display="inline"><semantics><mrow><mrow><mi>α</mi><mo>⋅</mo><mi>ω</mi></mrow><mo>=</mo><mrow><msub><mo>sup</mo><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></msub><mo>⁡</mo><mrow><mi>α</mi><mo>⋅</mo><mi>n</mi></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mrow><msub><mi>β</mi><mn>1</mn></msub><mo>+</mo><mn>1</mn></mrow></msup></mrow><annotation encoding="application/x-tex">\alpha\cdot\omega=\sup_{n&lt;\omega}\alpha\cdot n=\omega^{\beta_{1}+1}</annotation></semantics></math>. So actually, we have a nicer formula where
<math id="p6.m8" class="ltx_Math" alttext="\alpha\cdot\omega" display="inline"><semantics><mrow><mi>α</mi><mo>⋅</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\alpha\cdot\omega</annotation></semantics></math> is put in Cantor Normal Form:</p>
<table id="S0.Ex12" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex12.m1" class="ltx_Math" alttext="\forall\alpha\geq\omega,{\gamma(\alpha+\omega)}=\gamma(\alpha)+\omega^{\log_{%
\omega}(\alpha)+1}" display="block"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>≥</mo><mi>ω</mi></mrow><mo>,</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>ω</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mn>1</mn></mrow></msup></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha\geq\omega,{\gamma(\alpha+\omega)}=\gamma(\alpha)+\omega^{\log_{%
\omega}(\alpha)+1}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">This can be generalized by the following proposition:</p>
</div>
<div id="S0.Thmtheorem2" class="ltx_theorem ltx_theorem_proposition">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Proposition 0.2</span>.</h6>
<div id="S0.Thmtheorem2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">For any <math id="S0.Thmtheorem2.p1.m1" class="ltx_Math" alttext="\alpha\geq\omega" display="inline"><semantics><mrow><mi>α</mi><mo mathvariant="normal">≥</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\alpha\geq\omega</annotation></semantics></math> and
<math id="S0.Thmtheorem2.p1.m2" class="ltx_Math" alttext="\beta\geq 1" display="inline"><semantics><mrow><mi>β</mi><mo mathvariant="normal">≥</mo><mn mathvariant="normal">1</mn></mrow><annotation encoding="application/x-tex">\beta\geq 1</annotation></semantics></math> such that <math id="S0.Thmtheorem2.p1.m3" class="ltx_Math" alttext="\log_{\omega}(\alpha)+1\geq\beta" display="inline"><semantics><mrow><mrow><mrow><msub><mi mathvariant="normal">log</mi><mi>ω</mi></msub><mo mathvariant="italic">⁡</mo><mrow><mo mathvariant="normal" stretchy="false">(</mo><mi>α</mi><mo mathvariant="normal" stretchy="false">)</mo></mrow></mrow><mo mathvariant="normal">+</mo><mn mathvariant="normal">1</mn></mrow><mo mathvariant="normal">≥</mo><mi>β</mi></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)+1\geq\beta</annotation></semantics></math> we have</span></p>
<table id="S0.Ex13" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex13.m1" class="ltx_Math" alttext="{\gamma(\alpha+\omega^{\beta})}=\gamma(\alpha)+\omega^{\log_{\omega}(\alpha)+\beta}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><msup><mi>ω</mi><mi>β</mi></msup></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>β</mi></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha+\omega^{\beta})}=\gamma(\alpha)+\omega^{\log_{\omega}(\alpha)+\beta}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p7" class="ltx_para">
<p class="ltx_p">We prove by induction on <math id="p7.m1" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math> that for all such <math id="p7.m2" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>
the expression is true. We just verified <math id="p7.m3" class="ltx_Math" alttext="\beta=1" display="inline"><semantics><mrow><mi>β</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\beta=1</annotation></semantics></math> and the
limit case is obvious by continuity of <math id="p7.m4" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> and of the sum/exponentiation
in the second variable. For the successor step, if
<math id="p7.m5" class="ltx_Math" alttext="\log_{\omega}(\alpha)+1\geq\beta+1" display="inline"><semantics><mrow><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mn>1</mn></mrow><mo>≥</mo><mrow><mi>β</mi><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)+1\geq\beta+1</annotation></semantics></math> then
a fortiori
<math id="p7.m6" class="ltx_Math" alttext="\forall 1\leq n&lt;\omega,\log_{\omega}(\alpha+\omega^{\beta}\cdot n)+1\geq\beta+%
1\geq\beta" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mn>1</mn></mrow><mo>≤</mo><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><mo>,</mo><mrow><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mo>⋅</mo><mi>n</mi></mrow></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mn>1</mn></mrow><mo>≥</mo><mrow><mi>β</mi><mo>+</mo><mn>1</mn></mrow><mo>≥</mo><mi>β</mi></mrow></mrow><annotation encoding="application/x-tex">\forall 1\leq n&lt;\omega,\log_{\omega}(\alpha+\omega^{\beta}\cdot n)+1\geq\beta+%
1\geq\beta</annotation></semantics></math>.
We can then use the induction hypothesis to prove by induction on
<math id="p7.m7" class="ltx_Math" alttext="1\leq n&lt;\omega" display="inline"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">1\leq n&lt;\omega</annotation></semantics></math> that
<math id="p7.m8" class="ltx_Math" alttext="{\gamma(\alpha+{\omega^{\beta}\cdot n})}=\gamma(\alpha)+\omega^{\log_{\omega}(%
\alpha)+\beta}\cdot n" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mo>⋅</mo><mi>n</mi></mrow></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><msup><mi>ω</mi><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>β</mi></mrow></msup><mo>⋅</mo><mi>n</mi></mrow></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha+{\omega^{\beta}\cdot n})}=\gamma(\alpha)+\omega^{\log_{\omega}(%
\alpha)+\beta}\cdot n</annotation></semantics></math>. For <math id="p7.m9" class="ltx_Math" alttext="n=1" display="inline"><semantics><mrow><mi>n</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n=1</annotation></semantics></math>, this is
just the induction hypothesis of <math id="p7.m10" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math> (for the same <math id="p7.m11" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>!). For the
successor step, we need to use the induction hypothesis of <math id="p7.m12" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math>
(for <math id="p7.m13" class="ltx_Math" alttext="\alpha+\omega^{\beta}\cdot n" display="inline"><semantics><mrow><mi>α</mi><mo>+</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mo>⋅</mo><mi>n</mi></mrow></mrow><annotation encoding="application/x-tex">\alpha+\omega^{\beta}\cdot n</annotation></semantics></math>) which is
<math id="p7.m14" class="ltx_Math" alttext="{\gamma(\alpha+{\omega^{\beta}\cdot{(n+1)}})}={\gamma(\alpha+{\omega^{\beta}%
\cdot n})}+\omega^{\log_{\omega}(\alpha)+\beta}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mo>⋅</mo><mi>n</mi></mrow></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>β</mi></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha+{\omega^{\beta}\cdot{(n+1)}})}={\gamma(\alpha+{\omega^{\beta}%
\cdot n})}+\omega^{\log_{\omega}(\alpha)+\beta}</annotation></semantics></math>.
Finally,
<math id="p7.m15" class="ltx_Math" alttext="{\gamma(\alpha+{\omega^{\beta+1}})}={\sup_{1\leq n&lt;\omega}{\gamma(\alpha+{%
\omega^{\beta}\cdot n})}}=\gamma(\alpha)+\omega^{\log_{\omega}(\alpha)+\beta+1}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><msup><mi>ω</mi><mrow><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msub><mo>sup</mo><mrow><mn>1</mn><mo>≤</mo><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></msub><mo>⁡</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mo>⋅</mo><mi>n</mi></mrow></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha+{\omega^{\beta+1}})}={\sup_{1\leq n&lt;\omega}{\gamma(\alpha+{%
\omega^{\beta}\cdot n})}}=\gamma(\alpha)+\omega^{\log_{\omega}(\alpha)+\beta+1}</annotation></semantics></math>, as wanted.
∎</p>
</div>
</div>
<div id="p8" class="ltx_para">
<p class="ltx_p">For all <math id="p8.m1" class="ltx_Math" alttext="\alpha\geq 1" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\alpha\geq 1</annotation></semantics></math>,
<math id="p8.m2" class="ltx_Math" alttext="\log_{\omega}(\omega^{\alpha})+1=\alpha+1" display="inline"><semantics><mrow><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mi>α</mi></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mn>1</mn></mrow><mo>=</mo><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\omega^{\alpha})+1=\alpha+1</annotation></semantics></math> so the previous
paragraph also gives
<math id="p8.m3" class="ltx_Math" alttext="{\gamma(\omega^{\alpha+1})}=\gamma\left(\omega^{\alpha}+\omega^{\alpha+1}%
\right)={\gamma(\omega^{\alpha})}+\omega^{\alpha\cdot 2+1}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo>(</mo><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>+</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow><mo>)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mi>α</mi></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mn>1</mn></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\alpha+1})}=\gamma\left(\omega^{\alpha}+\omega^{\alpha+1}%
\right)={\gamma(\omega^{\alpha})}+\omega^{\alpha\cdot 2+1}</annotation></semantics></math>.
Then, we find</p>
<table id="S0.Ex14" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex14.m1" class="ltx_Math" alttext="\gamma(\omega^{2})=\omega+\omega^{3}=\omega^{3}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mn>2</mn></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>ω</mi><mo>+</mo><msup><mi>ω</mi><mn>3</mn></msup></mrow><mo>=</mo><msup><mi>ω</mi><mn>3</mn></msup></mrow><annotation encoding="application/x-tex">\gamma(\omega^{2})=\omega+\omega^{3}=\omega^{3}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<table id="S0.Ex15" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex15.m1" class="ltx_Math" alttext="\gamma(\omega^{3})=\omega^{3}+\omega^{5}=\omega^{5}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mn>3</mn></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mn>3</mn></msup><mo>+</mo><msup><mi>ω</mi><mn>5</mn></msup></mrow><mo>=</mo><msup><mi>ω</mi><mn>5</mn></msup></mrow><annotation encoding="application/x-tex">\gamma(\omega^{3})=\omega^{3}+\omega^{5}=\omega^{5}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">And more generally by induction on <math id="p8.m4" class="ltx_Math" alttext="n&lt;\omega" display="inline"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">n&lt;\omega</annotation></semantics></math>, we can show that</p>
<table id="S0.Ex16" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex16.m1" class="ltx_Math" alttext="\gamma(\omega^{n+1})=\omega^{2n+1}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mn>1</mn></mrow></msup></mrow><annotation encoding="application/x-tex">\gamma(\omega^{n+1})=\omega^{2n+1}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">Then we deduce another fixed point</p>
<table id="S0.Ex17" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex17.m1" class="ltx_Math" alttext="\gamma(\omega^{\omega})={\sup_{1\leq n&lt;\omega}\gamma\left({\omega^{n}}\right)}%
=\omega^{\omega}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mi>ω</mi></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><munder><mo movablelimits="false">sup</mo><mrow><mn>1</mn><mo>≤</mo><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></munder><mo>⁡</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo>(</mo><msup><mi>ω</mi><mi>n</mi></msup><mo>)</mo></mrow></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mi>ω</mi></msup></mrow><annotation encoding="application/x-tex">\gamma(\omega^{\omega})={\sup_{1\leq n&lt;\omega}\gamma\left({\omega^{n}}\right)}%
=\omega^{\omega}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">The following proposition tries to generalize the expression of
<math id="p8.m5" class="ltx_Math" alttext="{\gamma(\omega^{\alpha+1})}" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\alpha+1})}</annotation></semantics></math>.</p>
</div>
<div id="S0.Thmtheorem3" class="ltx_theorem ltx_theorem_proposition">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Proposition 0.3</span>.</h6>
<div id="S0.Thmtheorem3.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">For any <math id="S0.Thmtheorem3.p1.m1" class="ltx_Math" alttext="\alpha,\beta\geq 1" display="inline"><semantics><mrow><mrow><mi>α</mi><mo mathvariant="normal">,</mo><mi>β</mi></mrow><mo mathvariant="normal">≥</mo><mn mathvariant="normal">1</mn></mrow><annotation encoding="application/x-tex">\alpha,\beta\geq 1</annotation></semantics></math> such that
<math id="S0.Thmtheorem3.p1.m2" class="ltx_Math" alttext="\log_{\omega}(\alpha)&gt;\log_{\omega}(\beta)" display="inline"><semantics><mrow><mrow><msub><mi mathvariant="normal">log</mi><mi>ω</mi></msub><mo mathvariant="italic">⁡</mo><mrow><mo mathvariant="normal" stretchy="false">(</mo><mi>α</mi><mo mathvariant="normal" stretchy="false">)</mo></mrow></mrow><mo mathvariant="normal">&gt;</mo><mrow><msub><mi mathvariant="normal">log</mi><mi>ω</mi></msub><mo mathvariant="italic">⁡</mo><mrow><mo mathvariant="normal" stretchy="false">(</mo><mi>β</mi><mo mathvariant="normal" stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)&gt;\log_{\omega}(\beta)</annotation></semantics></math> we have</span></p>
<table id="S0.Ex18" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex18.m1" class="ltx_Math" alttext="{\gamma(\omega^{\alpha+\beta})}={\gamma(\omega^{\alpha})}+\omega^{\alpha\cdot 2%
+\beta}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mi>β</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mi>α</mi></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\alpha+\beta})}={\gamma(\omega^{\alpha})}+\omega^{\alpha\cdot 2%
+\beta}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p9" class="ltx_para">
<p class="ltx_p">This is done
by induction on <math id="p9.m1" class="ltx_Math" alttext="\beta&lt;\alpha" display="inline"><semantics><mrow><mi>β</mi><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beta&lt;\alpha</annotation></semantics></math> for a fixed <math id="p9.m2" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>. We already verified
the case <math id="p9.m3" class="ltx_Math" alttext="\beta=1" display="inline"><semantics><mrow><mi>β</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\beta=1</annotation></semantics></math> in the previous paragraph and the limit case is obvious
by continuity of <math id="p9.m4" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> and of the sum/exponentiation in the second variable.
For the successor step, we have
<math id="p9.m5" class="ltx_Math" alttext="{\gamma(\omega^{\alpha+\beta+1})}={\gamma(\omega^{\alpha+\beta})}+\omega^{{(%
\alpha+\beta)}\cdot 2+1}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mi>β</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>β</mi></mrow><mo stretchy="false">)</mo></mrow><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mn>1</mn></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\alpha+\beta+1})}={\gamma(\omega^{\alpha+\beta})}+\omega^{{(%
\alpha+\beta)}\cdot 2+1}</annotation></semantics></math> and by induction
hypothesis, <math id="p9.m6" class="ltx_Math" alttext="{\gamma(\omega^{\alpha+\beta})}={\gamma(\omega^{\alpha})}+\omega^{\alpha\cdot 2%
+\beta}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mi>β</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mi>α</mi></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\alpha+\beta})}={\gamma(\omega^{\alpha})}+\omega^{\alpha\cdot 2%
+\beta}</annotation></semantics></math>.
Since <math id="p9.m7" class="ltx_Math" alttext="\log_{\omega}(\alpha)&gt;\log_{\omega}(\beta+1)=\log_{\omega}(\beta)" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&gt;</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mrow><mi>β</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>β</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)&gt;\log_{\omega}(\beta+1)=\log_{\omega}(\beta)</annotation></semantics></math> we have
<math id="p9.m8" class="ltx_Math" alttext="{(\alpha+\beta)}\cdot 2+1=\alpha+\beta+\alpha+\beta+1=\alpha\cdot 2+\beta+1&gt;%
\alpha\cdot 2+\beta" display="inline"><semantics><mrow><mrow><mrow><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>β</mi></mrow><mo stretchy="false">)</mo></mrow><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mn>1</mn></mrow><mo>=</mo><mrow><mi>α</mi><mo>+</mo><mi>β</mi><mo>+</mo><mi>α</mi><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow><mo>=</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow><mo>&gt;</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi></mrow></mrow><annotation encoding="application/x-tex">{(\alpha+\beta)}\cdot 2+1=\alpha+\beta+\alpha+\beta+1=\alpha\cdot 2+\beta+1&gt;%
\alpha\cdot 2+\beta</annotation></semantics></math> and so
<math id="p9.m9" class="ltx_Math" alttext="\omega^{\alpha\cdot 2+\beta}+\omega^{\alpha\cdot 2+\beta+1}=\omega^{\alpha%
\cdot 2+\beta+1}" display="inline"><semantics><mrow><mrow><msup><mi>ω</mi><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi></mrow></msup><mo>+</mo><msup><mi>ω</mi><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow><mo>=</mo><msup><mi>ω</mi><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow><annotation encoding="application/x-tex">\omega^{\alpha\cdot 2+\beta}+\omega^{\alpha\cdot 2+\beta+1}=\omega^{\alpha%
\cdot 2+\beta+1}</annotation></semantics></math>.
Finally, <math id="p9.m10" class="ltx_Math" alttext="{\gamma(\omega^{\alpha+\beta+1})}={\gamma(\omega^{\alpha+\beta})}+\omega^{%
\alpha\cdot 2+\beta+1}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mi>β</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>+</mo><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\alpha+\beta+1})}={\gamma(\omega^{\alpha+\beta})}+\omega^{%
\alpha\cdot 2+\beta+1}</annotation></semantics></math> as wanted.
∎</p>
</div>
</div>
<div id="p10" class="ltx_para">
<p class="ltx_p">For any <math id="p10.m1" class="ltx_Math" alttext="1\leq n&lt;\omega" display="inline"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">1\leq n&lt;\omega</annotation></semantics></math>
and <math id="p10.m2" class="ltx_Math" alttext="\alpha\geq 1" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\alpha\geq 1</annotation></semantics></math>, if <math id="p10.m3" class="ltx_Math" alttext="1\leq\beta&lt;\omega^{\alpha}" display="inline"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>β</mi><mo>&lt;</mo><msup><mi>ω</mi><mi>α</mi></msup></mrow><annotation encoding="application/x-tex">1\leq\beta&lt;\omega^{\alpha}</annotation></semantics></math>
then <math id="p10.m4" class="ltx_Math" alttext="\log_{\omega}(\beta)&lt;\alpha=\log_{\omega}(\omega^{\alpha}\cdot n)" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>β</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mi>α</mi><mo>=</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\beta)&lt;\alpha=\log_{\omega}(\omega^{\alpha}\cdot n)</annotation></semantics></math>. Hence
proposition <a href="#S0.Thmtheorem3" title="Proposition 0.3. ‣ The canonical well-ordering of ×αα (part 2)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.3</span></a> gives
<math id="p10.m5" class="ltx_Math" alttext="{\gamma(\omega^{{\omega^{\alpha}\cdot n}+\beta})}={\gamma(\omega^{{\omega^{%
\alpha}\cdot n}})}+\omega^{{\omega^{\alpha}\cdot{2n}}+\beta}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow><mo>+</mo><mi>β</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi>β</mi></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{{\omega^{\alpha}\cdot n}+\beta})}={\gamma(\omega^{{\omega^{%
\alpha}\cdot n}})}+\omega^{{\omega^{\alpha}\cdot{2n}}+\beta}</annotation></semantics></math>
Then by continuity of <math id="p10.m6" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> and of the sum/exponentiation in the second
variable, we can consider the limit <math id="p10.m7" class="ltx_Math" alttext="\beta\rightarrow\omega^{\alpha}" display="inline"><semantics><mrow><mi>β</mi><mo>→</mo><msup><mi>ω</mi><mi>α</mi></msup></mrow><annotation encoding="application/x-tex">\beta\rightarrow\omega^{\alpha}</annotation></semantics></math> to get
<math id="p10.m8" class="ltx_Math" alttext="{\gamma(\omega^{{\omega^{\alpha}\cdot(n+1)}})}={\gamma(\omega^{{\omega^{\alpha%
}\cdot n}})}+\omega^{{\omega^{\alpha}\cdot{(2n+1)}}}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{{\omega^{\alpha}\cdot(n+1)}})}={\gamma(\omega^{{\omega^{\alpha%
}\cdot n}})}+\omega^{{\omega^{\alpha}\cdot{(2n+1)}}}</annotation></semantics></math>.
So continuing our calculation we have</p>
<table id="S0.Ex19" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex19.m1" class="ltx_Math" alttext="{\gamma(\omega^{\omega\cdot 2})}=\omega^{\omega}+\omega^{\omega\cdot 3}=\omega%
^{\omega\cdot 3}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>ω</mi><mo>⋅</mo><mn>2</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mi>ω</mi></msup><mo>+</mo><msup><mi>ω</mi><mrow><mi>ω</mi><mo>⋅</mo><mn>3</mn></mrow></msup></mrow><mo>=</mo><msup><mi>ω</mi><mrow><mi>ω</mi><mo>⋅</mo><mn>3</mn></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\omega\cdot 2})}=\omega^{\omega}+\omega^{\omega\cdot 3}=\omega%
^{\omega\cdot 3}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<table id="S0.Ex20" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex20.m1" class="ltx_Math" alttext="{\gamma(\omega^{\omega\cdot 3})}=\omega^{\omega\cdot 3}+\omega^{\omega\cdot 5}%
=\omega^{\omega\cdot 5}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><mi>ω</mi><mo>⋅</mo><mn>3</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><mi>ω</mi><mo>⋅</mo><mn>3</mn></mrow></msup><mo>+</mo><msup><mi>ω</mi><mrow><mi>ω</mi><mo>⋅</mo><mn>5</mn></mrow></msup></mrow><mo>=</mo><msup><mi>ω</mi><mrow><mi>ω</mi><mo>⋅</mo><mn>5</mn></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\omega\cdot 3})}=\omega^{\omega\cdot 3}+\omega^{\omega\cdot 5}%
=\omega^{\omega\cdot 5}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">and taking the limit we find another fixed point</p>
<table id="S0.Ex21" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex21.m1" class="ltx_Math" alttext="{\gamma(\omega^{\omega^{2}})}=\omega^{\omega^{2}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msup><mi>ω</mi><mn>2</mn></msup></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><msup><mi>ω</mi><mn>2</mn></msup></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\omega^{2}})}=\omega^{\omega^{2}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">then again</p>
<table id="S0.Ex22" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex22.m1" class="ltx_Math" alttext="{\gamma(\omega^{\omega^{2}\cdot 2})}=\omega^{\omega^{2}}+\omega^{\omega^{2}%
\cdot 3}=\omega^{\omega^{2}\cdot 3}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mn>2</mn></msup><mo>⋅</mo><mn>2</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><msup><mi>ω</mi><mn>2</mn></msup></msup><mo>+</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mn>2</mn></msup><mo>⋅</mo><mn>3</mn></mrow></msup></mrow><mo>=</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mn>2</mn></msup><mo>⋅</mo><mn>3</mn></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\omega^{2}\cdot 2})}=\omega^{\omega^{2}}+\omega^{\omega^{2}%
\cdot 3}=\omega^{\omega^{2}\cdot 3}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<table id="S0.Ex23" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex23.m1" class="ltx_Math" alttext="{\gamma(\omega^{\omega^{2}\cdot 3})}=\omega^{\omega^{2}\cdot 3}+\omega^{\omega%
^{2}\cdot 5}=\omega^{\omega^{2}\cdot 5}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mn>2</mn></msup><mo>⋅</mo><mn>3</mn></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mn>2</mn></msup><mo>⋅</mo><mn>3</mn></mrow></msup><mo>+</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mn>2</mn></msup><mo>⋅</mo><mn>5</mn></mrow></msup></mrow><mo>=</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mn>2</mn></msup><mo>⋅</mo><mn>5</mn></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\omega^{2}\cdot 3})}=\omega^{\omega^{2}\cdot 3}+\omega^{\omega%
^{2}\cdot 5}=\omega^{\omega^{2}\cdot 5}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">and taking the limit we find another fixed point</p>
<table id="S0.Ex24" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex24.m1" class="ltx_Math" alttext="{\gamma(\omega^{\omega^{3}})}=\omega^{\omega^{3}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msup><mi>ω</mi><mn>3</mn></msup></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><msup><mi>ω</mi><mn>3</mn></msup></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\omega^{3}})}=\omega^{\omega^{3}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">More generally, we have the following proposition:</p>
</div>
<div id="S0.Thmtheorem4" class="ltx_theorem ltx_theorem_proposition">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Proposition 0.4</span>.</h6>
<div id="S0.Thmtheorem4.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">For any ordinal <math id="S0.Thmtheorem4.p1.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> and <math id="S0.Thmtheorem4.p1.m2" class="ltx_Math" alttext="1\leq n&lt;\omega" display="inline"><semantics><mrow><mn mathvariant="normal">1</mn><mo mathvariant="normal">≤</mo><mi>n</mi><mo mathvariant="normal">&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">1\leq n&lt;\omega</annotation></semantics></math> we have</span></p>
<table id="S0.Ex25" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex25.m1" class="ltx_Math" alttext="{\gamma(\omega^{{\omega^{\alpha}\cdot n}})}=\omega^{{\omega^{\alpha}\cdot{(2n-%
1)}}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{{\omega^{\alpha}\cdot n}})}=\omega^{{\omega^{\alpha}\cdot{(2n-%
1)}}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p11" class="ltx_para">
<p class="ltx_p">From the relation <math id="p11.m1" class="ltx_Math" alttext="{\gamma(\omega^{{\omega^{\alpha}\cdot(n+1)}})}={\gamma(\omega^{{\omega^{\alpha%
}\cdot n}})}+\omega^{{\omega^{\alpha}\cdot{(2n+1)}}}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{{\omega^{\alpha}\cdot(n+1)}})}={\gamma(\omega^{{\omega^{\alpha%
}\cdot n}})}+\omega^{{\omega^{\alpha}\cdot{(2n+1)}}}</annotation></semantics></math>,
we deduce by induction on <math id="p11.m2" class="ltx_Math" alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math> that</p>
<table id="S0.Ex26" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex26.m1" class="ltx_Math" alttext="\forall n\geq 2,{\gamma(\omega^{{\omega^{\alpha}\cdot n}})}={\gamma(\omega^{{%
\omega^{\alpha}}})}+\omega^{{\omega^{\alpha}\cdot{(2n-1)}}}" display="block"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>n</mi></mrow><mo>≥</mo><mn>2</mn></mrow><mo>,</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall n\geq 2,{\gamma(\omega^{{\omega^{\alpha}\cdot n}})}={\gamma(\omega^{{%
\omega^{\alpha}}})}+\omega^{{\omega^{\alpha}\cdot{(2n-1)}}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">Taking the limit <math id="p11.m3" class="ltx_Math" alttext="n\rightarrow\omega" display="inline"><semantics><mrow><mi>n</mi><mo>→</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">n\rightarrow\omega</annotation></semantics></math>,we obtain</p>
<table id="S0.Ex27" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex27.m1" class="ltx_Math" alttext="{\gamma(\omega^{{\omega^{\alpha+1}}})}={\gamma(\omega^{{\omega^{\alpha}}})}+%
\omega^{{\omega^{\alpha+1}}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msup></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><msup><mi>ω</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msup></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{{\omega^{\alpha+1}}})}={\gamma(\omega^{{\omega^{\alpha}}})}+%
\omega^{{\omega^{\alpha+1}}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p12" class="ltx_para">
<p class="ltx_p">We can then show by induction that all the
<math id="p12.m1" class="ltx_Math" alttext="\omega^{\omega^{\alpha}}" display="inline"><semantics><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><annotation encoding="application/x-tex">\omega^{\omega^{\alpha}}</annotation></semantics></math> are actually fixed points, using the previous
relation at successor step, the continuity of <math id="p12.m2" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> at limit step
and the fact that <math id="p12.m3" class="ltx_Math" alttext="\gamma(\omega)=\omega" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>ω</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\gamma(\omega)=\omega</annotation></semantics></math>. This means</p>
</div>
<div id="p13" class="ltx_para">
<table id="S0.Ex28" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex28.m1" class="ltx_Math" alttext="{\gamma(\omega^{{\omega^{\alpha}}})}=\omega^{{\omega^{\alpha}}}=\omega^{{%
\omega^{\alpha}\cdot{(2\times 1-1)}}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><mo>=</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>×</mo><mn>1</mn></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{{\omega^{\alpha}}})}=\omega^{{\omega^{\alpha}}}=\omega^{{%
\omega^{\alpha}\cdot{(2\times 1-1)}}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p14" class="ltx_para">
<p class="ltx_p">Then for <math id="p14.m1" class="ltx_Math" alttext="n\geq 2" display="inline"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>2</mn></mrow><annotation encoding="application/x-tex">n\geq 2</annotation></semantics></math>, we get</p>
<table id="S0.Ex29" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex29.m1" class="ltx_Math" alttext="{\gamma(\omega^{{\omega^{\alpha}\cdot n}})}={\gamma(\omega^{{\omega^{\alpha}}}%
)}+\omega^{{\omega^{\alpha}\cdot{(2n-1)}}}={\omega^{{\omega^{\alpha}}}}+\omega%
^{{\omega^{\alpha}\cdot{(2n-1)}}}=\omega^{{\omega^{\alpha}\cdot{(2n-1)}}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mi>n</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow><mo>=</mo><mrow><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><mo>+</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow><mo>=</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>α</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>n</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{{\omega^{\alpha}\cdot n}})}={\gamma(\omega^{{\omega^{\alpha}}}%
)}+\omega^{{\omega^{\alpha}\cdot{(2n-1)}}}={\omega^{{\omega^{\alpha}}}}+\omega%
^{{\omega^{\alpha}\cdot{(2n-1)}}}=\omega^{{\omega^{\alpha}\cdot{(2n-1)}}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p15" class="ltx_para">
<p class="ltx_p">∎</p>
</div>
</div>
<div id="p16" class="ltx_para">
<p class="ltx_p">Equipped with these four propositions, we have a way to recursively calculate
<math id="p16.m1" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>. We are ready to prove the main theorem:</p>
</div>
<div id="S0.Thmtheorem5" class="ltx_theorem ltx_theorem_theorem">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Theorem 0.5</span>.</h6>
<div id="S0.Thmtheorem5.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">For all ordinal <math id="S0.Thmtheorem5.p1.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>, we denote <math id="S0.Thmtheorem5.p1.m2" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo mathvariant="italic">⁢</mo><mrow><mo mathvariant="normal" stretchy="false">(</mo><mi>α</mi><mo mathvariant="normal" stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math> the order-type of
the canonical ordering of <math id="S0.Thmtheorem5.p1.m3" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo mathvariant="normal">×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math>. Then <math id="S0.Thmtheorem5.p1.m4" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> can be
calculated as follows:</span></p>
<ol id="I1" class="ltx_enumerate">
<li id="I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">1.</span></span> 
<div id="I1.i1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Finite Ordinals:
For any </span><math id="I1.i1.p1.m1" class="ltx_Math" alttext="n&lt;\omega" display="inline"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">n&lt;\omega</annotation></semantics></math><span class="ltx_text ltx_font_italic"> we have</span></p>
<table id="S0.Ex30" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex30.m1" class="ltx_Math" alttext="\gamma(n)=n^{2}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>n</mi><mn>2</mn></msup></mrow><annotation encoding="application/x-tex">\gamma(n)=n^{2}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</li>
<li id="I1.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">2.</span></span> 
<div id="I1.i2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Limit Ordinals:
For any limit ordinal </span><math id="I1.i2.p1.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math><span class="ltx_text ltx_font_italic">,</span></p>
<ol id="I1.I1" class="ltx_enumerate">
<li id="I1.I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">(a)</span></span> 
<div id="I1.I1.i1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">If </span><math id="I1.I1.i1.p1.m1" class="ltx_Math" alttext="\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)\right)}" display="inline"><semantics><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mi>α</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></msup><annotation encoding="application/x-tex">\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)\right)}</annotation></semantics></math><span class="ltx_text ltx_font_italic"> does not
divide </span><math id="I1.I1.i1.p1.m2" class="ltx_Math" alttext="\log_{\omega}(\alpha)" display="inline"><semantics><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)</annotation></semantics></math><span class="ltx_text ltx_font_italic"> then</span></p>
<table id="S0.Ex31" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex31.m1" class="ltx_Math" alttext="\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\alpha" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mi>α</mi></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\alpha</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</li>
<li id="I1.I1.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">(b)</span></span> 
<div id="I1.I1.i2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Otherwise, we write
</span><math id="I1.I1.i2.p1.m1" class="ltx_Math" alttext="\alpha={\omega^{\log_{\omega}(\alpha)}n}+\rho" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi>ρ</mi></mrow></mrow><annotation encoding="application/x-tex">\alpha={\omega^{\log_{\omega}(\alpha)}n}+\rho</annotation></semantics></math><span class="ltx_text ltx_font_italic"> for some </span><math id="I1.I1.i2.p1.m2" class="ltx_Math" alttext="n\geq 1" display="inline"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n\geq 1</annotation></semantics></math><span class="ltx_text ltx_font_italic">. If
</span><math id="I1.I1.i2.p1.m3" class="ltx_Math" alttext="n\geq 2" display="inline"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>2</mn></mrow><annotation encoding="application/x-tex">n\geq 2</annotation></semantics></math><span class="ltx_text ltx_font_italic"> then</span></p>
<table id="S0.Ex32" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex32.m1" class="ltx_Math" alttext="\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\left({\omega^{\log_{\omega}%
(\alpha)}\cdot{(n-1)}}+\rho\right)" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mrow><mo>(</mo><mrow><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>ρ</mi></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\left({\omega^{\log_{\omega}%
(\alpha)}\cdot{(n-1)}}+\rho\right)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p"><span class="ltx_text ltx_font_italic">(like the first case but we “decrement </span><math id="I1.I1.i2.p1.m4" class="ltx_Math" alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math><span class="ltx_text ltx_font_italic"> in the second factor”)</span></p>
</div>
</li>
<li id="I1.I1.i3" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">(c)</span></span> 
<div id="I1.I1.i3.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Otherwise, </span><math id="I1.I1.i3.p1.m1" class="ltx_Math" alttext="\alpha={\omega^{\log_{\omega}(\alpha)}}+\rho" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>+</mo><mi>ρ</mi></mrow></mrow><annotation encoding="application/x-tex">\alpha={\omega^{\log_{\omega}(\alpha)}}+\rho</annotation></semantics></math><span class="ltx_text ltx_font_italic"> and
we write </span><math id="I1.I1.i3.p1.m2" class="ltx_Math" alttext="\log_{\omega}(\alpha)=\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha%
\right)\right)}m" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mi>α</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></msup><mo>⁢</mo><mi>m</mi></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)=\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha%
\right)\right)}m</annotation></semantics></math><span class="ltx_text ltx_font_italic">
for some </span><math id="I1.I1.i3.p1.m3" class="ltx_Math" alttext="m\geq 1" display="inline"><semantics><mrow><mi>m</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">m\geq 1</annotation></semantics></math><span class="ltx_text ltx_font_italic">. We have</span></p>
<table id="S0.Ex33" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex33.m1" class="ltx_Math" alttext="\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\left(\omega^{\omega^{\log_{%
\omega}\left(\log_{\omega}\left(\alpha\right)\right)}\cdot\left(m-1\right)}+%
\rho\right)" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mrow><mo>(</mo><mrow><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mi>α</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></msup><mo>⋅</mo><mrow><mo>(</mo><mrow><mi>m</mi><mo>-</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow></msup><mo>+</mo><mi>ρ</mi></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\left(\omega^{\omega^{\log_{%
\omega}\left(\log_{\omega}\left(\alpha\right)\right)}\cdot\left(m-1\right)}+%
\rho\right)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p"><span class="ltx_text ltx_font_italic">(like the first case but we “decrement </span><math id="I1.I1.i3.p1.m4" class="ltx_Math" alttext="m" display="inline"><semantics><mi>m</mi><annotation encoding="application/x-tex">m</annotation></semantics></math><span class="ltx_text ltx_font_italic"> in the second factor”)</span></p>
</div>
</li>
</ol>
</div>
</li>
<li id="I1.i3" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">3.</span></span> 
<div id="I1.i3.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Infinite Successor Ordinals:
For any limit ordinal </span><math id="I1.i3.p1.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math><span class="ltx_text ltx_font_italic"> and </span><math id="I1.i3.p1.m2" class="ltx_Math" alttext="1\leq n&lt;\omega" display="inline"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">1\leq n&lt;\omega</annotation></semantics></math><span class="ltx_text ltx_font_italic"> we have</span></p>
<table id="S0.Ex34" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex34.m1" class="ltx_Math" alttext="\gamma(\alpha+n)=\gamma(\alpha)+{\alpha\cdot{2n}}+n" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+n)=\gamma(\alpha)+{\alpha\cdot{2n}}+n</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p"><span class="ltx_text ltx_font_italic">where </span><math id="I1.i3.p1.m3" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math><span class="ltx_text ltx_font_italic"> is determined as in the previous point.</span></p>
</div>
</li>
</ol>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p17" class="ltx_para">
<p class="ltx_p">The “Finite Ordinals” has been discussed at the beginning and the
“Infinite Successor Ordinals” is proposition <a href="#S0.Thmtheorem1" title="Proposition 0.1. ‣ The canonical well-ordering of ×αα (part 2)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.1</span></a>.
Now let’s consider the Cantor Normal Form
<math id="p17.m1" class="ltx_Math" alttext="\omega^{\beta_{1}}n+...+\omega^{\beta_{k}}n_{k}" display="inline"><semantics><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi mathvariant="normal">…</mi><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mi>k</mi></msub></msup><mo>⁢</mo><msub><mi>n</mi><mi>k</mi></msub></mrow></mrow><annotation encoding="application/x-tex">\omega^{\beta_{1}}n+...+\omega^{\beta_{k}}n_{k}</annotation></semantics></math> of a limit ordinal
<math id="p17.m2" class="ltx_Math" alttext="\alpha\geq\omega" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\alpha\geq\omega</annotation></semantics></math> (so <math id="p17.m3" class="ltx_Math" alttext="\beta_{k}\geq 1" display="inline"><semantics><mrow><msub><mi>β</mi><mi>k</mi></msub><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\beta_{k}\geq 1</annotation></semantics></math> and
<math id="p17.m4" class="ltx_Math" alttext="\beta_{1}=\log_{\omega}(\alpha)" display="inline"><semantics><mrow><msub><mi>β</mi><mn>1</mn></msub><mo>=</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\beta_{1}=\log_{\omega}(\alpha)</annotation></semantics></math>). First,
from proposition <a href="#S0.Thmtheorem2" title="Proposition 0.2. ‣ The canonical well-ordering of ×αα (part 2)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.2</span></a> we can make successively
extract the <math id="p17.m5" class="ltx_Math" alttext="n_{k}" display="inline"><semantics><msub><mi>n</mi><mi>k</mi></msub><annotation encoding="application/x-tex">n_{k}</annotation></semantics></math> terms <math id="p17.m6" class="ltx_Math" alttext="\omega^{\beta_{k}}" display="inline"><semantics><msup><mi>ω</mi><msub><mi>β</mi><mi>k</mi></msub></msup><annotation encoding="application/x-tex">\omega^{\beta_{k}}</annotation></semantics></math> (by left-multiplying them
by <math id="p17.m7" class="ltx_Math" alttext="\omega^{\beta_{1}}" display="inline"><semantics><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><annotation encoding="application/x-tex">\omega^{\beta_{1}}</annotation></semantics></math>), then the <math id="p17.m8" class="ltx_Math" alttext="n_{k-1}" display="inline"><semantics><msub><mi>n</mi><mrow><mi>k</mi><mo>-</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">n_{k-1}</annotation></semantics></math> terms <math id="p17.m9" class="ltx_Math" alttext="\omega^{\beta_{k-1}}" display="inline"><semantics><msup><mi>ω</mi><msub><mi>β</mi><mrow><mi>k</mi><mo>-</mo><mn>1</mn></mrow></msub></msup><annotation encoding="application/x-tex">\omega^{\beta_{k-1}}</annotation></semantics></math>, …
then the <math id="p17.m10" class="ltx_Math" alttext="n_{2}" display="inline"><semantics><msub><mi>n</mi><mn>2</mn></msub><annotation encoding="application/x-tex">n_{2}</annotation></semantics></math> terms <math id="p17.m11" class="ltx_Math" alttext="\omega^{\beta_{2}}" display="inline"><semantics><msup><mi>ω</mi><msub><mi>β</mi><mn>2</mn></msub></msup><annotation encoding="application/x-tex">\omega^{\beta_{2}}</annotation></semantics></math> and finally
<math id="p17.m12" class="ltx_Math" alttext="n-1" display="inline"><semantics><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n-1</annotation></semantics></math> terms <math id="p17.m13" class="ltx_Math" alttext="\omega^{\beta_{1}}" display="inline"><semantics><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><annotation encoding="application/x-tex">\omega^{\beta_{1}}</annotation></semantics></math>. We obtain:</p>
<table id="S0.Ex35" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex35.m1" class="ltx_Math" alttext="{\gamma(\alpha)}={\gamma(\omega^{\beta_{1}})}+{\omega^{\beta_{1}}\left(\omega^%
{\beta_{1}}{(n-1)}+\omega^{\beta_{2}}n_{2}+\dots+\omega^{\beta_{k}}n_{k}\right)}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo>(</mo><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>2</mn></msub></msup><mo>⁢</mo><msub><mi>n</mi><mn>2</mn></msub></mrow><mo>+</mo><mi mathvariant="normal">…</mi><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mi>k</mi></msub></msup><mo>⁢</mo><msub><mi>n</mi><mi>k</mi></msub></mrow></mrow><mo>)</mo></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha)}={\gamma(\omega^{\beta_{1}})}+{\omega^{\beta_{1}}\left(\omega^%
{\beta_{1}}{(n-1)}+\omega^{\beta_{2}}n_{2}+\dots+\omega^{\beta_{k}}n_{k}\right)}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p18" class="ltx_para">
<p class="ltx_p">We now write <math id="p18.m1" class="ltx_Math" alttext="\beta_{1}=\omega^{\delta}m+\sigma" display="inline"><semantics><mrow><msub><mi>β</mi><mn>1</mn></msub><mo>=</mo><mrow><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow><mo>+</mo><mi>σ</mi></mrow></mrow><annotation encoding="application/x-tex">\beta_{1}=\omega^{\delta}m+\sigma</annotation></semantics></math> where
<math id="p18.m2" class="ltx_Math" alttext="\delta=\log_{\omega}{\beta_{1}}" display="inline"><semantics><mrow><mi>δ</mi><mo>=</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><msub><mi>β</mi><mn>1</mn></msub></mrow></mrow><annotation encoding="application/x-tex">\delta=\log_{\omega}{\beta_{1}}</annotation></semantics></math> and <math id="p18.m3" class="ltx_Math" alttext="m,\sigma" display="inline"><semantics><mrow><mi>m</mi><mo>,</mo><mi>σ</mi></mrow><annotation encoding="application/x-tex">m,\sigma</annotation></semantics></math> are the quotient and remainder
of the Euclidean division of <math id="p18.m4" class="ltx_Math" alttext="\beta_{1}" display="inline"><semantics><msub><mi>β</mi><mn>1</mn></msub><annotation encoding="application/x-tex">\beta_{1}</annotation></semantics></math> by <math id="p18.m5" class="ltx_Math" alttext="\omega^{\delta}" display="inline"><semantics><msup><mi>ω</mi><mi>δ</mi></msup><annotation encoding="application/x-tex">\omega^{\delta}</annotation></semantics></math>. We can then use
proposition <a href="#S0.Thmtheorem3" title="Proposition 0.3. ‣ The canonical well-ordering of ×αα (part 2)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.3</span></a> to extract <math id="p18.m6" class="ltx_Math" alttext="\sigma" display="inline"><semantics><mi>σ</mi><annotation encoding="application/x-tex">\sigma</annotation></semantics></math>:</p>
<table id="S0.Ex36" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex36.m1" class="ltx_Math" alttext="\sigma=0\implies{\gamma(\omega^{\beta_{1}})}={\gamma(\omega^{\omega^{\delta}m})}" display="block"><semantics><mrow><mi>σ</mi><mo>=</mo><mn>0</mn><mo>⟹</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\sigma=0\implies{\gamma(\omega^{\beta_{1}})}={\gamma(\omega^{\omega^{\delta}m})}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<table id="S0.Ex37" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex37.m1" class="ltx_Math" alttext="\sigma\neq 0\implies{\gamma(\omega^{\beta_{1}})}={\gamma(\omega^{\omega^{%
\delta}m})}+\omega^{\omega^{\delta}\cdot{(2m)}+\sigma}" display="block"><semantics><mrow><mi>σ</mi><mo>≠</mo><mn>0</mn><mo>⟹</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><msup><mi>ω</mi><mrow><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>σ</mi></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">\sigma\neq 0\implies{\gamma(\omega^{\beta_{1}})}={\gamma(\omega^{\omega^{%
\delta}m})}+\omega^{\omega^{\delta}\cdot{(2m)}+\sigma}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p19" class="ltx_para">
<p class="ltx_p">Finally, using proposition <a href="#S0.Thmtheorem4" title="Proposition 0.4. ‣ The canonical well-ordering of ×αα (part 2)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.4</span></a> we obtain</p>
<table id="S0.Ex38" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex38.m1" class="ltx_Math" alttext="{\gamma(\omega^{\omega^{\delta}m})}=\omega^{{\omega^{\delta}\cdot{(2m-1)}}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\omega^{\delta}m})}=\omega^{{\omega^{\delta}\cdot{(2m-1)}}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p20" class="ltx_para">
<p class="ltx_p"><math id="p20.m1" class="ltx_Math" alttext="\sigma\neq 0" display="inline"><semantics><mrow><mi>σ</mi><mo>≠</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\sigma\neq 0</annotation></semantics></math> means that
<math id="p20.m2" class="ltx_Math" alttext="\omega^{\delta}=\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)%
\right)}" display="inline"><semantics><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>=</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mi>α</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></msup></mrow><annotation encoding="application/x-tex">\omega^{\delta}=\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)%
\right)}</annotation></semantics></math>
does not divide
<math id="p20.m3" class="ltx_Math" alttext="\beta_{1}={\log_{\omega}(\alpha)}" display="inline"><semantics><mrow><msub><mi>β</mi><mn>1</mn></msub><mo>=</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\beta_{1}={\log_{\omega}(\alpha)}</annotation></semantics></math>. In that case,
<math id="p20.m4" class="ltx_Math" alttext="\omega^{\omega^{\delta}\cdot{(2m)}+\sigma}&gt;\omega^{{\omega^{\delta}\cdot{(2m-1%
)}}}" display="inline"><semantics><mrow><msup><mi>ω</mi><mrow><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>σ</mi></mrow></msup><mo>&gt;</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow><annotation encoding="application/x-tex">\omega^{\omega^{\delta}\cdot{(2m)}+\sigma}&gt;\omega^{{\omega^{\delta}\cdot{(2m-1%
)}}}</annotation></semantics></math>
and so
<math id="p20.m5" class="ltx_Math" alttext="{\gamma(\omega^{\beta_{1}})}=\omega^{\omega^{\delta}\cdot{(2m)}+\sigma}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mrow><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>σ</mi></mrow></msup></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\beta_{1}})}=\omega^{\omega^{\delta}\cdot{(2m)}+\sigma}</annotation></semantics></math>.
We note that <math id="p20.m6" class="ltx_Math" alttext="\beta_{1}\cdot 2=\omega^{\delta}m+\sigma+\omega^{\delta}m+\sigma=\omega^{%
\delta}{(2m)}+\sigma" display="inline"><semantics><mrow><mrow><msub><mi>β</mi><mn>1</mn></msub><mo>⋅</mo><mn>2</mn></mrow><mo>=</mo><mrow><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow><mo>+</mo><mi>σ</mi><mo>+</mo><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow><mo>+</mo><mi>σ</mi></mrow><mo>=</mo><mrow><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>σ</mi></mrow></mrow><annotation encoding="application/x-tex">\beta_{1}\cdot 2=\omega^{\delta}m+\sigma+\omega^{\delta}m+\sigma=\omega^{%
\delta}{(2m)}+\sigma</annotation></semantics></math> since the remainder <math id="p20.m7" class="ltx_Math" alttext="\sigma" display="inline"><semantics><mi>σ</mi><annotation encoding="application/x-tex">\sigma</annotation></semantics></math> is less than
<math id="p20.m8" class="ltx_Math" alttext="\omega^{\delta}" display="inline"><semantics><msup><mi>ω</mi><mi>δ</mi></msup><annotation encoding="application/x-tex">\omega^{\delta}</annotation></semantics></math>. So actually <math id="p20.m9" class="ltx_Math" alttext="{\gamma(\omega^{\beta_{1}})}=\omega^{\beta_{1}}\omega^{\beta_{1}}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\beta_{1}})}=\omega^{\beta_{1}}\omega^{\beta_{1}}</annotation></semantics></math>. Coming back to the expression
of <math id="p20.m10" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math>, this term can be grouped with
<math id="p20.m11" class="ltx_Math" alttext="\omega^{\beta_{1}}{(n-1)}" display="inline"><semantics><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\omega^{\beta_{1}}{(n-1)}</annotation></semantics></math> to
recover the Cantor Normal Form of <math id="p20.m12" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> and
we finally get <math id="p20.m13" class="ltx_Math" alttext="\gamma(\alpha)=\omega^{\beta_{1}}\alpha" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mi>α</mi></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)=\omega^{\beta_{1}}\alpha</annotation></semantics></math>.</p>
</div>
<div id="p21" class="ltx_para">
<p class="ltx_p">Otherwise, <math id="p21.m1" class="ltx_Math" alttext="\sigma=0" display="inline"><semantics><mrow><mi>σ</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\sigma=0</annotation></semantics></math>, <math id="p21.m2" class="ltx_Math" alttext="\beta_{1}=\omega^{\delta}m" display="inline"><semantics><mrow><msub><mi>β</mi><mn>1</mn></msub><mo>=</mo><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow></mrow><annotation encoding="application/x-tex">\beta_{1}=\omega^{\delta}m</annotation></semantics></math> and</p>
<table id="S0.Ex39" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex39.m1" class="ltx_Math" alttext="{\gamma(\omega^{\beta_{1}})}={\gamma(\omega^{\omega^{\delta}m})}=\omega^{{%
\omega^{\delta}\cdot{(2m-1)}}}={\omega^{\beta_{1}}{\omega^{\omega^{\delta}%
\cdot{(m-1)}}}}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow></msup><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>m</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\beta_{1}})}={\gamma(\omega^{\omega^{\delta}m})}=\omega^{{%
\omega^{\delta}\cdot{(2m-1)}}}={\omega^{\beta_{1}}{\omega^{\omega^{\delta}%
\cdot{(m-1)}}}}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p22" class="ltx_para">
<p class="ltx_p">But then <math id="p22.m1" class="ltx_Math" alttext="\beta_{1}=\omega^{\delta}m&gt;{\omega^{\delta}{(m-1)}}" display="inline"><semantics><mrow><msub><mi>β</mi><mn>1</mn></msub><mo>=</mo><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mi>m</mi></mrow><mo>&gt;</mo><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>m</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\beta_{1}=\omega^{\delta}m&gt;{\omega^{\delta}{(m-1)}}</annotation></semantics></math> and so
<math id="p22.m2" class="ltx_Math" alttext="\omega^{\beta_{1}}\omega^{\beta_{1}}&gt;\omega^{\beta_{1}}\omega^{{\omega^{\delta%
}\cdot{(m-1)}}}" display="inline"><semantics><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup></mrow><mo>&gt;</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>m</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">\omega^{\beta_{1}}\omega^{\beta_{1}}&gt;\omega^{\beta_{1}}\omega^{{\omega^{\delta%
}\cdot{(m-1)}}}</annotation></semantics></math>. Hence if
<math id="p22.m3" class="ltx_Math" alttext="n\geq 2" display="inline"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>2</mn></mrow><annotation encoding="application/x-tex">n\geq 2</annotation></semantics></math>, the term
<math id="p22.m4" class="ltx_Math" alttext="{\gamma(\omega^{\beta_{1}})}" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\omega^{\beta_{1}})}</annotation></semantics></math> is eliminated in the expression of <math id="p22.m5" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math>
and it remains</p>
<table id="S0.Ex40" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex40.m1" class="ltx_Math" alttext="{\gamma(\alpha)}={\omega^{\beta_{1}}\left(\omega^{\beta_{1}}{(n-1)}+\rho\right)}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo>(</mo><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mi>ρ</mi></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha)}={\omega^{\beta_{1}}\left(\omega^{\beta_{1}}{(n-1)}+\rho\right)}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">where <math id="p22.m6" class="ltx_Math" alttext="\rho=\omega^{\beta_{2}}n_{2}+\dots+\omega^{\beta_{k}}n_{k}" display="inline"><semantics><mrow><mi>ρ</mi><mo>=</mo><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>2</mn></msub></msup><mo>⁢</mo><msub><mi>n</mi><mn>2</mn></msub></mrow><mo>+</mo><mi mathvariant="normal">…</mi><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mi>k</mi></msub></msup><mo>⁢</mo><msub><mi>n</mi><mi>k</mi></msub></mrow></mrow></mrow><annotation encoding="application/x-tex">\rho=\omega^{\beta_{2}}n_{2}+\dots+\omega^{\beta_{k}}n_{k}</annotation></semantics></math>. If instead <math id="p22.m7" class="ltx_Math" alttext="n=1" display="inline"><semantics><mrow><mi>n</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n=1</annotation></semantics></math>, then the term
<math id="p22.m8" class="ltx_Math" alttext="\omega^{\beta_{1}}{(n-1)}" display="inline"><semantics><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\omega^{\beta_{1}}{(n-1)}</annotation></semantics></math> is zero and it remains</p>
<table id="S0.Ex41" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex41.m1" class="ltx_Math" alttext="{\gamma(\alpha)}={\omega^{\beta_{1}}\left(\omega^{{\omega^{\delta}\cdot{(m-1)}%
}}+\omega^{\beta_{2}}n_{2}+\dots+\omega^{\beta_{k}}n_{k}\right)}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><mo>⁢</mo><mrow><mo>(</mo><mrow><msup><mi>ω</mi><mrow><msup><mi>ω</mi><mi>δ</mi></msup><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>m</mi><mo>-</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow></msup><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>2</mn></msub></msup><mo>⁢</mo><msub><mi>n</mi><mn>2</mn></msub></mrow><mo>+</mo><mi mathvariant="normal">…</mi><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mi>k</mi></msub></msup><mo>⁢</mo><msub><mi>n</mi><mi>k</mi></msub></mrow></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha)}={\omega^{\beta_{1}}\left(\omega^{{\omega^{\delta}\cdot{(m-1)}%
}}+\omega^{\beta_{2}}n_{2}+\dots+\omega^{\beta_{k}}n_{k}\right)}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p23" class="ltx_para">
<p class="ltx_p">∎</p>
</div>
</div>


{% endraw %}
