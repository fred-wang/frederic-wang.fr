---
layout: post
title: "The canonical well-ordering of α×α (part 1)"
tags: maths
---

{% raw %}

  

<div id="p1" class="ltx_para">
<p class="ltx_p">It is well-known that the cartesian product of two infinite sets of cardinality
<math id="p1.m1" class="ltx_Math" alttext="\aleph_{\alpha}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\aleph_{\alpha}</annotation></semantics></math> is also of cardinality <math id="p1.m2" class="ltx_Math" alttext="\aleph_{\alpha}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\aleph_{\alpha}</annotation></semantics></math>.
Equivalently, the set
<math id="p1.m3" class="ltx_Math" alttext="\omega_{\alpha}\times\omega_{\alpha}" display="inline"><semantics><mrow><msub><mi>ω</mi><mi>α</mi></msub><mo>×</mo><msub><mi>ω</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\omega_{\alpha}\times\omega_{\alpha}</annotation></semantics></math> can be well-ordered in order-type
<math id="p1.m4" class="ltx_Math" alttext="\omega_{\alpha}" display="inline"><semantics><msub><mi>ω</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\omega_{\alpha}</annotation></semantics></math>. However, the standard ordering on
<math id="p1.m5" class="ltx_Math" alttext="\omega_{\alpha}\times\omega_{\alpha}" display="inline"><semantics><mrow><msub><mi>ω</mi><mi>α</mi></msub><mo>×</mo><msub><mi>ω</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\omega_{\alpha}\times\omega_{\alpha}</annotation></semantics></math> does
not work, since it is always of order type <math id="p1.m6" class="ltx_Math" alttext="\omega_{\alpha}^{2}" display="inline"><semantics><msubsup><mi>ω</mi><mi>α</mi><mn>2</mn></msubsup><annotation encoding="application/x-tex">\omega_{\alpha}^{2}</annotation></semantics></math>.
Instead, we introduce for each ordinal <math id="p1.m7" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>
the canonical well-ordering of <math id="p1.m8" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo>×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math> as follows:
<math id="p1.m9" class="ltx_Math" alttext="{(\xi_{1},\xi_{2})}\lhd{(\eta_{1},\eta_{2})}" display="inline"><semantics><mrow><mrow><mo stretchy="false">(</mo><msub><mi>ξ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>ξ</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow><mo>⊲</mo><mrow><mo stretchy="false">(</mo><msub><mi>η</mi><mn>1</mn></msub><mo>,</mo><msub><mi>η</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">{(\xi_{1},\xi_{2})}\lhd{(\eta_{1},\eta_{2})}</annotation></semantics></math> if either
<math id="p1.m10" class="ltx_Math" alttext="{\max{(\xi_{1},\xi_{2})}}&lt;{\max{(\eta_{1},\eta_{2})}}" display="inline"><semantics><mrow><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>ξ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>ξ</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>η</mi><mn>1</mn></msub><mo>,</mo><msub><mi>η</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">{\max{(\xi_{1},\xi_{2})}}&lt;{\max{(\eta_{1},\eta_{2})}}</annotation></semantics></math> or
<math id="p1.m11" class="ltx_Math" alttext="{\max{(\xi_{1},\xi_{2})}}={\max{(\eta_{1},\eta_{2})}}" display="inline"><semantics><mrow><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>ξ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>ξ</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>η</mi><mn>1</mn></msub><mo>,</mo><msub><mi>η</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">{\max{(\xi_{1},\xi_{2})}}={\max{(\eta_{1},\eta_{2})}}</annotation></semantics></math> but
<math id="p1.m12" class="ltx_Math" alttext="(\xi_{1},\xi_{2})" display="inline"><semantics><mrow><mo stretchy="false">(</mo><msub><mi>ξ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>ξ</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">(\xi_{1},\xi_{2})</annotation></semantics></math> precedes <math id="p1.m13" class="ltx_Math" alttext="(\eta_{1},\eta_{2})" display="inline"><semantics><mrow><mo stretchy="false">(</mo><msub><mi>η</mi><mn>1</mn></msub><mo>,</mo><msub><mi>η</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">(\eta_{1},\eta_{2})</annotation></semantics></math> lexicographically. If we note
<math id="p1.m14" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math> the ordinal isomorphic to that well-ordering ordering,
then we can prove that <math id="p1.m15" class="ltx_Math" alttext="\gamma(\omega_{\alpha})=\omega_{\alpha}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><msub><mi>ω</mi><mi>α</mi></msub><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msub><mi>ω</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\gamma(\omega_{\alpha})=\omega_{\alpha}</annotation></semantics></math> as wanted
(see Corollary <a href="#S0.Thmtheorem4" title="Corollary 0.4. ‣ The canonical well-ordering of ×αα (part 1)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.4</span></a>).</p>
</div>
<div id="p2" class="ltx_para">
<p class="ltx_p">Jech’s Set Theory
book contains several properties of <math id="p2.m1" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>. For example, <math id="p2.m2" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>
is increasing : for any ordinal <math id="p2.m3" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>,
<math id="p2.m4" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo>×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math> is a (proper) initial segment of
<math id="p2.m5" class="ltx_Math" alttext="{(\alpha+1)}\times{(\alpha+1)}" display="inline"><semantics><mrow><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow><mo>×</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">{(\alpha+1)}\times{(\alpha+1)}</annotation></semantics></math> and of <math id="p2.m6" class="ltx_Math" alttext="\lambda\times\lambda" display="inline"><semantics><mrow><mi>λ</mi><mo>×</mo><mi>λ</mi></mrow><annotation encoding="application/x-tex">\lambda\times\lambda</annotation></semantics></math>
for any limit ordinal <math id="p2.m7" class="ltx_Math" alttext="\lambda&gt;\alpha" display="inline"><semantics><mrow><mi>λ</mi><mo>&gt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\lambda&gt;\alpha</annotation></semantics></math>. As a consequence,
<math id="p2.m8" class="ltx_Math" alttext="\forall\alpha,\alpha\leq\gamma(\alpha)" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><mi>α</mi></mrow><mo>≤</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha,\alpha\leq\gamma(\alpha)</annotation></semantics></math> which can also trivially
be seen by the increasing function <math id="p2.m9" class="ltx_Math" alttext="\xi\mapsto(\xi,0)" display="inline"><semantics><mrow><mi>ξ</mi><mo>↦</mo><mrow><mo stretchy="false">(</mo><mi>ξ</mi><mo>,</mo><mn>0</mn><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\xi\mapsto(\xi,0)</annotation></semantics></math> from <math id="p2.m10" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>
to <math id="p2.m11" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo>×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math>. Also,
<math id="p2.m12" class="ltx_Math" alttext="\forall\alpha,\gamma(\alpha)&lt;\gamma(\lambda)" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>&lt;</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>λ</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha,\gamma(\alpha)&lt;\gamma(\lambda)</annotation></semantics></math> implies <math id="p2.m13" class="ltx_Math" alttext="\sup_{\alpha&lt;\lambda}{\gamma(\alpha)}\leq\gamma(\lambda)" display="inline"><semantics><mrow><mrow><msub><mo>sup</mo><mrow><mi>α</mi><mo>&lt;</mo><mi>λ</mi></mrow></msub><mo>⁡</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>≤</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>λ</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\sup_{\alpha&lt;\lambda}{\gamma(\alpha)}\leq\gamma(\lambda)</annotation></semantics></math>.
This can not be a strict equality,
or otherwise the element <math id="p2.m14" class="ltx_Math" alttext="{(\xi,\eta)}\in\lambda\times\lambda" display="inline"><semantics><mrow><mrow><mo stretchy="false">(</mo><mi>ξ</mi><mo>,</mo><mi>η</mi><mo stretchy="false">)</mo></mrow><mo>∈</mo><mrow><mi>λ</mi><mo>×</mo><mi>λ</mi></mrow></mrow><annotation encoding="application/x-tex">{(\xi,\eta)}\in\lambda\times\lambda</annotation></semantics></math>
corresponding to <math id="p2.m15" class="ltx_Math" alttext="\sup_{\alpha&lt;\lambda}{\gamma(\alpha)}" display="inline"><semantics><mrow><msub><mo>sup</mo><mrow><mi>α</mi><mo>&lt;</mo><mi>λ</mi></mrow></msub><mo>⁡</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\sup_{\alpha&lt;\lambda}{\gamma(\alpha)}</annotation></semantics></math> via the
isomorphism between <math id="p2.m16" class="ltx_Math" alttext="\lambda\times\lambda" display="inline"><semantics><mrow><mi>λ</mi><mo>×</mo><mi>λ</mi></mrow><annotation encoding="application/x-tex">\lambda\times\lambda</annotation></semantics></math> and <math id="p2.m17" class="ltx_Math" alttext="\gamma(\lambda)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>λ</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\lambda)</annotation></semantics></math>
would be an element larger than all <math id="p2.m18" class="ltx_Math" alttext="(\alpha,\alpha)" display="inline"><semantics><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>,</mo><mi>α</mi><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">(\alpha,\alpha)</annotation></semantics></math> for <math id="p2.m19" class="ltx_Math" alttext="\alpha&lt;\lambda" display="inline"><semantics><mrow><mi>α</mi><mo>&lt;</mo><mi>λ</mi></mrow><annotation encoding="application/x-tex">\alpha&lt;\lambda</annotation></semantics></math>.
Hence <math id="p2.m20" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> is continuous and by exercise 2.7 of the same
book, <math id="p2.m21" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> has arbitrary large fixed points. Exercise 3.5 shows that
<math id="p2.m22" class="ltx_Math" alttext="\gamma(\alpha)\leq\omega^{\alpha}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><msup><mi>ω</mi><mi>α</mi></msup></mrow><annotation encoding="application/x-tex">\gamma(\alpha)\leq\omega^{\alpha}</annotation></semantics></math> and so <math id="p2.m23" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> does not increase
cardinality (see Corollary <a href="#S0.Thmtheorem2" title="Corollary 0.2. ‣ The canonical well-ordering of ×αα (part 1)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.2</span></a> for a much
better upper bound).
Hence starting at any infinite cardinal <math id="p2.m24" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math> the construction
of exercise 2.7 provides infinitely many fixed points of <math id="p2.m25" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> having
cardinality <math id="p2.m26" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math>. Hence the infinite fixed points of <math id="p2.m27" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> are not just
cardinals and we can wonder what they are exactly…</p>
</div>
<div id="p3" class="ltx_para">
<p class="ltx_p">I recently tried to solve Exercise I.11.7 of Kunen’s Set Theory book which
suggests a nice characterization of infinite fixed points of <math id="p3.m1" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>:
they are the ordinals of the form <math id="p3.m2" class="ltx_Math" alttext="\omega^{\omega^{\alpha}}" display="inline"><semantics><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><annotation encoding="application/x-tex">\omega^{\omega^{\alpha}}</annotation></semantics></math>. However, I could not
find a simple proof of this statement so instead I tried to determine the
explicit expression of <math id="p3.m3" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math>, from which the result becomes obvious
(see Corollary <a href="#S0.Thmtheorem3" title="Corollary 0.3. ‣ The canonical well-ordering of ×αα (part 1)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.3</span></a>).
My final calculation is summarized in Theorem <a href="#S0.Thmtheorem1" title="Theorem 0.1. ‣ The canonical well-ordering of ×αα (part 1)" class="ltx_ref"><span class="ltx_text ltx_ref_tag">0.1</span></a>, which provides
a relatively nice expression of <math id="p3.m4" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math>. Recall that any
<math id="p3.m5" class="ltx_Math" alttext="\alpha\geq 1" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\alpha\geq 1</annotation></semantics></math> can be written uniquely as
<math id="p3.m6" class="ltx_Math" alttext="\alpha=\omega^{\beta}q+\rho" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><mrow><msup><mi>ω</mi><mi>β</mi></msup><mo>⁢</mo><mi>q</mi></mrow><mo>+</mo><mi>ρ</mi></mrow></mrow><annotation encoding="application/x-tex">\alpha=\omega^{\beta}q+\rho</annotation></semantics></math> where <math id="p3.m7" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math> is (following Kunen’s terminology)
the “logarithm in base <math id="p3.m8" class="ltx_Math" alttext="\omega" display="inline"><semantics><mi>ω</mi><annotation encoding="application/x-tex">\omega</annotation></semantics></math> of <math id="p3.m9" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>” (that we
will denote <math id="p3.m10" class="ltx_Math" alttext="\log_{\omega}{\alpha}" display="inline"><semantics><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\log_{\omega}{\alpha}</annotation></semantics></math> for <math id="p3.m11" class="ltx_Math" alttext="\alpha\geq\omega" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\alpha\geq\omega</annotation></semantics></math>)
and <math id="p3.m12" class="ltx_Math" alttext="q,\rho" display="inline"><semantics><mrow><mi>q</mi><mo>,</mo><mi>ρ</mi></mrow><annotation encoding="application/x-tex">q,\rho</annotation></semantics></math> are the quotient and
remainder of the Euclidean division of <math id="p3.m13" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> by <math id="p3.m14" class="ltx_Math" alttext="\omega^{\beta}" display="inline"><semantics><msup><mi>ω</mi><mi>β</mi></msup><annotation encoding="application/x-tex">\omega^{\beta}</annotation></semantics></math>. Alternatively,
this can be seen from Cantor’s Normal Form: <math id="p3.m15" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math> and <math id="p3.m16" class="ltx_Math" alttext="q" display="inline"><semantics><mi>q</mi><annotation encoding="application/x-tex">q</annotation></semantics></math> are the exponent
and coefficient of the largest term while <math id="p3.m17" class="ltx_Math" alttext="\rho" display="inline"><semantics><mi>ρ</mi><annotation encoding="application/x-tex">\rho</annotation></semantics></math> is the sum of terms of smaller
exponents.</p>
</div>
<div id="S0.Thmtheorem1" class="ltx_theorem ltx_theorem_theorem">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Theorem 0.1</span>.</h6>
<div id="S0.Thmtheorem1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">For all ordinal <math id="S0.Thmtheorem1.p1.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>, we denote <math id="S0.Thmtheorem1.p1.m2" class="ltx_Math" alttext="\gamma(\alpha)" display="inline"><semantics><mrow><mi>γ</mi><mo mathvariant="italic">⁢</mo><mrow><mo mathvariant="normal" stretchy="false">(</mo><mi>α</mi><mo mathvariant="normal" stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)</annotation></semantics></math> the order-type of
the canonical ordering of <math id="S0.Thmtheorem1.p1.m3" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo mathvariant="normal">×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math>. Then <math id="S0.Thmtheorem1.p1.m4" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> can be
calculated as follows:</span></p>
<ol id="I1" class="ltx_enumerate">
<li id="I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate"><span class="ltx_text ltx_font_italic">1.</span></span> 
<div id="I1.i1.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Finite Ordinals:
For any </span><math id="I1.i1.p1.m1" class="ltx_Math" alttext="n&lt;\omega" display="inline"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">n&lt;\omega</annotation></semantics></math><span class="ltx_text ltx_font_italic"> we have</span></p>
<table id="S0.Ex1" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex1.m1" class="ltx_Math" alttext="\gamma(n)=n^{2}" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>n</mi><mn>2</mn></msup></mrow><annotation encoding="application/x-tex">\gamma(n)=n^{2}</annotation></semantics></math></td>
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
<table id="S0.Ex2" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex2.m1" class="ltx_Math" alttext="\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\alpha" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mi>α</mi></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\alpha</annotation></semantics></math></td>
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
<table id="S0.Ex3" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex3.m1" class="ltx_Math" alttext="\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\left({\omega^{\log_{\omega}%
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
<table id="S0.Ex4" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex4.m1" class="ltx_Math" alttext="\gamma(\alpha)=\omega^{\log_{\omega}(\alpha)}\cdot\left(\omega^{\omega^{\log_{%
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
<table id="S0.Ex5" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex5.m1" class="ltx_Math" alttext="\gamma(\alpha+n)=\gamma(\alpha)+{\alpha\cdot{2n}}+n" display="block"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+n)=\gamma(\alpha)+{\alpha\cdot{2n}}+n</annotation></semantics></math></td>
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
<div id="p4" class="ltx_para">
<p class="ltx_p">In a future blog post ;-) ∎</p>
</div>
</div>
<div id="p5" class="ltx_para">
<p class="ltx_p">From this theorem, we deduce several corollaries:</p>
</div>
<div id="S0.Thmtheorem2" class="ltx_theorem ltx_theorem_corollary">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Corollary 0.2</span>.</h6>
<div id="S0.Thmtheorem2.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">For any ordinal <math id="S0.Thmtheorem2.p1.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>, we have</span></p>
</div>
<div id="S0.Thmtheorem2.p2" class="ltx_para">
<table id="S0.Ex6" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex6.m1" class="ltx_Math" alttext="\alpha\leq{\gamma(\alpha)}\leq{{\omega^{\log_{\omega}(\alpha)}\cdot\left({%
\alpha-r}\right)}+{\alpha\cdot{2r}}}\leq\alpha\left(\alpha+r\right)" display="block"><semantics><mrow><mi>α</mi><mo>≤</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mrow><mo>(</mo><mrow><mi>α</mi><mo>-</mo><mi>r</mi></mrow><mo>)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>r</mi></mrow></mrow><mo>≤</mo><mrow><mi>α</mi><mo>⁢</mo><mrow><mo>(</mo><mrow><mi>α</mi><mo>+</mo><mi>r</mi></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\alpha\leq{\gamma(\alpha)}\leq{{\omega^{\log_{\omega}(\alpha)}\cdot\left({%
\alpha-r}\right)}+{\alpha\cdot{2r}}}\leq\alpha\left(\alpha+r\right)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p"><span class="ltx_text ltx_font_italic">where <math id="S0.Thmtheorem2.p2.m1" class="ltx_Math" alttext="r=\alpha\mod\omega" display="inline"><semantics><mrow><mi>r</mi><mo mathvariant="normal">=</mo><mrow><mi>α</mi><mo lspace="2.5pt" mathvariant="normal" rspace="2.5pt">mod</mo><mi>ω</mi></mrow></mrow><annotation encoding="application/x-tex">r=\alpha\mod\omega</annotation></semantics></math> is the remainder in the Euclidean division
of <math id="S0.Thmtheorem2.p2.m2" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> by <math id="S0.Thmtheorem2.p2.m3" class="ltx_Math" alttext="\omega" display="inline"><semantics><mi>ω</mi><annotation encoding="application/x-tex">\omega</annotation></semantics></math> (i.e. the constant term in the Cantor Normal Form).</span></p>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p6" class="ltx_para">
<p class="ltx_p">The “Limit Ordinals” case is <math id="p6.m1" class="ltx_Math" alttext="r=0" display="inline"><semantics><mrow><mi>r</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">r=0</annotation></semantics></math> i.e. <math id="p6.m2" class="ltx_Math" alttext="\alpha\leq{\gamma(\alpha)}\leq{{\omega^{\log_{\omega}(\alpha)}\cdot\alpha}}" display="inline"><semantics><mrow><mi>α</mi><mo>≤</mo><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mi>α</mi></mrow></mrow><annotation encoding="application/x-tex">\alpha\leq{\gamma(\alpha)}\leq{{\omega^{\log_{\omega}(\alpha)}\cdot\alpha}}</annotation></semantics></math>,
which is readily seen by the
previous theorem.
Then we deduce for the “Infinite Successor Ordinals” case:
<math id="p6.m3" class="ltx_Math" alttext="{\gamma(\alpha+n)}=\gamma(\alpha)+{\alpha\cdot{2n}}+n\leq{{\omega^{\log_{%
\omega}(\alpha)}\cdot\alpha}}+{\left(\alpha+n\right)\cdot{2n}}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow><mo>+</mo><mi>n</mi></mrow><mo>≤</mo><mrow><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mi>α</mi></mrow><mo>+</mo><mrow><mrow><mrow><mo>(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo>)</mo></mrow><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow></mrow></mrow><annotation encoding="application/x-tex">{\gamma(\alpha+n)}=\gamma(\alpha)+{\alpha\cdot{2n}}+n\leq{{\omega^{\log_{%
\omega}(\alpha)}\cdot\alpha}}+{\left(\alpha+n\right)\cdot{2n}}</annotation></semantics></math>
where <math id="p6.m4" class="ltx_Math" alttext="{\log_{\omega}(\alpha+n)}={\log_{\omega}(\alpha)}" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">{\log_{\omega}(\alpha+n)}={\log_{\omega}(\alpha)}</annotation></semantics></math> and
<math id="p6.m5" class="ltx_Math" alttext="n=\left(\alpha+n\mod\omega\right)" display="inline"><semantics><mrow><mi>n</mi><mo>=</mo><mrow><mo>(</mo><mrow><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo lspace="2.5pt" rspace="2.5pt">mod</mo><mi>ω</mi></mrow><mo>)</mo></mrow></mrow><annotation encoding="application/x-tex">n=\left(\alpha+n\mod\omega\right)</annotation></semantics></math>.
Since <math id="p6.m6" class="ltx_Math" alttext="\omega^{\log_{\omega}(\alpha)}\leq\alpha" display="inline"><semantics><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>≤</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\omega^{\log_{\omega}(\alpha)}\leq\alpha</annotation></semantics></math> we can write
<math id="p6.m7" class="ltx_Math" alttext="{{\omega^{\log_{\omega}(\alpha)}\cdot\left({\alpha-r}\right)}+{\alpha\cdot{2r}%
}}\leq{\alpha\cdot\left(\alpha-r+2r\right)}={\alpha\cdot{(\alpha+r)}}" display="inline"><semantics><mrow><mrow><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⋅</mo><mrow><mo>(</mo><mrow><mi>α</mi><mo>-</mo><mi>r</mi></mrow><mo>)</mo></mrow></mrow><mo>+</mo><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>r</mi></mrow></mrow><mo>≤</mo><mrow><mi>α</mi><mo>⋅</mo><mrow><mo>(</mo><mrow><mrow><mi>α</mi><mo>-</mo><mi>r</mi></mrow><mo>+</mo><mrow><mn>2</mn><mo>⁢</mo><mi>r</mi></mrow></mrow><mo>)</mo></mrow></mrow><mo>=</mo><mrow><mi>α</mi><mo>⋅</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>r</mi></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">{{\omega^{\log_{\omega}(\alpha)}\cdot\left({\alpha-r}\right)}+{\alpha\cdot{2r}%
}}\leq{\alpha\cdot\left(\alpha-r+2r\right)}={\alpha\cdot{(\alpha+r)}}</annotation></semantics></math>. ∎</p>
</div>
</div>
<div id="p7" class="ltx_para">
<p class="ltx_p">Hence the order type of the canonical ordering <math id="p7.m1" class="ltx_Math" alttext="\lhd" display="inline"><semantics><mo>⊲</mo><annotation encoding="application/x-tex">\lhd</annotation></semantics></math> of <math id="p7.m2" class="ltx_Math" alttext="\alpha\times\alpha" display="inline"><semantics><mrow><mi>α</mi><mo>×</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\times\alpha</annotation></semantics></math>
(i.e. <math id="p7.m3" class="ltx_Math" alttext="\gamma(\alpha)\leq\alpha{(\alpha+\omega)}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><mi>α</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>ω</mi></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)\leq\alpha{(\alpha+\omega)}</annotation></semantics></math>) is never
significantly bigger than the one of the standard lexical ordering
(i.e. <math id="p7.m4" class="ltx_Math" alttext="\alpha^{2}" display="inline"><semantics><msup><mi>α</mi><mn>2</mn></msup><annotation encoding="application/x-tex">\alpha^{2}</annotation></semantics></math>), and even never larger
for limit ordinals. Moreover, for many ordinals <math id="p7.m5" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>
the canonical ordering is of order type <math id="p7.m6" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>:
</p>
</div>
<div id="S0.Thmtheorem3" class="ltx_theorem ltx_theorem_corollary">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Corollary 0.3</span>.</h6>
<div id="S0.Thmtheorem3.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">The fixed points of <math id="S0.Thmtheorem3.p1.m1" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> are <math id="S0.Thmtheorem3.p1.m2" class="ltx_Math" alttext="0,1" display="inline"><semantics><mrow><mn mathvariant="normal">0</mn><mo mathvariant="normal">,</mo><mn mathvariant="normal">1</mn></mrow><annotation encoding="application/x-tex">0,1</annotation></semantics></math> and <math id="S0.Thmtheorem3.p1.m3" class="ltx_Math" alttext="\omega^{\omega^{\alpha}}" display="inline"><semantics><msup><mi>ω</mi><msup><mi>ω</mi><mi>α</mi></msup></msup><annotation encoding="application/x-tex">\omega^{\omega^{\alpha}}</annotation></semantics></math> for
all ordinals <math id="S0.Thmtheorem3.p1.m4" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>.</span></p>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p8" class="ltx_para">
<p class="ltx_p">For the “Finite Ordinals” case, we have <math id="p8.m1" class="ltx_Math" alttext="\gamma(n)=n^{2}=n" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>n</mi><mn>2</mn></msup><mo>=</mo><mi>n</mi></mrow><annotation encoding="application/x-tex">\gamma(n)=n^{2}=n</annotation></semantics></math> iff <math id="p8.m2" class="ltx_Math" alttext="n=0" display="inline"><semantics><mrow><mi>n</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">n=0</annotation></semantics></math> or
<math id="p8.m3" class="ltx_Math" alttext="n=1" display="inline"><semantics><mrow><mi>n</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n=1</annotation></semantics></math>. For the “Infinite Successor Ordinals” case, we have
<math id="p8.m4" class="ltx_Math" alttext="\alpha\cdot{2n}&gt;\alpha" display="inline"><semantics><mrow><mrow><mrow><mi>α</mi><mo>⋅</mo><mn>2</mn></mrow><mo>⁢</mo><mi>n</mi></mrow><mo>&gt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\alpha\cdot{2n}&gt;\alpha</annotation></semantics></math> if <math id="p8.m5" class="ltx_Math" alttext="n\geq 1" display="inline"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n\geq 1</annotation></semantics></math> so <math id="p8.m6" class="ltx_Math" alttext="\gamma(\alpha+n)&gt;\alpha+n" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>&gt;</mo><mrow><mi>α</mi><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha+n)&gt;\alpha+n</annotation></semantics></math>.
Now we look at the three subcases of the “Limit Ordinals” case. For the
first one, we have <math id="p8.m7" class="ltx_Math" alttext="\log_{\omega}(\alpha)\geq 1" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)\geq 1</annotation></semantics></math>
and so <math id="p8.m8" class="ltx_Math" alttext="\omega^{\log_{\omega}(\alpha)}\alpha\geq\omega\alpha&gt;\alpha" display="inline"><semantics><mrow><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⁢</mo><mi>α</mi></mrow><mo>≥</mo><mrow><mi>ω</mi><mo>⁢</mo><mi>α</mi></mrow><mo>&gt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\omega^{\log_{\omega}(\alpha)}\alpha\geq\omega\alpha&gt;\alpha</annotation></semantics></math>.
For the second one, we note that
<math id="p8.m9" class="ltx_Math" alttext="{\log_{\omega}(\alpha)}2&gt;\log_{\omega}(\alpha)" display="inline"><semantics><mrow><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>⁢</mo><mn>2</mn></mrow><mo>&gt;</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">{\log_{\omega}(\alpha)}2&gt;\log_{\omega}(\alpha)</annotation></semantics></math> and so
<math id="p8.m10" class="ltx_Math" alttext="\omega^{{\log_{\omega}(\alpha)}2}&gt;\alpha" display="inline"><semantics><mrow><msup><mi>ω</mi><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>⁢</mo><mn>2</mn></mrow></msup><mo>&gt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\omega^{{\log_{\omega}(\alpha)}2}&gt;\alpha</annotation></semantics></math> (compare the Cantor Normal Form).
Since <math id="p8.m11" class="ltx_Math" alttext="n-1\geq 1" display="inline"><semantics><mrow><mrow><mi>n</mi><mo>-</mo><mn>1</mn></mrow><mo>≥</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">n-1\geq 1</annotation></semantics></math> by assumption, we have <math id="p8.m12" class="ltx_Math" alttext="\gamma(\alpha)&gt;\alpha" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&gt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\gamma(\alpha)&gt;\alpha</annotation></semantics></math>.
Similarly in the third case, if we expand the parenthesis the first term
is <math id="p8.m13" class="ltx_Math" alttext="\omega" display="inline"><semantics><mi>ω</mi><annotation encoding="application/x-tex">\omega</annotation></semantics></math> raised to the power
<math id="p8.m14" class="ltx_Math" alttext="{\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)\right)}\cdot\left%
(2m-1\right)}" display="inline"><semantics><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mi>α</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></msup><mo>⋅</mo><mrow><mo>(</mo><mrow><mrow><mn>2</mn><mo>⁢</mo><mi>m</mi></mrow><mo>-</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow><annotation encoding="application/x-tex">{\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)\right)}\cdot\left%
(2m-1\right)}</annotation></semantics></math> which is stricly greater than
<math id="p8.m15" class="ltx_Math" alttext="\log_{\omega}(\alpha)=\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha%
\right)\right)}m" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mi>α</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></msup><mo>⁢</mo><mi>m</mi></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}(\alpha)=\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha%
\right)\right)}m</annotation></semantics></math> if <math id="p8.m16" class="ltx_Math" alttext="m\geq 2" display="inline"><semantics><mrow><mi>m</mi><mo>≥</mo><mn>2</mn></mrow><annotation encoding="application/x-tex">m\geq 2</annotation></semantics></math>.
Now if <math id="p8.m17" class="ltx_Math" alttext="m=1" display="inline"><semantics><mrow><mi>m</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">m=1</annotation></semantics></math>, we obtain <math id="p8.m18" class="ltx_Math" alttext="\gamma(\alpha)={\omega^{\log_{\omega}(\alpha)}+{\omega^{\log_{\omega}(\alpha)}%
\rho}}" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>+</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>⁢</mo><mi>ρ</mi></mrow></mrow></mrow><annotation encoding="application/x-tex">\gamma(\alpha)={\omega^{\log_{\omega}(\alpha)}+{\omega^{\log_{\omega}(\alpha)}%
\rho}}</annotation></semantics></math> and
<math id="p8.m19" class="ltx_Math" alttext="\alpha={\omega^{\log_{\omega}(\alpha)}}+\rho" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></msup><mo>+</mo><mi>ρ</mi></mrow></mrow><annotation encoding="application/x-tex">\alpha={\omega^{\log_{\omega}(\alpha)}}+\rho</annotation></semantics></math>. Hence <math id="p8.m20" class="ltx_Math" alttext="\gamma(\alpha)&gt;\alpha" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&gt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\gamma(\alpha)&gt;\alpha</annotation></semantics></math> if
<math id="p8.m21" class="ltx_Math" alttext="\rho&gt;0" display="inline"><semantics><mrow><mi>ρ</mi><mo>&gt;</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\rho&gt;0</annotation></semantics></math> and <math id="p8.m22" class="ltx_Math" alttext="\gamma(\alpha)=\alpha" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\gamma(\alpha)=\alpha</annotation></semantics></math> if <math id="p8.m23" class="ltx_Math" alttext="\rho=0" display="inline"><semantics><mrow><mi>ρ</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\rho=0</annotation></semantics></math>.
Finally for <math id="p8.m24" class="ltx_Math" alttext="\alpha\geq\omega" display="inline"><semantics><mrow><mi>α</mi><mo>≥</mo><mi>ω</mi></mrow><annotation encoding="application/x-tex">\alpha\geq\omega</annotation></semantics></math>, <math id="p8.m25" class="ltx_Math" alttext="\gamma(\alpha)=\alpha" display="inline"><semantics><mrow><mrow><mi>γ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\gamma(\alpha)=\alpha</annotation></semantics></math> iff
<math id="p8.m26" class="ltx_Math" alttext="\alpha=\omega^{\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)%
\right)}}" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><msup><mi>ω</mi><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><mo>(</mo><mi>α</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></msup></msup></mrow><annotation encoding="application/x-tex">\alpha=\omega^{\omega^{\log_{\omega}\left(\log_{\omega}\left(\alpha\right)%
\right)}}</annotation></semantics></math> iff
<math id="p8.m27" class="ltx_Math" alttext="\alpha=\omega^{\omega^{\beta}}" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><msup><mi>ω</mi><msup><mi>ω</mi><mi>β</mi></msup></msup></mrow><annotation encoding="application/x-tex">\alpha=\omega^{\omega^{\beta}}</annotation></semantics></math> for some ordinal <math id="p8.m28" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math>. ∎</p>
</div>
</div>
<div id="p9" class="ltx_para">
<p class="ltx_p">Finally, now that we know that infinite fixed points of <math id="p9.m1" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> are of the
form <math id="p9.m2" class="ltx_Math" alttext="\alpha=\omega^{\omega^{\beta}}" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><msup><mi>ω</mi><msup><mi>ω</mi><mi>β</mi></msup></msup></mrow><annotation encoding="application/x-tex">\alpha=\omega^{\omega^{\beta}}</annotation></semantics></math> we only need to verify that infinite
cardinals <math id="p9.m3" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math> are of this form to prove that
<math id="p9.m4" class="ltx_Math" alttext="{|\kappa\times\kappa|}=\kappa" display="inline"><semantics><mrow><mrow><mo stretchy="false">|</mo><mrow><mi>κ</mi><mo>×</mo><mi>κ</mi></mrow><mo stretchy="false">|</mo></mrow><mo>=</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">{|\kappa\times\kappa|}=\kappa</annotation></semantics></math>. This provides an alternative
(less straightforward) proof of Theorem 3.5 from Jech’s Set Theory book.</p>
</div>
<div id="S0.Thmtheorem4" class="ltx_theorem ltx_theorem_corollary">
<h6 class="ltx_title ltx_runin ltx_font_bold ltx_title_theorem">
<span class="ltx_tag ltx_tag_theorem">Corollary 0.4</span>.</h6>
<div id="S0.Thmtheorem4.p1" class="ltx_para">
<p class="ltx_p"><span class="ltx_text ltx_font_italic">Any infinite cardinal <math id="S0.Thmtheorem4.p1.m1" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math> is a fixed point of <math id="S0.Thmtheorem4.p1.m2" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>.
Hence for any infinite cardinal <math id="S0.Thmtheorem4.p1.m3" class="ltx_Math" alttext="\kappa_{1},\kappa_{2}" display="inline"><semantics><mrow><msub><mi>κ</mi><mn mathvariant="normal">1</mn></msub><mo mathvariant="normal">,</mo><msub><mi>κ</mi><mn mathvariant="normal">2</mn></msub></mrow><annotation encoding="application/x-tex">\kappa_{1},\kappa_{2}</annotation></semantics></math> we have</span></p>
<table id="S0.Ex7" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex7.m1" class="ltx_Math" alttext="\kappa_{1}+\kappa_{2}=\kappa_{1}\kappa_{2}={\max(\kappa_{1},\kappa_{2})}" display="block"><semantics><mrow><mrow><msub><mi>κ</mi><mn>1</mn></msub><mo>+</mo><msub><mi>κ</mi><mn>2</mn></msub></mrow><mo>=</mo><mrow><msub><mi>κ</mi><mn>1</mn></msub><mo>⁢</mo><msub><mi>κ</mi><mn>2</mn></msub></mrow><mo>=</mo><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>κ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>κ</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\kappa_{1}+\kappa_{2}=\kappa_{1}\kappa_{2}={\max(\kappa_{1},\kappa_{2})}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</div>
<div class="ltx_proof">
<h6 class="ltx_title ltx_runin ltx_font_italic ltx_title_proof">Proof.</h6>
<div id="p10" class="ltx_para">
<p class="ltx_p">For any cardinal infinite cardinal <math id="p10.m1" class="ltx_Math" alttext="\mu" display="inline"><semantics><mi>μ</mi><annotation encoding="application/x-tex">\mu</annotation></semantics></math> that is a fixed point of <math id="p10.m2" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>,
the canonical well-ordering provides a bijection between <math id="p10.m3" class="ltx_Math" alttext="\mu" display="inline"><semantics><mi>μ</mi><annotation encoding="application/x-tex">\mu</annotation></semantics></math> and
<math id="p10.m4" class="ltx_Math" alttext="\mu\times\mu" display="inline"><semantics><mrow><mi>μ</mi><mo>×</mo><mi>μ</mi></mrow><annotation encoding="application/x-tex">\mu\times\mu</annotation></semantics></math> i.e. <math id="p10.m5" class="ltx_Math" alttext="\mu^{2}=\mu" display="inline"><semantics><mrow><msup><mi>μ</mi><mn>2</mn></msup><mo>=</mo><mi>μ</mi></mrow><annotation encoding="application/x-tex">\mu^{2}=\mu</annotation></semantics></math>.
Hence if <math id="p10.m6" class="ltx_Math" alttext="\mu_{1}\leq\mu_{2}" display="inline"><semantics><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>≤</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><annotation encoding="application/x-tex">\mu_{1}\leq\mu_{2}</annotation></semantics></math> are two fixed points, we have</p>
<table id="S0.Ex8" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex8.m1" class="ltx_Math" alttext="\mu_{2}\leq{\mu_{1}+\mu_{2}}\leq{\mu_{1}\mu_{2}}\leq\mu_{2}^{2}=\mu_{2}" display="block"><semantics><mrow><msub><mi>μ</mi><mn>2</mn></msub><mo>≤</mo><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>+</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><mo>≤</mo><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>⁢</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><mo>≤</mo><msubsup><mi>μ</mi><mn>2</mn><mn>2</mn></msubsup><mo>=</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><annotation encoding="application/x-tex">\mu_{2}\leq{\mu_{1}+\mu_{2}}\leq{\mu_{1}\mu_{2}}\leq\mu_{2}^{2}=\mu_{2}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="p11" class="ltx_para">
<p class="ltx_p">Suppose that there is a cardinal <math id="p11.m1" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math> which is not a fixed point of
<math id="p11.m2" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> and consider the smallest one.
Then any infinite cardinal below <math id="p11.m3" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math> is a fixed point of <math id="p11.m4" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>
and the previous equality is still true below <math id="p11.m5" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math>.</p>
</div>
<div id="p12" class="ltx_para">
<p class="ltx_p">Suppose <math id="p12.m1" class="ltx_Math" alttext="\kappa&gt;\omega^{\log_{\omega}{\kappa}}" display="inline"><semantics><mrow><mi>κ</mi><mo>&gt;</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup></mrow><annotation encoding="application/x-tex">\kappa&gt;\omega^{\log_{\omega}{\kappa}}</annotation></semantics></math> and
write <math id="p12.m2" class="ltx_Math" alttext="\kappa=\omega^{\log_{\omega}{\kappa}}+\rho" display="inline"><semantics><mrow><mi>κ</mi><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup><mo>+</mo><mi>ρ</mi></mrow></mrow><annotation encoding="application/x-tex">\kappa=\omega^{\log_{\omega}{\kappa}}+\rho</annotation></semantics></math> where <math id="p12.m3" class="ltx_Math" alttext="\rho&lt;\kappa" display="inline"><semantics><mrow><mi>ρ</mi><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\rho&lt;\kappa</annotation></semantics></math>
corresponds to the remaining terms in Cantor Normal Form. Then
<math id="p12.m4" class="ltx_Math" alttext="\aleph_{0}\leq\mu_{1}=\left|\omega^{\log_{\omega}{\kappa}}\right|&lt;\kappa" display="inline"><semantics><mrow><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub><mo>≤</mo><msub><mi>μ</mi><mn>1</mn></msub><mo>=</mo><mrow><mo>|</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup><mo>|</mo></mrow><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\aleph_{0}\leq\mu_{1}=\left|\omega^{\log_{\omega}{\kappa}}\right|&lt;\kappa</annotation></semantics></math>,
<math id="p12.m5" class="ltx_Math" alttext="\mu_{2}={|\rho|}&lt;\kappa" display="inline"><semantics><mrow><msub><mi>μ</mi><mn>2</mn></msub><mo>=</mo><mrow><mo stretchy="false">|</mo><mi>ρ</mi><mo stretchy="false">|</mo></mrow><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu_{2}={|\rho|}&lt;\kappa</annotation></semantics></math> and <math id="p12.m6" class="ltx_Math" alttext="\mu_{1}+\mu_{2}=\kappa" display="inline"><semantics><mrow><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>+</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><mo>=</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu_{1}+\mu_{2}=\kappa</annotation></semantics></math>. But the two first
relations imply
<math id="p12.m7" class="ltx_Math" alttext="\mu_{1}+\mu_{2}=\max(\mu_{1},\mu_{2})&lt;\kappa" display="inline"><semantics><mrow><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>+</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><mo>=</mo><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>μ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>μ</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu_{1}+\mu_{2}=\max(\mu_{1},\mu_{2})&lt;\kappa</annotation></semantics></math> which contradicts the third one.
Hence <math id="p12.m8" class="ltx_Math" alttext="\kappa=\omega^{\log_{\omega}{\kappa}}" display="inline"><semantics><mrow><mi>κ</mi><mo>=</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup></mrow><annotation encoding="application/x-tex">\kappa=\omega^{\log_{\omega}{\kappa}}</annotation></semantics></math>.</p>
</div>
<div id="p13" class="ltx_para">
<p class="ltx_p">Now suppose
<math id="p13.m1" class="ltx_Math" alttext="\log_{\omega}{\kappa}&gt;\omega^{\log_{\omega}{\log_{\omega}{\kappa}}}" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow><mo>&gt;</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></mrow></msup></mrow><annotation encoding="application/x-tex">\log_{\omega}{\kappa}&gt;\omega^{\log_{\omega}{\log_{\omega}{\kappa}}}</annotation></semantics></math> and write
<math id="p13.m2" class="ltx_Math" alttext="\log_{\omega}{\kappa}=\omega^{\log_{\omega}{\kappa}}+\rho" display="inline"><semantics><mrow><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow><mo>=</mo><mrow><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup><mo>+</mo><mi>ρ</mi></mrow></mrow><annotation encoding="application/x-tex">\log_{\omega}{\kappa}=\omega^{\log_{\omega}{\kappa}}+\rho</annotation></semantics></math> where <math id="p13.m3" class="ltx_Math" alttext="\rho&lt;\log_{\omega}{\kappa}" display="inline"><semantics><mrow><mi>ρ</mi><mo>&lt;</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></mrow><annotation encoding="application/x-tex">\rho&lt;\log_{\omega}{\kappa}</annotation></semantics></math>
corresponds to the remaining terms in Cantor Normal Form. Then we have</p>
<table id="S0.Ex9" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex9.m1" class="ltx_Math" alttext="\kappa=\omega^{\log_{\omega}{\kappa}}=\omega^{\omega^{\log_{\omega}{\log_{%
\omega}{\kappa}}}}\omega^{\rho}" display="block"><semantics><mrow><mi>κ</mi><mo>=</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup><mo>=</mo><mrow><msup><mi>ω</mi><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></mrow></msup></msup><mo>⁢</mo><msup><mi>ω</mi><mi>ρ</mi></msup></mrow></mrow><annotation encoding="application/x-tex">\kappa=\omega^{\log_{\omega}{\kappa}}=\omega^{\omega^{\log_{\omega}{\log_{%
\omega}{\kappa}}}}\omega^{\rho}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
<p class="ltx_p">where <math id="p13.m4" class="ltx_Math" alttext="\omega^{\omega^{\log_{\omega}{\log_{\omega}{\kappa}}}}&lt;\omega^{\log_{\omega}{%
\kappa}}=\kappa" display="inline"><semantics><mrow><msup><mi>ω</mi><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></mrow></msup></msup><mo>&lt;</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup><mo>=</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\omega^{\omega^{\log_{\omega}{\log_{\omega}{\kappa}}}}&lt;\omega^{\log_{\omega}{%
\kappa}}=\kappa</annotation></semantics></math> and
<math id="p13.m5" class="ltx_Math" alttext="\omega^{\rho}&lt;\omega^{\log_{\omega}{\kappa}}=\kappa" display="inline"><semantics><mrow><msup><mi>ω</mi><mi>ρ</mi></msup><mo>&lt;</mo><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></msup><mo>=</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\omega^{\rho}&lt;\omega^{\log_{\omega}{\kappa}}=\kappa</annotation></semantics></math> since
<math id="p13.m6" class="ltx_Math" alttext="\alpha\mapsto\omega^{\alpha}" display="inline"><semantics><mrow><mi>α</mi><mo>↦</mo><msup><mi>ω</mi><mi>α</mi></msup></mrow><annotation encoding="application/x-tex">\alpha\mapsto\omega^{\alpha}</annotation></semantics></math> is strictly increasing. Then
<math id="p13.m7" class="ltx_Math" alttext="\aleph_{0}\leq\mu_{1}=\left|\omega^{\omega^{\log_{\omega}{\log_{\omega}{\kappa%
}}}}\right|&lt;\kappa" display="inline"><semantics><mrow><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub><mo>≤</mo><msub><mi>μ</mi><mn>1</mn></msub><mo>=</mo><mrow><mo>|</mo><msup><mi>ω</mi><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></mrow></msup></msup><mo>|</mo></mrow><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\aleph_{0}\leq\mu_{1}=\left|\omega^{\omega^{\log_{\omega}{\log_{\omega}{\kappa%
}}}}\right|&lt;\kappa</annotation></semantics></math>, <math id="p13.m8" class="ltx_Math" alttext="\mu_{2}={|\omega^{\rho}|}&lt;\kappa" display="inline"><semantics><mrow><msub><mi>μ</mi><mn>2</mn></msub><mo>=</mo><mrow><mo stretchy="false">|</mo><msup><mi>ω</mi><mi>ρ</mi></msup><mo stretchy="false">|</mo></mrow><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu_{2}={|\omega^{\rho}|}&lt;\kappa</annotation></semantics></math> and <math id="p13.m9" class="ltx_Math" alttext="\mu_{1}\mu_{2}=\kappa" display="inline"><semantics><mrow><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>⁢</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><mo>=</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu_{1}\mu_{2}=\kappa</annotation></semantics></math>. But
again, the two first relations imply <math id="p13.m10" class="ltx_Math" alttext="\mu_{1}\mu_{2}=\max(\mu_{1},\mu_{2})&lt;\kappa" display="inline"><semantics><mrow><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>⁢</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><mo>=</mo><mrow><mi>max</mi><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>μ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>μ</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mi>κ</mi></mrow><annotation encoding="application/x-tex">\mu_{1}\mu_{2}=\max(\mu_{1},\mu_{2})&lt;\kappa</annotation></semantics></math> which contradicts the third one.</p>
</div>
<div id="p14" class="ltx_para">
<p class="ltx_p">Finally,
<math id="p14.m1" class="ltx_Math" alttext="\kappa=\omega^{\omega^{\log_{\omega}{\log_{\omega}{\kappa}}}}" display="inline"><semantics><mrow><mi>κ</mi><mo>=</mo><msup><mi>ω</mi><msup><mi>ω</mi><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mrow><msub><mi>log</mi><mi>ω</mi></msub><mo>⁡</mo><mi>κ</mi></mrow></mrow></msup></msup></mrow><annotation encoding="application/x-tex">\kappa=\omega^{\omega^{\log_{\omega}{\log_{\omega}{\kappa}}}}</annotation></semantics></math> and so is a fixed point
of <math id="p14.m2" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math>, a contradiction. Hence all the infinite cardinals are
fixed point of <math id="p14.m3" class="ltx_Math" alttext="\gamma" display="inline"><semantics><mi>γ</mi><annotation encoding="application/x-tex">\gamma</annotation></semantics></math> and so the property stated at the beginning is
true for arbitrary infinite cardinals <math id="p14.m4" class="ltx_Math" alttext="\mu_{1},\mu_{2}" display="inline"><semantics><mrow><msub><mi>μ</mi><mn>1</mn></msub><mo>,</mo><msub><mi>μ</mi><mn>2</mn></msub></mrow><annotation encoding="application/x-tex">\mu_{1},\mu_{2}</annotation></semantics></math>. ∎</p>
</div>
</div>


{% endraw %}
