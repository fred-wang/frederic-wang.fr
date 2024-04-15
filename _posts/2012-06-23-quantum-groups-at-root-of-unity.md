---
layout: post
title: "Quantum Groups at root of unity"
tags: maths
---

{% raw %}

  {% raw %}
<div class="para" id="p1">
<p class="p">All the papers or books I read so far on quantum groups about Lusztig’s restricted specialization consider only primitive roots of unity of odd order and additional conditions. In most cases, it is claimed that these restrictions could be removed without too much harm but details are not given. So I have tried to do the calculation myself. Below is what I find for the finite dimensional representations of <math alttext="{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})" display="inline"><semantics><mrow><msubsup><mi>U</mi><mi>ϵ</mi><mi>res</mi></msubsup><mo>⁢</mo><mfenced close=")" open="("><mi mathvariant="fraktur">g</mi></mfenced></mrow><annotation encoding="application/x-tex">{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})</annotation></semantics></math>. Note that most authors consider the case <math alttext="l=m=m_{i}" display="inline"><semantics><mrow><mi>l</mi><mo>=</mo><mi>m</mi><mo>=</mo><msub><mi>m</mi><mi>i</mi></msub></mrow><annotation encoding="application/x-tex">l=m=m_{i}</annotation></semantics></math> odd. Then <math alttext="{(-1)}^{{m_{i}}}=\epsilon _{i}^{{m_{i}}}=1" display="inline"><semantics><mrow><msup><mfenced close=")" open="("><mrow><mo>-</mo><mn>1</mn></mrow></mfenced><msub><mi>m</mi><mi>i</mi></msub></msup><mo>=</mo><msubsup><mi>ϵ</mi><mi>i</mi><msub><mi>m</mi><mi>i</mi></msub></msubsup><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">{(-1)}^{{m_{i}}}=\epsilon _{i}^{{m_{i}}}=1</annotation></semantics></math> and we can even restrict the study to the representations for which <math alttext="\sigma" display="inline"><semantics><mi>σ</mi><annotation encoding="application/x-tex">\sigma</annotation></semantics></math> is always 1. Indeed, all these assumptions make the expression below much simpler.</p>
</div>

