---
layout: post
title: "Exercises in Set Theory: Applications of Forcing"
tags: maths
---

{% raw %}

  

<div id="p1" class="ltx_para">
<p class="ltx_p">New solutions to exercises from Thomas Jech’s book “Set Theory”:</p>
</div>
<div id="p2" class="ltx_para">
<ul id="I1" class="ltx_itemize">
<li id="I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_itemize">•</span> 
<div id="I1.i1.p1" class="ltx_para">
<p class="ltx_p"><a href="/applications-of-forcing.html">Chapter 15: Forcing</a></p>
</div>
</li>
</ul>
</div>
<div id="p3" class="ltx_para">
<p class="ltx_p">The exercises from this chapter was a good opportunity to play a bit more
with the forcing method. Exercise 15.15 seemed a straightforward
generalization of <a href="https://en.wikipedia.org/wiki/Forcing_%28set_theory%29#Easton_forcing" title="" class="ltx_ref">Easton’s forcing</a> but turned out to be a bit technical.
I realized that the forcing notion used in that exercise provides a
result in ZFC (a bit like Exercises 15.31 and 15.32 allow to prove some
theorems on Boolean Algebras by Forcing).</p>
</div>
<div id="p4" class="ltx_para">
<p class="ltx_p">Remember that <math id="p4.m1" class="ltx_Math" alttext="\beth_{0}=\aleph_{0},\beth_{1}=2^{\beth_{0}},\beth_{2}=2^{\beth_{1}}...,\beth_%
{\omega}=\sup\beth_{n},...,\beth_{\alpha+1}=2^{\beth_{\alpha}},..." display="inline"><semantics><mrow><mrow><msub><mi mathvariant="normal">ℶ</mi><mn>0</mn></msub><mo>=</mo><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub></mrow><mo>,</mo><mrow><mrow><msub><mi mathvariant="normal">ℶ</mi><mn>1</mn></msub><mo>=</mo><msup><mn>2</mn><msub><mi mathvariant="normal">ℶ</mi><mn>0</mn></msub></msup></mrow><mo>,</mo><mrow><mrow><msub><mi mathvariant="normal">ℶ</mi><mn>2</mn></msub><mo>=</mo><mrow><msup><mn>2</mn><msub><mi mathvariant="normal">ℶ</mi><mn>1</mn></msub></msup><mo>⁢</mo><mi mathvariant="normal">…</mi></mrow></mrow><mo>,</mo><mrow><mrow><msub><mi mathvariant="normal">ℶ</mi><mi>ω</mi></msub><mo>=</mo><mrow><mrow><mo>sup</mo><mo>⁡</mo><msub><mi mathvariant="normal">ℶ</mi><mi>n</mi></msub></mrow><mo>,</mo><mi mathvariant="normal">…</mi></mrow></mrow><mo>,</mo><mrow><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>=</mo><mrow><msup><mn>2</mn><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></msup><mo>,</mo><mi mathvariant="normal">…</mi></mrow></mrow></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\beth_{0}=\aleph_{0},\beth_{1}=2^{\beth_{0}},\beth_{2}=2^{\beth_{1}}...,\beth_%
{\omega}=\sup\beth_{n},...,\beth_{\alpha+1}=2^{\beth_{\alpha}},...</annotation></semantics></math> is the normal sequence built by
application of the continuum function at successor step.
One may wonder: is <math id="p4.m2" class="ltx_Math" alttext="\beth_{\alpha}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\beth_{\alpha}</annotation></semantics></math> regular?</p>
</div>
<div id="p5" class="ltx_para">
<p class="ltx_p">First consider the case where <math id="p5.m1" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is limit. The case <math id="p5.m2" class="ltx_Math" alttext="\alpha=0" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\alpha=0</annotation></semantics></math> is
clear (<math id="p5.m3" class="ltx_Math" alttext="\beth_{0}=\aleph_{0}" display="inline"><semantics><mrow><msub><mi mathvariant="normal">ℶ</mi><mn>0</mn></msub><mo>=</mo><msub><mi mathvariant="normal">ℵ</mi><mn>0</mn></msub></mrow><annotation encoding="application/x-tex">\beth_{0}=\aleph_{0}</annotation></semantics></math> is regular) so assume <math id="p5.m4" class="ltx_Math" alttext="\alpha&gt;0" display="inline"><semantics><mrow><mi>α</mi><mo>&gt;</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\alpha&gt;0</annotation></semantics></math>.
If <math id="p5.m5" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is an inacessible
cardinal, it is easy to prove by induction that for all <math id="p5.m6" class="ltx_Math" alttext="\beta&lt;\alpha" display="inline"><semantics><mrow><mi>β</mi><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beta&lt;\alpha</annotation></semantics></math> we
have
<math id="p5.m7" class="ltx_Math" alttext="\beth_{\beta}&lt;\alpha" display="inline"><semantics><mrow><msub><mi mathvariant="normal">ℶ</mi><mi>β</mi></msub><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beth_{\beta}&lt;\alpha</annotation></semantics></math>: at step <math id="p5.m8" class="ltx_Math" alttext="\beta=0" display="inline"><semantics><mrow><mi>β</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\beta=0</annotation></semantics></math> we use that <math id="p5.m9" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is uncountable,
at successor step that it is strong limit and at limit step that it is
regular. Hence <math id="p5.m10" class="ltx_Math" alttext="\beth_{\alpha}=\alpha" display="inline"><semantics><mrow><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><mo>=</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beth_{\alpha}=\alpha</annotation></semantics></math> and so is regular.
If <math id="p5.m11" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is not a cardinal then
<math id="p5.m12" class="ltx_Math" alttext="\operatorname{cf}(\beth_{\alpha})=\operatorname{cf}(\alpha)\leq|\alpha|&lt;\alpha%
\leq\beth_{\alpha}" display="inline"><semantics><mrow><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mo>&lt;</mo><mi>α</mi><mo>≤</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\operatorname{cf}(\beth_{\alpha})=\operatorname{cf}(\alpha)\leq|\alpha|&lt;\alpha%
\leq\beth_{\alpha}</annotation></semantics></math>
so <math id="p5.m13" class="ltx_Math" alttext="\beth_{\alpha}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\beth_{\alpha}</annotation></semantics></math> is singular. If <math id="p5.m14" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is a cardinal but not strong limit
then there is <math id="p5.m15" class="ltx_Math" alttext="\beta&lt;\alpha" display="inline"><semantics><mrow><mi>β</mi><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beta&lt;\alpha</annotation></semantics></math> such that <math id="p5.m16" class="ltx_Math" alttext="2^{\beta}\geq\alpha" display="inline"><semantics><mrow><msup><mn>2</mn><mi>β</mi></msup><mo>≥</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">2^{\beta}\geq\alpha</annotation></semantics></math>. Since
<math id="p5.m17" class="ltx_Math" alttext="\beta&lt;\alpha\leq\beth_{\alpha}" display="inline"><semantics><mrow><mi>β</mi><mo>&lt;</mo><mi>α</mi><mo>≤</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\beta&lt;\alpha\leq\beth_{\alpha}</annotation></semantics></math> there is <math id="p5.m18" class="ltx_Math" alttext="\gamma&lt;\alpha" display="inline"><semantics><mrow><mi>γ</mi><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\gamma&lt;\alpha</annotation></semantics></math> such that
<math id="p5.m19" class="ltx_Math" alttext="\beth_{\gamma}&gt;\beta" display="inline"><semantics><mrow><msub><mi mathvariant="normal">ℶ</mi><mi>γ</mi></msub><mo>&gt;</mo><mi>β</mi></mrow><annotation encoding="application/x-tex">\beth_{\gamma}&gt;\beta</annotation></semantics></math>. Then
<math id="p5.m20" class="ltx_Math" alttext="\beth_{\alpha}\geq\beth_{\gamma+1}=2^{\beth_{\gamma}}&gt;2^{\beta}\geq\alpha" display="inline"><semantics><mrow><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><mo>≥</mo><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>γ</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>=</mo><msup><mn>2</mn><msub><mi mathvariant="normal">ℶ</mi><mi>γ</mi></msub></msup><mo>&gt;</mo><msup><mn>2</mn><mi>β</mi></msup><mo>≥</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beth_{\alpha}\geq\beth_{\gamma+1}=2^{\beth_{\gamma}}&gt;2^{\beta}\geq\alpha</annotation></semantics></math>.
So <math id="p5.m21" class="ltx_Math" alttext="\operatorname{cf}(\beth_{\alpha})=\operatorname{cf}(\alpha)\leq\alpha&lt;\beth_{\alpha}" display="inline"><semantics><mrow><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mi>α</mi><mo>&lt;</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\operatorname{cf}(\beth_{\alpha})=\operatorname{cf}(\alpha)\leq\alpha&lt;\beth_{\alpha}</annotation></semantics></math> and
<math id="p5.m22" class="ltx_Math" alttext="\beth_{\alpha}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\beth_{\alpha}</annotation></semantics></math> is singular. Finally, if <math id="p5.m23" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is a singular cardinal,
then again <math id="p5.m24" class="ltx_Math" alttext="\operatorname{cf}(\beth_{\alpha})=\operatorname{cf}(\alpha)&lt;\alpha\leq\beth_{\alpha}" display="inline"><semantics><mrow><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mi>α</mi><mo>≤</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\operatorname{cf}(\beth_{\alpha})=\operatorname{cf}(\alpha)&lt;\alpha\leq\beth_{\alpha}</annotation></semantics></math> and
<math id="p5.m25" class="ltx_Math" alttext="\beth_{\alpha}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\beth_{\alpha}</annotation></semantics></math> is singular.</p>
</div>
<div id="p6" class="ltx_para">
<p class="ltx_p">What about the successor case i.e. <math id="p6.m1" class="ltx_Math" alttext="\beth_{\alpha+1}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">\beth_{\alpha+1}</annotation></semantics></math>?
By Corollary 5.3 from Thomas Jech’s book any <math id="p6.m2" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>, we can show
that <math id="p6.m3" class="ltx_Math" alttext="\aleph_{\alpha+1}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">\aleph_{\alpha+1}</annotation></semantics></math> is a regular cardinal. The Generalized
Continuum Hypothesis says that <math id="p6.m4" class="ltx_Math" alttext="\forall\alpha,\aleph_{\alpha}=\beth_{\alpha}" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><msub><mi mathvariant="normal">ℵ</mi><mi>α</mi></msub></mrow><mo>=</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\forall\alpha,\aleph_{\alpha}=\beth_{\alpha}</annotation></semantics></math>.
Since it holds in <math id="p6.m5" class="ltx_Math" alttext="L" display="inline"><semantics><mi>L</mi><annotation encoding="application/x-tex">L</annotation></semantics></math> we can not prove in ZFC that for some
<math id="p6.m6" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>, <math id="p6.m7" class="ltx_Math" alttext="\beth_{\alpha+1}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">\beth_{\alpha+1}</annotation></semantics></math> is singular.</p>
</div>
<div id="p7" class="ltx_para">
<p class="ltx_p">The generic extension <math id="p7.m1" class="ltx_Math" alttext="V[G]\supseteq V" display="inline"><semantics><mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><mo>⊇</mo><mi>V</mi></mrow><annotation encoding="application/x-tex">V[G]\supseteq V</annotation></semantics></math> constructed in exercise 15.15
satisfies GCH and so it’s another way
to show that <math id="p7.m2" class="ltx_Math" alttext="\beth_{\alpha+1}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">\beth_{\alpha+1}</annotation></semantics></math> can not be proved to be singular for some
<math id="p7.m3" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>. However, it provides a better result: by construction,
<math id="p7.m4" class="ltx_Math" alttext="V[G]\models\beth_{\alpha+1}^{V}={(\beth_{\alpha}^{V})}^{+}" display="inline"><semantics><mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><mo>⊧</mo><msubsup><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mi>V</mi></msubsup><mo>=</mo><msup><mrow><mo stretchy="false">(</mo><msubsup><mi mathvariant="normal">ℶ</mi><mi>α</mi><mi>V</mi></msubsup><mo stretchy="false">)</mo></mrow><mo>+</mo></msup></mrow><annotation encoding="application/x-tex">V[G]\models\beth_{\alpha+1}^{V}={(\beth_{\alpha}^{V})}^{+}</annotation></semantics></math> and so
<math id="p7.m5" class="ltx_Math" alttext="V[G]\models[\beth_{\alpha+1}^{V}\text{ is a regular cardinal}]" display="inline"><semantics><mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><mo>⊧</mo><mrow><mo stretchy="false">[</mo><mrow><msubsup><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow><mi>V</mi></msubsup><mo>⁢</mo><mtext> is a regular cardinal</mtext></mrow><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="application/x-tex">V[G]\models[\beth_{\alpha+1}^{V}\text{ is a regular cardinal}]</annotation></semantics></math>. Since
“regular cardinal” is a <math id="p7.m6" class="ltx_Math" alttext="\Pi_{1}" display="inline"><semantics><msub><mi mathvariant="normal">Π</mi><mn>1</mn></msub><annotation encoding="application/x-tex">\Pi_{1}</annotation></semantics></math> notion we deduce that
<math id="p7.m7" class="ltx_Math" alttext="\beth_{\alpha+1}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">\beth_{\alpha+1}</annotation></semantics></math> is a regular cardinal in <math id="p7.m8" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math>.</p>
</div>
<div id="p8" class="ltx_para">
<p class="ltx_p">Now the question is: is there any “elementary” proof of the fact that
<math id="p8.m1" class="ltx_Math" alttext="\beth_{\alpha+1}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">\beth_{\alpha+1}</annotation></semantics></math> is regular i.e. without using the forcing method?</p>
</div>
<div id="p9" class="ltx_para">
<p class="ltx_p">–update: of course, I forgot to mention that by KÃ¶nig’s theorem,
<math id="p9.m1" class="ltx_Math" alttext="2^{\beth_{\alpha}}=\beth_{\alpha+1}\geq\operatorname{cf}(\beth_{\alpha+1})=%
\operatorname{cf}(2^{\beth_{\alpha}})\geq{(\beth_{\alpha})}^{+}" display="inline"><semantics><mrow><msup><mn>2</mn><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></msup><mo>=</mo><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>≥</mo><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mo>cf</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub></msup><mo stretchy="false">)</mo></mrow></mrow><mo>≥</mo><msup><mrow><mo stretchy="false">(</mo><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><mo stretchy="false">)</mo></mrow><mo>+</mo></msup></mrow><annotation encoding="application/x-tex">2^{\beth_{\alpha}}=\beth_{\alpha+1}\geq\operatorname{cf}(\beth_{\alpha+1})=%
\operatorname{cf}(2^{\beth_{\alpha}})\geq{(\beth_{\alpha})}^{+}</annotation></semantics></math>
so the singularity of <math id="p9.m2" class="ltx_Math" alttext="\beth_{\alpha+1}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="application/x-tex">\beth_{\alpha+1}</annotation></semantics></math> would imply the failure of the
continuum hypothesis for the cardinal <math id="p9.m3" class="ltx_Math" alttext="\beth_{\alpha}" display="inline"><semantics><msub><mi mathvariant="normal">ℶ</mi><mi>α</mi></msub><annotation encoding="application/x-tex">\beth_{\alpha}</annotation></semantics></math> and this is not provable
in ZFC.</p>
</div>


{% endraw %}