<div class="para" id="p2">
<p class="p">We consider <math alttext="\mathfrak{g}" display="inline"><semantics><mi mathvariant="fraktur">g</mi><annotation encoding="application/x-tex">\mathfrak{g}</annotation></semantics></math> a simple Lie algebra of rank <math alttext="n" display="inline"><semantics><mi>n</mi><annotation encoding="application/x-tex">n</annotation></semantics></math> and use standard notations <math alttext="\alpha _{i}" display="inline"><semantics><msub><mi>α</mi><mi>i</mi></msub><annotation encoding="application/x-tex">\alpha _{i}</annotation></semantics></math> for roots, <math alttext="\alpha _{i}^{\vee}" display="inline"><semantics><msubsup><mi>α</mi><mi>i</mi><mo>∨</mo></msubsup><annotation encoding="application/x-tex">\alpha _{i}^{\vee}</annotation></semantics></math> for coroots and <math alttext="P(\mathfrak{g})" display="inline"><semantics><mrow><mi>P</mi><mo>⁢</mo><mfenced close=")" open="("><mi mathvariant="fraktur">g</mi></mfenced></mrow><annotation encoding="application/x-tex">P(\mathfrak{g})</annotation></semantics></math> for the weight space. Let <math alttext="l&gt;2" display="inline"><semantics><mrow><mi>l</mi><mo>&gt;</mo><mn>2</mn></mrow><annotation encoding="application/x-tex">l&gt;2</annotation></semantics></math> be an integer and <math alttext="\epsilon" display="inline"><semantics><mi>ϵ</mi><annotation encoding="application/x-tex">\epsilon</annotation></semantics></math> a primitive <math alttext="l" display="inline"><semantics><mi>l</mi><annotation encoding="application/x-tex">l</annotation></semantics></math>-root of the unity. We let <math alttext="m=\frac{l}{2}" display="inline"><semantics><mrow><mi>m</mi><mo>=</mo><mfrac><mi>l</mi><mn>2</mn></mfrac></mrow><annotation encoding="application/x-tex">m=\frac{l}{2}</annotation></semantics></math> if <math alttext="l" display="inline"><semantics><mi>l</mi><annotation encoding="application/x-tex">l</annotation></semantics></math> is even and <math alttext="m=l" display="inline"><semantics><mrow><mi>m</mi><mo>=</mo><mi>l</mi></mrow><annotation encoding="application/x-tex">m=l</annotation></semantics></math> otherwise. For all <math alttext="1\leq i\leq n" display="inline"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mi>n</mi></mrow><annotation encoding="application/x-tex">1\leq i\leq n</annotation></semantics></math>, define <math alttext="\epsilon _{i}=\epsilon^{{d_{i}}}" display="inline"><semantics><mrow><msub><mi>ϵ</mi><mi>i</mi></msub><mo>=</mo><msup><mi>ϵ</mi><msub><mi>d</mi><mi>i</mi></msub></msup></mrow><annotation encoding="application/x-tex">\epsilon _{i}=\epsilon^{{d_{i}}}</annotation></semantics></math>, <math alttext="\delta _{i}=\gcd(d_{i},m)" display="inline"><semantics><mrow><msub><mi>δ</mi><mi>i</mi></msub><mo>=</mo><mrow><mi>gcd</mi><mo>⁡</mo><mfenced close=")" open="("><mrow><msub><mi>d</mi><mi>i</mi></msub><mo>,</mo><mi>m</mi></mrow></mfenced></mrow></mrow><annotation encoding="application/x-tex">\delta _{i}=\gcd(d_{i},m)</annotation></semantics></math>, and <math alttext="m_{i}=\frac{m}{\delta _{i}}" display="inline"><semantics><mrow><msub><mi>m</mi><mi>i</mi></msub><mo>=</mo><mfrac><mi>m</mi><msub><mi>δ</mi><mi>i</mi></msub></mfrac></mrow><annotation encoding="application/x-tex">m_{i}=\frac{m}{\delta _{i}}</annotation></semantics></math>. We assume that no <math alttext="d_{i}" display="inline"><semantics><msub><mi>d</mi><mi>i</mi></msub><annotation encoding="application/x-tex">d_{i}</annotation></semantics></math> is a multiple of <math alttext="m" display="inline"><semantics><mi>m</mi><annotation encoding="application/x-tex">m</annotation></semantics></math>, which is obviously true for <math alttext="l" display="inline"><semantics><mi>l</mi><annotation encoding="application/x-tex">l</annotation></semantics></math> large enough.</p>
</div>

<div class="para" id="p3">
<p class="p">We denote <math alttext="{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})" display="inline"><semantics><mrow><msubsup><mi>U</mi><mi>ϵ</mi><mi>res</mi></msubsup><mo>⁢</mo><mfenced close=")" open="("><mi mathvariant="fraktur">g</mi></mfenced></mrow><annotation encoding="application/x-tex">{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})</annotation></semantics></math> the restricted specialization as defined in Chari and Pressley’s guide to quantum groups and keep their notations for the elements <math alttext="K_{i}" display="inline"><semantics><msub><mi>K</mi><mi>i</mi></msub><annotation encoding="application/x-tex">K_{i}</annotation></semantics></math>, <math alttext="{\genfrac{[}{]}{0.0pt}{0}{{K_{i}};{c}}{r}}_{{\epsilon _{i}}}" display="inline"><semantics><msub><mfenced close="]" open="["><mstyle scriptlevel="+1"><mtable columnspacing="0.4em" rowspacing="0.2ex"><mtr><mtd><mrow><msub><mi>K</mi><mi>i</mi></msub><mo>;</mo><mi>c</mi></mrow></mtd></mtr><mtr><mtd><mi>r</mi></mtd></mtr></mtable></mstyle></mfenced><msub><mi>ϵ</mi><mi>i</mi></msub></msub><annotation encoding="application/x-tex">{\genfrac{[}{]}{0.0pt}{0}{{K_{i}};{c}}{r}}_{{\epsilon _{i}}}</annotation></semantics></math>, <math alttext="X_{i}^{{\pm}}" display="inline"><semantics><msubsup><mi>X</mi><mi>i</mi><mo>±</mo></msubsup><annotation encoding="application/x-tex">X_{i}^{{\pm}}</annotation></semantics></math> and <math alttext="{(X_{i}^{\pm})}^{{(r)}}" display="inline"><semantics><msup><mfenced close=")" open="("><msubsup><mi>X</mi><mi>i</mi><mo>±</mo></msubsup></mfenced><mfenced close=")" open="("><mi>r</mi></mfenced></msup><annotation encoding="application/x-tex">{(X_{i}^{\pm})}^{{(r)}}</annotation></semantics></math> of <math alttext="{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})" display="inline"><semantics><mrow><msubsup><mi>U</mi><mi>ϵ</mi><mi>res</mi></msubsup><mo>⁢</mo><mfenced close=")" open="("><mi mathvariant="fraktur">g</mi></mfenced></mrow><annotation encoding="application/x-tex">{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})</annotation></semantics></math>. Finally, we let <math alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math> be a finite <math alttext="{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})" display="inline"><semantics><mrow><msubsup><mi>U</mi><mi>ϵ</mi><mi>res</mi></msubsup><mo>⁢</mo><mfenced close=")" open="("><mi mathvariant="fraktur">g</mi></mfenced></mrow><annotation encoding="application/x-tex">{U_{\epsilon}^{{\mathrm{res}}}}(\mathfrak{g})</annotation></semantics></math>-module.</p>
</div>

<div class="para" id="p4">
<p class="p">For any <math alttext="\lambda\in P(\mathfrak{g})" display="inline"><semantics><mrow><mi>λ</mi><mo>∈</mo><mrow><mi>P</mi><mo>⁢</mo><mfenced close=")" open="("><mi mathvariant="fraktur">g</mi></mfenced></mrow></mrow><annotation encoding="application/x-tex">\lambda\in P(\mathfrak{g})</annotation></semantics></math> and <math alttext="\sigma\in{\{-1,1\}}^{n}" display="inline"><semantics><mrow><mi>σ</mi><mo>∈</mo><msup><mfenced close="}" open="{"><mrow><mrow><mo>-</mo><mn>1</mn></mrow><mo>,</mo><mn>1</mn></mrow></mfenced><mi>n</mi></msup></mrow><annotation encoding="application/x-tex">\sigma\in{\{-1,1\}}^{n}</annotation></semantics></math> define</p>
</div>

<div class="para" id="p5">
<table class="equation">
	<tbody>
		<tr class="equation baseline" id="Ch0.Ex1">
			<td class="eqpad"> </td>
			<td class="center" colspan="1"><math alttext="V_{{\sigma,\lambda}}=\bigcap _{{1\leq i\leq n}}{\operatorname{Ker}{\left(K_{i}-\sigma _{i}\epsilon _{i}^{{\lambda(\alpha _{i}^{\vee})}}1\right)}\cap\operatorname{Ker}{{\left({\genfrac{[}{]}{0.0pt}{0}{{K_{i}};{0}}{m_{i}}}_{{\epsilon _{i}}}-\Delta _{i}(\lambda)\left\lfloor\frac{\lambda(\alpha _{i}^{\vee})}{m_{i}}\right\rfloor 1\right)}}}" display="block"><semantics><mrow><msub><mi>V</mi><mrow><mi>σ</mi><mo>,</mo><mi>λ</mi></mrow></msub><mo>=</mo><mrow><mrow><munder><mo movablelimits="false">⋂</mo><mrow><mn>1</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mi>n</mi></mrow></munder><mo>Ker</mo><mo>⁡</mo><mfenced close=")" open="("><mrow><msub><mi>K</mi><mi>i</mi></msub><mo>-</mo><mrow><msub><mi>σ</mi><mi>i</mi></msub><mo>⁢</mo><msubsup><mi>ϵ</mi><mi>i</mi><mrow><mi>λ</mi><mo>⁢</mo><mfenced close=")" open="("><msubsup><mi>α</mi><mi>i</mi><mo>∨</mo></msubsup></mfenced></mrow></msubsup><mo>⁢</mo><mn>1</mn></mrow></mrow></mfenced></mrow><mo>∩</mo><mrow><mo>Ker</mo><mo>⁡</mo><mfenced close=")" open="("><mrow><msub><mfenced close="]" open="["><mtable columnspacing="0.4em" rowspacing="0.2ex"><mtr><mtd><mrow><msub><mi>K</mi><mi>i</mi></msub><mo>;</mo><mn>0</mn></mrow></mtd></mtr><mtr><mtd><msub><mi>m</mi><mi>i</mi></msub></mtd></mtr></mtable></mfenced><msub><mi>ϵ</mi><mi>i</mi></msub></msub><mo>-</mo><mrow><msub><mi mathvariant="normal">Δ</mi><mi>i</mi></msub><mo>⁢</mo><mfenced close=")" open="("><mi>λ</mi></mfenced><mo>⁢</mo><mfenced close="⌋" open="⌊"><mfrac><mrow><mi>λ</mi><mo>⁢</mo><mfenced close=")" open="("><msubsup><mi>α</mi><mi>i</mi><mo>∨</mo></msubsup></mfenced></mrow><msub><mi>m</mi><mi>i</mi></msub></mfrac></mfenced><mo>⁢</mo><mn>1</mn></mrow></mrow></mfenced></mrow></mrow></mrow><annotation encoding="application/x-tex">V_{{\sigma,\lambda}}=\bigcap _{{1\leq i\leq n}}{\operatorname{Ker}{\left(K_{i}-\sigma _{i}\epsilon _{i}^{{\lambda(\alpha _{i}^{\vee})}}1\right)}\cap\operatorname{Ker}{{\left({\genfrac{[}{]}{0.0pt}{0}{{K_{i}};{0}}{m_{i}}}_{{\epsilon _{i}}}-\Delta _{i}(\lambda)\left\lfloor\frac{\lambda(\alpha _{i}^{\vee})}{m_{i}}\right\rfloor 1\right)}}}</annotation></semantics></math></td>
			<td class="eqpad"> </td>
		</tr>
	</tbody>
</table>
</div>

<div class="para" id="p6">
<p class="p">where <math alttext="\forall i,\Delta _{i}(\lambda)={(-1)}^{{m_{i}+1}}\sigma _{i}^{{m_{i}}}{(\epsilon _{i}^{{m_{i}}})}^{{\lambda(\alpha _{i}^{\vee})+1}}" display="inline"><semantics><mrow><mrow><mrow><mi mathvariant="normal">∀</mi><mi>i</mi></mrow><mo>,</mo><mrow><msub><mi mathvariant="normal">Δ</mi><mi>i</mi></msub><mo>⁢</mo><mfenced close=")" open="("><mi>λ</mi></mfenced></mrow></mrow><mo>=</mo><mrow><msup><mfenced close=")" open="("><mrow><mo>-</mo><mn>1</mn></mrow></mfenced><mrow><msub><mi>m</mi><mi>i</mi></msub><mo>+</mo><mn>1</mn></mrow></msup><mo>⁢</mo><msubsup><mi>σ</mi><mi>i</mi><msub><mi>m</mi><mi>i</mi></msub></msubsup><mo>⁢</mo><msup><mfenced close=")" open="("><msubsup><mi>ϵ</mi><mi>i</mi><msub><mi>m</mi><mi>i</mi></msub></msubsup></mfenced><mrow><mrow><mi>λ</mi><mo>⁢</mo><mfenced close=")" open="("><msubsup><mi>α</mi><mi>i</mi><mo>∨</mo></msubsup></mfenced></mrow><mo>+</mo><mn>1</mn></mrow></msup></mrow></mrow><annotation encoding="application/x-tex">\forall i,\Delta _{i}(\lambda)={(-1)}^{{m_{i}+1}}\sigma _{i}^{{m_{i}}}{(\epsilon _{i}^{{m_{i}}})}^{{\lambda(\alpha _{i}^{\vee})+1}}</annotation></semantics></math></p>
</div>

<div class="para" id="p7">
<p class="p">For any <math alttext="1\leq j\leq n" display="inline"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>j</mi><mo>≤</mo><mi>n</mi></mrow><annotation encoding="application/x-tex">1\leq j\leq n</annotation></semantics></math>, we have</p>
</div>

<div class="para" id="p8">
<table class="equation">
	<tbody>
		<tr class="equation baseline" id="Ch0.Ex2">
			<td class="eqpad"> </td>
			<td class="center" colspan="1"><math alttext="X_{j}^{\pm}V_{{\sigma\lambda}}\subseteq V_{{\sigma,\lambda\pm\alpha _{j}}}" display="block"><semantics><mrow><mrow><msubsup><mi>X</mi><mi>j</mi><mo>±</mo></msubsup><mo>⁢</mo><msub><mi>V</mi><mrow><mi>σ</mi><mo>⁢</mo><mi>λ</mi></mrow></msub></mrow><mo>⊆</mo><msub><mi>V</mi><mrow><mi>σ</mi><mo>,</mo><mrow><mi>λ</mi><mo>±</mo><msub><mi>α</mi><mi>j</mi></msub></mrow></mrow></msub></mrow><annotation encoding="application/x-tex">X_{j}^{\pm}V_{{\sigma\lambda}}\subseteq V_{{\sigma,\lambda\pm\alpha _{j}}}</annotation></semantics></math></td>
			<td class="eqpad"> </td>
		</tr>
	</tbody>
</table>

<table class="equation">
	<tbody>
		<tr class="equation baseline" id="Ch0.Ex3">
			<td class="eqpad"> </td>
			<td class="center" colspan="1"><math alttext="{(X_{j}^{\pm})}^{{(m_{j})}}V_{{\sigma\lambda}}\subseteq V_{{\sigma,\lambda\pm m_{j}\alpha _{j}}}" display="block"><semantics><mrow><mrow><msup><mfenced close=")" open="("><msubsup><mi>X</mi><mi>j</mi><mo>±</mo></msubsup></mfenced><mfenced close=")" open="("><msub><mi>m</mi><mi>j</mi></msub></mfenced></msup><mo>⁢</mo><msub><mi>V</mi><mrow><mi>σ</mi><mo>⁢</mo><mi>λ</mi></mrow></msub></mrow><mo>⊆</mo><msub><mi>V</mi><mrow><mi>σ</mi><mo>,</mo><mrow><mi>λ</mi><mo>±</mo><mrow><msub><mi>m</mi><mi>j</mi></msub><mo>⁢</mo><msub><mi>α</mi><mi>j</mi></msub></mrow></mrow></mrow></msub></mrow><annotation encoding="application/x-tex">{(X_{j}^{\pm})}^{{(m_{j})}}V_{{\sigma\lambda}}\subseteq V_{{\sigma,\lambda\pm m_{j}\alpha _{j}}}</annotation></semantics></math></td>
			<td class="eqpad"> </td>
		</tr>
	</tbody>
</table>
</div>

<div class="para" id="p9">
<p class="p">Moreover if <math alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math> is simple, <math alttext="V=\bigoplus _{{\sigma,\lambda}}V_{{\sigma,\lambda}}" display="inline"><semantics><mrow><mi>V</mi><mo>=</mo><mrow><msub><mo>⊕</mo><mrow><mi>σ</mi><mo>,</mo><mi>λ</mi></mrow></msub><msub><mi>V</mi><mrow><mi>σ</mi><mo>,</mo><mi>λ</mi></mrow></msub></mrow></mrow><annotation encoding="application/x-tex">V=\bigoplus _{{\sigma,\lambda}}V_{{\sigma,\lambda}}</annotation></semantics></math>.</p>
</div>

<div class="para" id="p10">
<p class="p"><math alttext="\square" display="inline"><semantics><mi mathvariant="normal">□</mi><annotation encoding="application/x-tex">\square</annotation></semantics></math></p>
</div>



{% endraw %}

