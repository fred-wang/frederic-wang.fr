---
layout: post
title: "Exercises in Set Theory: Classical Independence Results"
tags: maths
---

{% raw %}

  
<div id="p1" class="ltx_para">
<p class="ltx_p">I worked on Chapter 13 and 14 of Thomas Jech’s book ‘‘Set Theory’’.</p>
</div>
<div id="p2" class="ltx_para">
<p class="ltx_p">Doing the exercises from these chapters gave me the opportunity to come back
to the ‘‘classical’’ results about the independence of the Axiom of Choice
and (Generalized) Continuum Hypothesis by Kurt Gödel and Paul Cohen.
It’s funny to note that it’s easier to prove that AC holds in <math id="p2.m1" class="ltx_Math" alttext="L" display="inline"><semantics><mi>L</mi><annotation encoding="application/x-tex">L</annotation></semantics></math>
(essentially,
the definition by ordinal induction provides the
well-ordering of the class of contructible sets) than to prove that GCH
holds in <math id="p2.m2" class="ltx_Math" alttext="L" display="inline"><semantics><mi>L</mi><annotation encoding="application/x-tex">L</annotation></semantics></math> (you rely on AC in <math id="p2.m3" class="ltx_Math" alttext="L" display="inline"><semantics><mi>L</mi><annotation encoding="application/x-tex">L</annotation></semantics></math> and on the technical condensation
lemma). Actually, I believe Gödel found his proof for AC
one or two years after the one for GCH.
On the other hand, it is easy to make GCH fails (just add
<math id="p2.m4" class="ltx_Math" alttext="\aleph_{2}" display="inline"><semantics><msub><mi mathvariant="normal">ℵ</mi><mn>2</mn></msub><annotation encoding="application/x-tex">\aleph_{2}</annotation></semantics></math> Cohen reals by Forcing) but more difficult to make AC fails
(e.g. AC is preserved by Forcing). This can be interpreted as AC being
more ‘‘natural’’ than GCH.</p>
</div>
<div id="p3" class="ltx_para">
<p class="ltx_p">After reading the chapters again and now I analyzed in details
the claims, I’m now convinced about the correctness of the proof.
There are only two points I
didn’t verify precisely about the Forcing method (namely that all axioms of
predicate calculus and rules of inference are compatible
with the Forcing method ; that the Forcing/Generic Model theorems can
be transported from the Boolean Algebra case to the general case) but
these do not seem too difficult. Here are some notes about claims that were
not obvious to me
at the first reading. As usual, I hope they might be useful to
the readers of that blog:</p>
</div>
<div id="p4" class="ltx_para">
<ol id="I1" class="ltx_enumerate">
<li id="I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">1.</span> 
<div id="I1.i1.p1" class="ltx_para">
<p class="ltx_p">In the first page of chapter 13, it is claimed that
for any set <math id="I1.i1.p1.m1" class="ltx_Math" alttext="M" display="inline"><semantics><mi>M</mi><annotation encoding="application/x-tex">M</annotation></semantics></math>, <math id="I1.i1.p1.m2" class="ltx_Math" alttext="M\in\mathrm{def}(M)" display="inline"><semantics><mrow><mi>M</mi><mo>∈</mo><mrow><mi>def</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">M\in\mathrm{def}(M)</annotation></semantics></math> and
<math id="I1.i1.p1.m3" class="ltx_Math" alttext="M\subseteq\mathrm{def}(M)\subseteq\operatorname{\mathcal{P}}(M)" display="inline"><semantics><mrow><mi>M</mi><mo>⊆</mo><mrow><mi>def</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow><mo>⊆</mo><mrow><mo class="ltx_font_mathcaligraphic">𝒫</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">M\subseteq\mathrm{def}(M)\subseteq\operatorname{\mathcal{P}}(M)</annotation></semantics></math>. The first statement
is always true because
<math id="I1.i1.p1.m4" class="ltx_Math" alttext="M=\{x\in M:(M,\in)\models x=x\}\in\mathrm{def}(M)" display="inline"><semantics><mrow><mi>M</mi><mo>=</mo><mrow><mo stretchy="false">{</mo><mrow><mi>x</mi><mo>∈</mo><mi>M</mi></mrow><mo>:</mo><mrow><mrow><mo stretchy="false">(</mo><mi>M</mi><mo>,</mo><mo>∈</mo><mo stretchy="false">)</mo></mrow><mo>⊧</mo><mi>x</mi><mo>=</mo><mi>x</mi></mrow><mo stretchy="false">}</mo></mrow><mo>∈</mo><mrow><mi>def</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">M=\{x\in M:(M,\in)\models x=x\}\in\mathrm{def}(M)</annotation></semantics></math> and
<math id="I1.i1.p1.m5" class="ltx_Math" alttext="{(x=x)}^{(M,\in)}" display="inline"><semantics><msup><mrow><mo stretchy="false">(</mo><mi>x</mi><mo>=</mo><mi>x</mi><mo stretchy="false">)</mo></mrow><mrow><mo stretchy="false">(</mo><mi>M</mi><mo>,</mo><mo>∈</mo><mo stretchy="false">)</mo></mrow></msup><annotation encoding="application/x-tex">{(x=x)}^{(M,\in)}</annotation></semantics></math> is <math id="I1.i1.p1.m6" class="ltx_Math" alttext="x=x" display="inline"><semantics><mrow><mi>x</mi><mo>=</mo><mi>x</mi></mrow><annotation encoding="application/x-tex">x=x</annotation></semantics></math> by definition. However, the second
statement can only be true if <math id="I1.i1.p1.m7" class="ltx_Math" alttext="M" display="inline"><semantics><mi>M</mi><annotation encoding="application/x-tex">M</annotation></semantics></math> is transitive
(since that implies <math id="I1.i1.p1.m8" class="ltx_Math" alttext="M\subseteq\operatorname{\mathcal{P}}(M)" display="inline"><semantics><mrow><mi>M</mi><mo>⊆</mo><mrow><mo class="ltx_font_mathcaligraphic">𝒫</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">M\subseteq\operatorname{\mathcal{P}}(M)</annotation></semantics></math>).
Indeed, if <math id="I1.i1.p1.m9" class="ltx_Math" alttext="M" display="inline"><semantics><mi>M</mi><annotation encoding="application/x-tex">M</annotation></semantics></math> is transitive then for all
<math id="I1.i1.p1.m10" class="ltx_Math" alttext="a\in M" display="inline"><semantics><mrow><mi>a</mi><mo>∈</mo><mi>M</mi></mrow><annotation encoding="application/x-tex">a\in M</annotation></semantics></math> we have <math id="I1.i1.p1.m11" class="ltx_Math" alttext="a\subseteq M" display="inline"><semantics><mrow><mi>a</mi><mo>⊆</mo><mi>M</mi></mrow><annotation encoding="application/x-tex">a\subseteq M</annotation></semantics></math> and since <math id="I1.i1.p1.m12" class="ltx_Math" alttext="x\in a" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><mi>a</mi></mrow><annotation encoding="application/x-tex">x\in a</annotation></semantics></math> is <math id="I1.i1.p1.m13" class="ltx_Math" alttext="\Delta_{0}" display="inline"><semantics><msub><mi mathvariant="normal">Δ</mi><mn>0</mn></msub><annotation encoding="application/x-tex">\Delta_{0}</annotation></semantics></math> we
get <math id="I1.i1.p1.m14" class="ltx_Math" alttext="a=\{x\in M:(M,\in)\models x\in a\}\in\mathrm{def}(M)" display="inline"><semantics><mrow><mi>a</mi><mo>=</mo><mrow><mo stretchy="false">{</mo><mrow><mi>x</mi><mo>∈</mo><mi>M</mi></mrow><mo>:</mo><mrow><mrow><mo stretchy="false">(</mo><mi>M</mi><mo>,</mo><mo>∈</mo><mo stretchy="false">)</mo></mrow><mo>⊧</mo><mi>x</mi><mo>∈</mo><mi>a</mi></mrow><mo stretchy="false">}</mo></mrow><mo>∈</mo><mrow><mi>def</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">a=\{x\in M:(M,\in)\models x\in a\}\in\mathrm{def}(M)</annotation></semantics></math>.
If moreover we consider <math id="I1.i1.p1.m15" class="ltx_Math" alttext="x\in X\in\mathrm{def}(M)" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><mi>X</mi><mo>∈</mo><mrow><mi>def</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">x\in X\in\mathrm{def}(M)</annotation></semantics></math> then
<math id="I1.i1.p1.m16" class="ltx_Math" alttext="x\in X\subseteq M" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><mi>X</mi><mo>⊆</mo><mi>M</mi></mrow><annotation encoding="application/x-tex">x\in X\subseteq M</annotation></semantics></math> so <math id="I1.i1.p1.m17" class="ltx_Math" alttext="x\in M\subseteq\mathrm{def}(M)" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><mi>M</mi><mo>⊆</mo><mrow><mi>def</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">x\in M\subseteq\mathrm{def}(M)</annotation></semantics></math> and
<math id="I1.i1.p1.m18" class="ltx_Math" alttext="\mathrm{def}(M)" display="inline"><semantics><mrow><mi>def</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\mathrm{def}(M)</annotation></semantics></math> is also transitive. Hence the transitivity of the
<math id="I1.i1.p1.m19" class="ltx_Math" alttext="L_{\alpha}" display="inline"><semantics><msub><mi>L</mi><mi>α</mi></msub><annotation encoding="application/x-tex">L_{\alpha}</annotation></semantics></math> can still be shown by ordinal induction.</p>
</div>
</li>
<li id="I1.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">2.</span> 
<div id="I1.i2.p1" class="ltx_para">
<p class="ltx_p">The proof of lemma 13.7 can not be done exactly by induction on
the complexity of <math id="I1.i2.p1.m1" class="ltx_Math" alttext="G" display="inline"><semantics><mi>G</mi><annotation encoding="application/x-tex">G</annotation></semantics></math>, as suggested. For example to prove (ii)
for <math id="I1.i2.p1.m2" class="ltx_Math" alttext="G=G_{2}=\cdot\times\cdot" display="inline"><semantics><mrow><mi>G</mi><mo>=</mo><msub><mi>G</mi><mn>2</mn></msub><mo>=</mo><mo>⋅</mo><mo>×</mo><mo>⋅</mo></mrow><annotation encoding="application/x-tex">G=G_{2}=\cdot\times\cdot</annotation></semantics></math>, we would consider
<math id="I1.i2.p1.m3" class="ltx_Math" alttext="\exists u\in F(...)\times H(...)\varphi(u)\Leftrightarrow\exists a\in F(...),%
\exists b\in H(...),\varphi((a,b))" display="inline"><semantics><mrow><mrow><mrow><mo>∃</mo><mi>u</mi></mrow><mo>∈</mo><mrow><mrow><mrow><mi>F</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi mathvariant="normal">…</mi><mo stretchy="false">)</mo></mrow></mrow><mo>×</mo><mi>H</mi></mrow><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi mathvariant="normal">…</mi><mo stretchy="false">)</mo></mrow><mo>⁢</mo><mi>φ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>u</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>⇔</mo><mrow><mrow><mrow><mo>∃</mo><mi>a</mi></mrow><mo>∈</mo><mrow><mi>F</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi mathvariant="normal">…</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>,</mo><mrow><mrow><mo>∃</mo><mi>b</mi></mrow><mo>∈</mo><mrow><mrow><mi>H</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi mathvariant="normal">…</mi><mo stretchy="false">)</mo></mrow></mrow><mo>,</mo><mrow><mi>φ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mo stretchy="false">(</mo><mi>a</mi><mo>,</mo><mi>b</mi><mo stretchy="false">)</mo></mrow><mo stretchy="false">)</mo></mrow></mrow></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\exists u\in F(...)\times H(...)\varphi(u)\Leftrightarrow\exists a\in F(...),%
\exists b\in H(...),\varphi((a,b))</annotation></semantics></math>
and would like to say that <math id="I1.i2.p1.m4" class="ltx_Math" alttext="\varphi((a,b))" display="inline"><semantics><mrow><mi>φ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mrow><mo stretchy="false">(</mo><mi>a</mi><mo>,</mo><mi>b</mi><mo stretchy="false">)</mo></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">\varphi((a,b))</annotation></semantics></math> is <math id="I1.i2.p1.m5" class="ltx_Math" alttext="\Delta_{0}" display="inline"><semantics><msub><mi mathvariant="normal">Δ</mi><mn>0</mn></msub><annotation encoding="application/x-tex">\Delta_{0}</annotation></semantics></math>. Nevertheless,
we can not
deduce that from the induction hypothesis. Hence the right thing to do is
to prove the lemma for <math id="I1.i2.p1.m6" class="ltx_Math" alttext="G_{1}=\{\cdot,\cdot\}" display="inline"><semantics><mrow><msub><mi>G</mi><mn>1</mn></msub><mo>=</mo><mrow><mo stretchy="false">{</mo><mo>⋅</mo><mo>,</mo><mo>⋅</mo><mo stretchy="false">}</mo></mrow></mrow><annotation encoding="application/x-tex">G_{1}=\{\cdot,\cdot\}</annotation></semantics></math> first and deduce the
lemma for <math id="I1.i2.p1.m7" class="ltx_Math" alttext="G=(\cdot,\cdot)" display="inline"><semantics><mrow><mi>G</mi><mo>=</mo><mrow><mo stretchy="false">(</mo><mo>⋅</mo><mo>,</mo><mo>⋅</mo><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">G=(\cdot,\cdot)</annotation></semantics></math> (and <math id="I1.i2.p1.m8" class="ltx_Math" alttext="G^{\prime}=(\cdot,\cdot,\cdot)" display="inline"><semantics><mrow><msup><mi>G</mi><mo>′</mo></msup><mo>=</mo><mrow><mo stretchy="false">(</mo><mo>⋅</mo><mo>,</mo><mo>⋅</mo><mo>,</mo><mo>⋅</mo><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">G^{\prime}=(\cdot,\cdot,\cdot)</annotation></semantics></math>). Then
we can proceed by induction.</p>
</div>
</li>
<li id="I1.i3" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">3.</span> 
<div id="I1.i3.p1" class="ltx_para">
<p class="ltx_p">In the proof of theorem 13.18, it is mentioned that the assumption</p>
</div>
<div id="I1.i3.p2" class="ltx_para">
<ol id="I1.I1" class="ltx_enumerate">
<li id="I1.I1.i1" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">(i)</span> 
<div id="I1.I1.i1.p1" class="ltx_para">
<p class="ltx_p"><math id="I1.I1.i1.p1.m1" class="ltx_Math" alttext="x&lt;_{\alpha}y" display="inline"><semantics><mrow><mi>x</mi><msub><mo>&lt;</mo><mi>α</mi></msub><mi>y</mi></mrow><annotation encoding="application/x-tex">x&lt;_{\alpha}y</annotation></semantics></math> implies <math id="I1.I1.i1.p1.m2" class="ltx_Math" alttext="x&lt;_{\beta}y" display="inline"><semantics><mrow><mi>x</mi><msub><mo>&lt;</mo><mi>β</mi></msub><mi>y</mi></mrow><annotation encoding="application/x-tex">x&lt;_{\beta}y</annotation></semantics></math></p>
</div>
</li>
<li id="I1.I1.i2" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">(ii)</span> 
<div id="I1.I1.i2.p1" class="ltx_para">
<p class="ltx_p"><math id="I1.I1.i2.p1.m1" class="ltx_Math" alttext="x\in L_{\alpha}" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><msub><mi>L</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">x\in L_{\alpha}</annotation></semantics></math> and <math id="I1.I1.i2.p1.m2" class="ltx_Math" alttext="y\in L_{\beta}\setminus L_{\alpha}" display="inline"><semantics><mrow><mi>y</mi><mo>∈</mo><mrow><msub><mi>L</mi><mi>β</mi></msub><mo>∖</mo><msub><mi>L</mi><mi>α</mi></msub></mrow></mrow><annotation encoding="application/x-tex">y\in L_{\beta}\setminus L_{\alpha}</annotation></semantics></math> implies
<math id="I1.I1.i2.p1.m3" class="ltx_Math" alttext="x&lt;_{\beta}y" display="inline"><semantics><mrow><mi>x</mi><msub><mo>&lt;</mo><mi>β</mi></msub><mi>y</mi></mrow><annotation encoding="application/x-tex">x&lt;_{\beta}y</annotation></semantics></math></p>
</div>
</li>
</ol>
</div>
<div id="I1.i3.p3" class="ltx_para">
<p class="ltx_p">implies that if <math id="I1.i3.p3.m1" class="ltx_Math" alttext="x\in y\in L_{\alpha}" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><mi>y</mi><mo>∈</mo><msub><mi>L</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">x\in y\in L_{\alpha}</annotation></semantics></math> then <math id="I1.i3.p3.m2" class="ltx_Math" alttext="x&lt;_{\alpha}y" display="inline"><semantics><mrow><mi>x</mi><msub><mo>&lt;</mo><mi>α</mi></msub><mi>y</mi></mrow><annotation encoding="application/x-tex">x&lt;_{\alpha}y</annotation></semantics></math>. To show that,
we consider <math id="I1.i3.p3.m3" class="ltx_Math" alttext="\beta\leq\alpha" display="inline"><semantics><mrow><mi>β</mi><mo>≤</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beta\leq\alpha</annotation></semantics></math> the least ordinal such that
<math id="I1.i3.p3.m4" class="ltx_Math" alttext="y\in L_{\beta}" display="inline"><semantics><mrow><mi>y</mi><mo>∈</mo><msub><mi>L</mi><mi>β</mi></msub></mrow><annotation encoding="application/x-tex">y\in L_{\beta}</annotation></semantics></math>. In particular, <math id="I1.i3.p3.m5" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math> is not limit
(<math id="I1.i3.p3.m6" class="ltx_Math" alttext="L_{0}=\emptyset" display="inline"><semantics><mrow><msub><mi>L</mi><mn>0</mn></msub><mo>=</mo><mi mathvariant="normal">∅</mi></mrow><annotation encoding="application/x-tex">L_{0}=\emptyset</annotation></semantics></math> and if <math id="I1.i3.p3.m7" class="ltx_Math" alttext="y\in L_{\beta}" display="inline"><semantics><mrow><mi>y</mi><mo>∈</mo><msub><mi>L</mi><mi>β</mi></msub></mrow><annotation encoding="application/x-tex">y\in L_{\beta}</annotation></semantics></math> for some limit <math id="I1.i3.p3.m8" class="ltx_Math" alttext="\beta&gt;0" display="inline"><semantics><mrow><mi>β</mi><mo>&gt;</mo><mn>0</mn></mrow><annotation encoding="application/x-tex">\beta&gt;0</annotation></semantics></math>
then there is <math id="I1.i3.p3.m9" class="ltx_Math" alttext="\gamma&lt;\beta" display="inline"><semantics><mrow><mi>γ</mi><mo>&lt;</mo><mi>β</mi></mrow><annotation encoding="application/x-tex">\gamma&lt;\beta</annotation></semantics></math> such that <math id="I1.i3.p3.m10" class="ltx_Math" alttext="y\in L_{\gamma}" display="inline"><semantics><mrow><mi>y</mi><mo>∈</mo><msub><mi>L</mi><mi>γ</mi></msub></mrow><annotation encoding="application/x-tex">y\in L_{\gamma}</annotation></semantics></math>) and we can
write it <math id="I1.i3.p3.m11" class="ltx_Math" alttext="\beta=\gamma+1" display="inline"><semantics><mrow><mi>β</mi><mo>=</mo><mrow><mi>γ</mi><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\beta=\gamma+1</annotation></semantics></math>. We have
<math id="I1.i3.p3.m12" class="ltx_Math" alttext="y\in L_{\beta}=L_{\gamma+1}" display="inline"><semantics><mrow><mi>y</mi><mo>∈</mo><msub><mi>L</mi><mi>β</mi></msub><mo>=</mo><msub><mi>L</mi><mrow><mi>γ</mi><mo>+</mo><mn>1</mn></mrow></msub></mrow><annotation encoding="application/x-tex">y\in L_{\beta}=L_{\gamma+1}</annotation></semantics></math> so there is a formula <math id="I1.i3.p3.m13" class="ltx_Math" alttext="\varphi" display="inline"><semantics><mi>φ</mi><annotation encoding="application/x-tex">\varphi</annotation></semantics></math> and
elements <math id="I1.i3.p3.m14" class="ltx_Math" alttext="a_{1},...,a_{n}\in L_{\gamma}" display="inline"><semantics><mrow><mrow><msub><mi>a</mi><mn>1</mn></msub><mo>,</mo><mi mathvariant="normal">…</mi><mo>,</mo><msub><mi>a</mi><mi>n</mi></msub></mrow><mo>∈</mo><msub><mi>L</mi><mi>γ</mi></msub></mrow><annotation encoding="application/x-tex">a_{1},...,a_{n}\in L_{\gamma}</annotation></semantics></math> such that
<math id="I1.i3.p3.m15" class="ltx_Math" alttext="x\in y=\{z\in L_{\gamma}:(L_{\gamma},\in)\models\varphi(z,a_{1},...,a_{n})\}" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><mi>y</mi><mo>=</mo><mrow><mo stretchy="false">{</mo><mrow><mi>z</mi><mo>∈</mo><msub><mi>L</mi><mi>γ</mi></msub></mrow><mo>:</mo><mrow><mrow><mo stretchy="false">(</mo><msub><mi>L</mi><mi>γ</mi></msub><mo>,</mo><mo>∈</mo><mo stretchy="false">)</mo></mrow><mo>⊧</mo><mrow><mi>φ</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>z</mi><mo>,</mo><msub><mi>a</mi><mn>1</mn></msub><mo>,</mo><mi mathvariant="normal">…</mi><mo>,</mo><msub><mi>a</mi><mi>n</mi></msub><mo stretchy="false">)</mo></mrow></mrow></mrow><mo stretchy="false">}</mo></mrow></mrow><annotation encoding="application/x-tex">x\in y=\{z\in L_{\gamma}:(L_{\gamma},\in)\models\varphi(z,a_{1},...,a_{n})\}</annotation></semantics></math>. Hence <math id="I1.i3.p3.m16" class="ltx_Math" alttext="x\in L_{\gamma}" display="inline"><semantics><mrow><mi>x</mi><mo>∈</mo><msub><mi>L</mi><mi>γ</mi></msub></mrow><annotation encoding="application/x-tex">x\in L_{\gamma}</annotation></semantics></math>. Moreover
by minimality of <math id="I1.i3.p3.m17" class="ltx_Math" alttext="\beta" display="inline"><semantics><mi>β</mi><annotation encoding="application/x-tex">\beta</annotation></semantics></math>, <math id="I1.i3.p3.m18" class="ltx_Math" alttext="y\in L_{\beta}\setminus L_{\gamma}" display="inline"><semantics><mrow><mi>y</mi><mo>∈</mo><mrow><msub><mi>L</mi><mi>β</mi></msub><mo>∖</mo><msub><mi>L</mi><mi>γ</mi></msub></mrow></mrow><annotation encoding="application/x-tex">y\in L_{\beta}\setminus L_{\gamma}</annotation></semantics></math> so
by (ii) we have <math id="I1.i3.p3.m19" class="ltx_Math" alttext="x&lt;_{\beta}y" display="inline"><semantics><mrow><mi>x</mi><msub><mo>&lt;</mo><mi>β</mi></msub><mi>y</mi></mrow><annotation encoding="application/x-tex">x&lt;_{\beta}y</annotation></semantics></math> and by (i) <math id="I1.i3.p3.m20" class="ltx_Math" alttext="x&lt;_{\alpha}y" display="inline"><semantics><mrow><mi>x</mi><msub><mo>&lt;</mo><mi>α</mi></msub><mi>y</mi></mrow><annotation encoding="application/x-tex">x&lt;_{\alpha}y</annotation></semantics></math>.</p>
</div>
</li>
<li id="I1.i4" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">4.</span> 
<div id="I1.i4.p1" class="ltx_para">
<p class="ltx_p">In lemma 14.18, we have expressions that seem
ill-defined for example <math id="I1.i4.p1.m1" class="ltx_Math" alttext="a_{u}(t)" display="inline"><semantics><mrow><msub><mi>a</mi><mi>u</mi></msub><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>t</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="application/x-tex">a_{u}(t)</annotation></semantics></math> where <math id="I1.i4.p1.m2" class="ltx_Math" alttext="t\notin\operatorname{dom}(a_{u})" display="inline"><semantics><mrow><mi>t</mi><mo>∉</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><msub><mi>a</mi><mi>u</mi></msub><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">t\notin\operatorname{dom}(a_{u})</annotation></semantics></math>.
This happens in other places, like lemma 14.17 or definition 14.27.
The trick
is to understand that the functions are extended by 0. Indeed, for any
<math id="I1.i4.p1.m3" class="ltx_Math" alttext="x,y\in V^{B}" display="inline"><semantics><mrow><mrow><mi>x</mi><mo>,</mo><mi>y</mi></mrow><mo>∈</mo><msup><mi>V</mi><mi>B</mi></msup></mrow><annotation encoding="application/x-tex">x,y\in V^{B}</annotation></semantics></math> if <math id="I1.i4.p1.m4" class="ltx_Math" alttext="x\subseteq y" display="inline"><semantics><mrow><mi>x</mi><mo>⊆</mo><mi>y</mi></mrow><annotation encoding="application/x-tex">x\subseteq y</annotation></semantics></math> and
<math id="I1.i4.p1.m5" class="ltx_Math" alttext="\forall t\in\operatorname{dom}(y)\setminus\operatorname{dom}(x),y(t)=0" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>t</mi></mrow><mo>∈</mo><mrow><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>y</mi><mo stretchy="false">)</mo></mrow></mrow><mo>∖</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></mrow><mo>,</mo><mrow><mrow><mi>y</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>t</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mn>0</mn></mrow></mrow><annotation encoding="application/x-tex">\forall t\in\operatorname{dom}(y)\setminus\operatorname{dom}(x),y(t)=0</annotation></semantics></math> then</p>
</div>
<div id="I1.i4.p2" class="ltx_para">
<table id="S0.Ex1" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex1.m1" class="ltx_Math" alttext="\begin{gathered}\displaystyle\|y\subseteq x\|\\
\displaystyle=\prod_{t\in\operatorname{dom}(y)}\left(-y(t)+{\|t\in x\|}\right)%
\\
\displaystyle=\prod_{t\in\operatorname{dom}(x)}\left(-x(t)+{\|t\in x\|}\right)%
\\
\displaystyle=\|x\subseteq x\|=1\end{gathered}" display="block"><semantics><mtable displaystyle="true" rowspacing="0pt"><mtr><mtd columnalign="center"><mrow><mo>∥</mo><mi>y</mi><mo>⊆</mo><mi>x</mi><mo>∥</mo></mrow></mtd></mtr><mtr><mtd columnalign="center"><mrow><mo>=</mo><munder><mo largeop="true" movablelimits="false" symmetric="true">∏</mo><mrow><mi>t</mi><mo>∈</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>y</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></munder><mrow><mo>(</mo><mo>-</mo><mi>y</mi><mrow><mo stretchy="false">(</mo><mi>t</mi><mo stretchy="false">)</mo></mrow><mo>+</mo><mo>∥</mo><mi>t</mi><mo>∈</mo><mi>x</mi><mo>∥</mo><mo>)</mo></mrow></mrow></mtd></mtr><mtr><mtd columnalign="center"><mrow><mo>=</mo><munder><mo largeop="true" movablelimits="false" symmetric="true">∏</mo><mrow><mi>t</mi><mo>∈</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></munder><mrow><mo>(</mo><mo>-</mo><mi>x</mi><mrow><mo stretchy="false">(</mo><mi>t</mi><mo stretchy="false">)</mo></mrow><mo>+</mo><mo>∥</mo><mi>t</mi><mo>∈</mo><mi>x</mi><mo>∥</mo><mo>)</mo></mrow></mrow></mtd></mtr><mtr><mtd columnalign="center"><mrow><mo>=</mo><mo>∥</mo><mi>x</mi><mo>⊆</mo><mi>x</mi><mo>∥</mo><mo>=</mo><mn>1</mn></mrow></mtd></mtr></mtable><annotation encoding="application/x-tex">\begin{gathered}\displaystyle\|y\subseteq x\|\\
\displaystyle=\prod_{t\in\operatorname{dom}(y)}\left(-y(t)+{\|t\in x\|}\right)%
\\
\displaystyle=\prod_{t\in\operatorname{dom}(x)}\left(-x(t)+{\|t\in x\|}\right)%
\\
\displaystyle=\|x\subseteq x\|=1\end{gathered}</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="I1.i4.p3" class="ltx_para">
<p class="ltx_p">and similarly we get <math id="I1.i4.p3.m1" class="ltx_Math" alttext="\|x=y\|=1" display="inline"><semantics><mrow><mo>∥</mo><mi>x</mi><mo>=</mo><mi>y</mi><mo>∥</mo><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\|x=y\|=1</annotation></semantics></math>. Then we can use the inequality
page 207 (<math id="I1.i4.p3.m2" class="ltx_Math" alttext="\|\varphi(x)\|=\|x=y\|\cdot\|\varphi(x)\|\leq\|\varphi(y)\|=\|x=y\|\cdot\|%
\varphi(y)\|\leq\|\varphi(x)\|" display="inline"><semantics><mrow><mo>∥</mo><mi>φ</mi><mrow><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow><mo>∥</mo><mo>=</mo><mo>∥</mo><mi>x</mi><mo>=</mo><mi>y</mi><mo>∥</mo><mo>⋅</mo><mo>∥</mo><mi>φ</mi><mrow><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow><mo>∥</mo><mo>≤</mo><mo>∥</mo><mi>φ</mi><mrow><mo stretchy="false">(</mo><mi>y</mi><mo stretchy="false">)</mo></mrow><mo>∥</mo><mo>=</mo><mo>∥</mo><mi>x</mi><mo>=</mo><mi>y</mi><mo>∥</mo><mo>⋅</mo><mo>∥</mo><mi>φ</mi><mrow><mo stretchy="false">(</mo><mi>y</mi><mo stretchy="false">)</mo></mrow><mo>∥</mo><mo>≤</mo><mo>∥</mo><mi>φ</mi><mrow><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow><mo>∥</mo></mrow><annotation encoding="application/x-tex">\|\varphi(x)\|=\|x=y\|\cdot\|\varphi(x)\|\leq\|\varphi(y)\|=\|x=y\|\cdot\|%
\varphi(y)\|\leq\|\varphi(x)\|</annotation></semantics></math>) to
replace <math id="I1.i4.p3.m3" class="ltx_Math" alttext="x" display="inline"><semantics><mi>x</mi><annotation encoding="application/x-tex">x</annotation></semantics></math> by its extension <math id="I1.i4.p3.m4" class="ltx_Math" alttext="y" display="inline"><semantics><mi>y</mi><annotation encoding="application/x-tex">y</annotation></semantics></math>.</p>
</div>
</li>
<li id="I1.i5" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">5.</span> 
<div id="I1.i5.p1" class="ltx_para">
<p class="ltx_p">In lemma 14.23, the inequality</p>
</div>
<div id="I1.i5.p2" class="ltx_para">
<table id="S0.Ex2" class="ltx_equation ltx_eqn_table">

<tr class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_eqn_cell ltx_align_center"><math id="S0.Ex2.m1" class="ltx_Math" alttext="\|x\text{ is an ordinal}\|\leq\|x\in\check{\alpha}\|+\|x=\check{\alpha}\|+\|%
\check{\alpha}\in x\|" display="block"><semantics><mrow><mo>∥</mo><mi>x</mi><mtext> is an ordinal</mtext><mo>∥</mo><mo>≤</mo><mo>∥</mo><mi>x</mi><mo>∈</mo><mover accent="true"><mi>α</mi><mo stretchy="false">ˇ</mo></mover><mo>∥</mo><mo>+</mo><mo>∥</mo><mi>x</mi><mo>=</mo><mover accent="true"><mi>α</mi><mo stretchy="false">ˇ</mo></mover><mo>∥</mo><mo>+</mo><mo>∥</mo><mover accent="true"><mi>α</mi><mo stretchy="false">ˇ</mo></mover><mo>∈</mo><mi>x</mi><mo>∥</mo></mrow><annotation encoding="application/x-tex">\|x\text{ is an ordinal}\|\leq\|x\in\check{\alpha}\|+\|x=\check{\alpha}\|+\|%
\check{\alpha}\in x\|</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="I1.i5.p3" class="ltx_para">
<p class="ltx_p">seems obvious but I don’t believe that it can be proved so easily at
that point. For example the proof from chapter 2 requires at least the
Separation axiom and the <math id="I1.i5.p3.m1" class="ltx_Math" alttext="\Delta_{0}" display="inline"><semantics><msub><mi mathvariant="normal">Δ</mi><mn>0</mn></msub><annotation encoding="application/x-tex">\Delta_{0}</annotation></semantics></math> formulation from chapter 10 is based
on the Axiom of Regularity. To solve that issue, it seems to me that
the lemma should be moved after the proof that axioms of ZFC are valid
in <math id="I1.i5.p3.m2" class="ltx_Math" alttext="V^{B}" display="inline"><semantics><msup><mi>V</mi><mi>B</mi></msup><annotation encoding="application/x-tex">V^{B}</annotation></semantics></math>. This is not an issue since lemma 14.23 is only used much
later in lemma 14.31.</p>
</div>
</li>
<li id="I1.i6" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">6.</span> 
<div id="I1.i6.p1" class="ltx_para">
<p class="ltx_p">Many details could be added to the proof of theorem 14.24, but
let’s just mention Powerset. For any <math id="I1.i6.p1.m1" class="ltx_Math" alttext="u\in V^{B}" display="inline"><semantics><mrow><mi>u</mi><mo>∈</mo><msup><mi>V</mi><mi>B</mi></msup></mrow><annotation encoding="application/x-tex">u\in V^{B}</annotation></semantics></math>, some
<math id="I1.i6.p1.m2" class="ltx_Math" alttext="u^{\prime}\in\operatorname{dom}(Y)" display="inline"><semantics><mrow><msup><mi>u</mi><mo>′</mo></msup><mo>∈</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>Y</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">u^{\prime}\in\operatorname{dom}(Y)</annotation></semantics></math> is defined and satisfies
<math id="I1.i6.p1.m3" class="ltx_Math" alttext="\|u\subseteq X\|\leq\|u=u^{\prime}\|" display="inline"><semantics><mrow><mo>∥</mo><mi>u</mi><mo>⊆</mo><mi>X</mi><mo>∥</mo><mo>≤</mo><mo>∥</mo><mi>u</mi><mo>=</mo><msup><mi>u</mi><mo>′</mo></msup><mo>∥</mo></mrow><annotation encoding="application/x-tex">\|u\subseteq X\|\leq\|u=u^{\prime}\|</annotation></semantics></math> (this follows from the
definitions, using the Boolean inequality
<math id="I1.i6.p1.m4" class="ltx_Math" alttext="-a+b\leq-a+b\cdot a" display="inline"><semantics><mrow><mrow><mrow><mo>-</mo><mi>a</mi></mrow><mo>+</mo><mi>b</mi></mrow><mo>≤</mo><mrow><mrow><mo>-</mo><mi>a</mi></mrow><mo>+</mo><mrow><mi>b</mi><mo>⋅</mo><mi>a</mi></mrow></mrow></mrow><annotation encoding="application/x-tex">-a+b\leq-a+b\cdot a</annotation></semantics></math> to conclude).
Since moreover <math id="I1.i6.p1.m5" class="ltx_Math" alttext="\forall t\in\operatorname{dom}(Y),Y(t)=1" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>t</mi></mrow><mo>∈</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>Y</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>,</mo><mrow><mrow><mi>Y</mi><mo>⁢</mo><mrow><mo stretchy="false">(</mo><mi>t</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mn>1</mn></mrow></mrow><annotation encoding="application/x-tex">\forall t\in\operatorname{dom}(Y),Y(t)=1</annotation></semantics></math> we get
</p>
</div>
<div id="I1.i6.p2" class="ltx_para">
<table id="S0.Ex3" class="ltx_equationgroup ltx_eqn_table">

<tr id="S0.Ex3X" class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_td ltx_align_right ltx_eqn_cell"><math id="S0.Ex3X.m2" class="ltx_Math" alttext="\displaystyle\|u\subseteq X\|\implies\|u\in Y\|" display="inline"><semantics><mrow><mo>∥</mo><mi>u</mi><mo>⊆</mo><mi>X</mi><mo>∥</mo><mo>⟹</mo><mo>∥</mo><mi>u</mi><mo>∈</mo><mi>Y</mi><mo>∥</mo></mrow><annotation encoding="application/x-tex">\displaystyle\|u\subseteq X\|\implies\|u\in Y\|</annotation></semantics></math></td>
<td class="ltx_td ltx_align_left ltx_eqn_cell"><math id="S0.Ex3X.m3" class="ltx_Math" alttext="\displaystyle\geq-\|u=u^{\prime}\|+\sum_{t\in\operatorname{dom}(Y)}\left(\|u=t%
\|\cdot Y(t)\right)" display="inline"><semantics><mrow><mo>≥</mo><mo>-</mo><mo>∥</mo><mi>u</mi><mo>=</mo><msup><mi>u</mi><mo>′</mo></msup><mo>∥</mo><mo>+</mo><mstyle displaystyle="true"><munder><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>t</mi><mo>∈</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>Y</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></munder></mstyle><mrow><mo>(</mo><mo>∥</mo><mi>u</mi><mo>=</mo><mi>t</mi><mo>∥</mo><mo>⋅</mo><mi>Y</mi><mrow><mo stretchy="false">(</mo><mi>t</mi><mo stretchy="false">)</mo></mrow><mo>)</mo></mrow></mrow><annotation encoding="application/x-tex">\displaystyle\geq-\|u=u^{\prime}\|+\sum_{t\in\operatorname{dom}(Y)}\left(\|u=t%
\|\cdot Y(t)\right)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
<tr id="S0.Ex3Xa" class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_td ltx_eqn_cell"></td>
<td class="ltx_td ltx_align_left ltx_eqn_cell"><math id="S0.Ex3Xa.m2" class="ltx_Math" alttext="\displaystyle=\sum_{t\in\operatorname{dom}(Y)}-\left(\|u\neq t\|\cdot\|u=u^{%
\prime}\|\right)" display="inline"><semantics><mrow><mo>=</mo><mstyle displaystyle="true"><munder><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>t</mi><mo>∈</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>Y</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></munder></mstyle><mo>-</mo><mrow><mo>(</mo><mo>∥</mo><mi>u</mi><mo>≠</mo><mi>t</mi><mo>∥</mo><mo>⋅</mo><mo>∥</mo><mi>u</mi><mo>=</mo><msup><mi>u</mi><mo>′</mo></msup><mo>∥</mo><mo>)</mo></mrow></mrow><annotation encoding="application/x-tex">\displaystyle=\sum_{t\in\operatorname{dom}(Y)}-\left(\|u\neq t\|\cdot\|u=u^{%
\prime}\|\right)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
<tr id="S0.Ex3Xb" class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_td ltx_eqn_cell"></td>
<td class="ltx_td ltx_align_left ltx_eqn_cell"><math id="S0.Ex3Xb.m2" class="ltx_Math" alttext="\displaystyle\geq\sum_{t\in\operatorname{dom}(Y)}\|u^{\prime}=t\|=1" display="inline"><semantics><mrow><mo>≥</mo><mstyle displaystyle="true"><munder><mo largeop="true" movablelimits="false" symmetric="true">∑</mo><mrow><mi>t</mi><mo>∈</mo><mrow><mo>dom</mo><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>Y</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></munder></mstyle><mo>∥</mo><msup><mi>u</mi><mo>′</mo></msup><mo>=</mo><mi>t</mi><mo>∥</mo><mo>=</mo><mn>1</mn></mrow><annotation encoding="application/x-tex">\displaystyle\geq\sum_{t\in\operatorname{dom}(Y)}\|u^{\prime}=t\|=1</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
</li>
<li id="I1.i7" class="ltx_item" style="list-style-type:none;">
<span class="ltx_tag ltx_tag_enumerate">7.</span> 
<div id="I1.i7.p1" class="ltx_para">
<p class="ltx_p">In theorem 14.34, we prove that any <math id="I1.i7.p1.m1" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math> regular in
<math id="I1.i7.p1.m2" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math> remains regular in <math id="I1.i7.p1.m3" class="ltx_Math" alttext="V[G]" display="inline"><semantics><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="application/x-tex">V[G]</annotation></semantics></math> (the hard case is really
<math id="I1.i7.p1.m4" class="ltx_Math" alttext="\kappa" display="inline"><semantics><mi>κ</mi><annotation encoding="application/x-tex">\kappa</annotation></semantics></math> uncountable and this assumption is implicitely used later
to say that <math id="I1.i7.p1.m5" class="ltx_Math" alttext="\bigcup_{\alpha&lt;\lambda}A_{\alpha}" display="inline"><semantics><mrow><msub><mo largeop="true" mathsize="160%" stretchy="false" symmetric="true">⋃</mo><mrow><mi>α</mi><mo>&lt;</mo><mi>λ</mi></mrow></msub><msub><mi>A</mi><mi>α</mi></msub></mrow><annotation encoding="application/x-tex">\bigcup_{\alpha&lt;\lambda}A_{\alpha}</annotation></semantics></math> is bounded).
It may not be obvious why this is enough. First recall that
for any ordinal <math id="I1.i7.p1.m6" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>,
<math id="I1.i7.p1.m7" class="ltx_Math" alttext="\operatorname{cf}^{V[G]}(\alpha)\leq\operatorname{cf}^{V}(\alpha)" display="inline"><semantics><mrow><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\operatorname{cf}^{V[G]}(\alpha)\leq\operatorname{cf}^{V}(\alpha)</annotation></semantics></math>,
<math id="I1.i7.p1.m8" class="ltx_Math" alttext="{|\alpha|}^{V[G]}\leq{|\alpha|}^{V}" display="inline"><semantics><mrow><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>≤</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">{|\alpha|}^{V[G]}\leq{|\alpha|}^{V}</annotation></semantics></math>, and
any (regular) cardinal in <math id="I1.i7.p1.m9" class="ltx_Math" alttext="V[G]" display="inline"><semantics><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="application/x-tex">V[G]</annotation></semantics></math> is a (regular) cardinal in <math id="I1.i7.p1.m10" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math>.
Next we have,</p>
</div>
<div id="I1.i7.p2" class="ltx_para">
<table id="S0.Ex4" class="ltx_equationgroup ltx_eqn_table">

<tr id="S0.Ex4X" class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_td ltx_align_right ltx_eqn_cell"><math id="S0.Ex4X.m2" class="ltx_Math" alttext="\displaystyle\exists\alpha\in\mathrm{Ord},\operatorname{cf}^{V[G]}(\alpha)\leq%
\operatorname{cf}^{V}(\alpha)" display="inline"><semantics><mrow><mrow><mrow><mo>∃</mo><mi>α</mi></mrow><mo>∈</mo><mi>Ord</mi></mrow><mo>,</mo><mrow><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\displaystyle\exists\alpha\in\mathrm{Ord},\operatorname{cf}^{V[G]}(\alpha)\leq%
\operatorname{cf}^{V}(\alpha)</annotation></semantics></math></td>
<td class="ltx_td ltx_align_left ltx_eqn_cell"><math id="S0.Ex4X.m3" class="ltx_Math" alttext="\displaystyle\implies\exists\alpha\in\mathrm{Ord},\operatorname{cf}^{V[G]}(%
\operatorname{cf}^{V}(\alpha))\leq\operatorname{cf}^{V[G]}(\alpha)&lt;%
\operatorname{cf}^{V}(\alpha)" display="inline"><semantics><mrow><mrow><mi></mi><mo>⟹</mo><mrow><mo>∃</mo><mi>α</mi></mrow><mo>∈</mo><mi>Ord</mi></mrow><mo>,</mo><mrow><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\displaystyle\implies\exists\alpha\in\mathrm{Ord},\operatorname{cf}^{V[G]}(%
\operatorname{cf}^{V}(\alpha))\leq\operatorname{cf}^{V[G]}(\alpha)&lt;%
\operatorname{cf}^{V}(\alpha)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
<tr id="S0.Ex4Xa" class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_td ltx_eqn_cell"></td>
<td class="ltx_td ltx_align_left ltx_eqn_cell"><math id="S0.Ex4Xa.m2" class="ltx_Math" alttext="\displaystyle\implies\exists\beta\textrm{ regular cardinal in }V,\textrm{ not %
regular cardinal in }V[G]" display="inline"><semantics><mrow><mi></mi><mo>⟹</mo><mrow><mrow><mo>∃</mo><mrow><mi>β</mi><mo>⁢</mo><mtext> regular cardinal in </mtext><mo>⁢</mo><mi>V</mi></mrow></mrow><mo>,</mo><mrow><mtext> not regular cardinal in </mtext><mo>⁢</mo><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\displaystyle\implies\exists\beta\textrm{ regular cardinal in }V,\textrm{ not %
regular cardinal in }V[G]</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
<tr id="S0.Ex4Xb" class="ltx_equation ltx_eqn_row ltx_align_baseline">
<td class="ltx_eqn_cell ltx_eqn_center_padleft"></td>
<td class="ltx_td ltx_eqn_cell"></td>
<td class="ltx_td ltx_align_left ltx_eqn_cell"><math id="S0.Ex4Xb.m2" class="ltx_Math" alttext="\displaystyle\implies\exists\beta\in\mathrm{Ord},\operatorname{cf}^{V[G]}(%
\beta)&lt;\beta=\operatorname{cf}^{V}(\beta)" display="inline"><semantics><mrow><mrow><mi></mi><mo>⟹</mo><mrow><mo>∃</mo><mi>β</mi></mrow><mo>∈</mo><mi>Ord</mi></mrow><mo>,</mo><mrow><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>β</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mi>β</mi><mo>=</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>β</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\displaystyle\implies\exists\beta\in\mathrm{Ord},\operatorname{cf}^{V[G]}(%
\beta)&lt;\beta=\operatorname{cf}^{V}(\beta)</annotation></semantics></math></td>
<td class="ltx_eqn_cell ltx_eqn_center_padright"></td>
</tr>
</table>
</div>
<div id="I1.i7.p3" class="ltx_para">
<p class="ltx_p">that is
<math id="I1.i7.p3.m1" class="ltx_Math" alttext="\forall\alpha\in\mathrm{Ord},\operatorname{cf}^{V[G]}(\alpha)=\operatorname{cf%
}^{V}(\alpha)" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>∈</mo><mi>Ord</mi></mrow><mo>,</mo><mrow><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha\in\mathrm{Ord},\operatorname{cf}^{V[G]}(\alpha)=\operatorname{cf%
}^{V}(\alpha)</annotation></semantics></math> is equivalent
to ‘‘<math id="I1.i7.p3.m2" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math> and <math id="I1.i7.p3.m3" class="ltx_Math" alttext="V[G]" display="inline"><semantics><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="application/x-tex">V[G]</annotation></semantics></math> have the same regular cardinals’’. Similarly,
we can prove that
<math id="I1.i7.p3.m4" class="ltx_Math" alttext="\forall\alpha\in\mathrm{Ord},{|\alpha|}^{V[G]}={|\alpha|}^{V}" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>∈</mo><mi>Ord</mi></mrow><mo>,</mo><mrow><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha\in\mathrm{Ord},{|\alpha|}^{V[G]}={|\alpha|}^{V}</annotation></semantics></math> is equivalent to
‘‘<math id="I1.i7.p3.m5" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math> and <math id="I1.i7.p3.m6" class="ltx_Math" alttext="V[G]" display="inline"><semantics><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="application/x-tex">V[G]</annotation></semantics></math> have the same cardinals’’.</p>
</div>
<div id="I1.i7.p4" class="ltx_para">
<p class="ltx_p">The proof of theorem 14.34 shows that
‘‘<math id="I1.i7.p4.m1" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math> and <math id="I1.i7.p4.m2" class="ltx_Math" alttext="V[G]" display="inline"><semantics><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="application/x-tex">V[G]</annotation></semantics></math> have the same regular cardinals’’ and so
to complete the proof, it is enough to show that
<math id="I1.i7.p4.m3" class="ltx_Math" alttext="\forall\alpha,\operatorname{cf}^{V[G]}(\alpha)=\operatorname{cf}^{V}(\alpha)" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha,\operatorname{cf}^{V[G]}(\alpha)=\operatorname{cf}^{V}(\alpha)</annotation></semantics></math>
implies <math id="I1.i7.p4.m4" class="ltx_Math" alttext="\forall\alpha,{|\alpha|}^{V[G]}={|\alpha|}^{V}" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup></mrow><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">\forall\alpha,{|\alpha|}^{V[G]}={|\alpha|}^{V}</annotation></semantics></math>.
So suppose <math id="I1.i7.p4.m5" class="ltx_Math" alttext="\forall\alpha,\operatorname{cf}^{V[G]}(\alpha)=\operatorname{cf}^{V}(\alpha)" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><mo>=</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\forall\alpha,\operatorname{cf}^{V[G]}(\alpha)=\operatorname{cf}^{V}(\alpha)</annotation></semantics></math>
and assume that there is <math id="I1.i7.p4.m6" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> such that
<math id="I1.i7.p4.m7" class="ltx_Math" alttext="{|\alpha|}^{V[G]}&lt;{|\alpha|}^{V}" display="inline"><semantics><mrow><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>&lt;</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">{|\alpha|}^{V[G]}&lt;{|\alpha|}^{V}</annotation></semantics></math>. Consider the least such <math id="I1.i7.p4.m8" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>.
If <math id="I1.i7.p4.m9" class="ltx_Math" alttext="\beta={|\alpha|}^{V}" display="inline"><semantics><mrow><mi>β</mi><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">\beta={|\alpha|}^{V}</annotation></semantics></math>
then <math id="I1.i7.p4.m10" class="ltx_Math" alttext="\beta\leq\alpha" display="inline"><semantics><mrow><mi>β</mi><mo>≤</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beta\leq\alpha</annotation></semantics></math> so
<math id="I1.i7.p4.m11" class="ltx_Math" alttext="{|\beta|}^{V[G]}\leq{|\alpha|}^{V[G]}&lt;{|\alpha|}^{V}=\beta" display="inline"><semantics><mrow><msup><mrow><mo stretchy="false">|</mo><mi>β</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>≤</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>&lt;</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup><mo>=</mo><mi>β</mi></mrow><annotation encoding="application/x-tex">{|\beta|}^{V[G]}\leq{|\alpha|}^{V[G]}&lt;{|\alpha|}^{V}=\beta</annotation></semantics></math>.
By minimality of <math id="I1.i7.p4.m12" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>, <math id="I1.i7.p4.m13" class="ltx_Math" alttext="\beta=\alpha" display="inline"><semantics><mrow><mi>β</mi><mo>=</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\beta=\alpha</annotation></semantics></math> and so
<math id="I1.i7.p4.m14" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is a cardinal in <math id="I1.i7.p4.m15" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math>. <math id="I1.i7.p4.m16" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math> is actually regular in <math id="I1.i7.p4.m17" class="ltx_Math" alttext="V" display="inline"><semantics><mi>V</mi><annotation encoding="application/x-tex">V</annotation></semantics></math>.
Otherwise, suppose <math id="I1.i7.p4.m18" class="ltx_Math" alttext="\operatorname{cf}^{V}(\alpha)&lt;\alpha" display="inline"><semantics><mrow><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="application/x-tex">\operatorname{cf}^{V}(\alpha)&lt;\alpha</annotation></semantics></math> and
let <math id="I1.i7.p4.m19" class="ltx_Math" alttext="\alpha=\bigcup_{\beta&lt;\operatorname{cf}^{V}(\alpha)}X_{\beta}" display="inline"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msub><mo largeop="true" mathsize="160%" stretchy="false" symmetric="true">⋃</mo><mrow><mi>β</mi><mo>&lt;</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></msub><msub><mi>X</mi><mi>β</mi></msub></mrow></mrow><annotation encoding="application/x-tex">\alpha=\bigcup_{\beta&lt;\operatorname{cf}^{V}(\alpha)}X_{\beta}</annotation></semantics></math>
such that <math id="I1.i7.p4.m20" class="ltx_Math" alttext="{|X_{\beta}|}^{V}&lt;{|\alpha|}^{V}" display="inline"><semantics><mrow><msup><mrow><mo stretchy="false">|</mo><msub><mi>X</mi><mi>β</mi></msub><mo stretchy="false">|</mo></mrow><mi>V</mi></msup><mo>&lt;</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">{|X_{\beta}|}^{V}&lt;{|\alpha|}^{V}</annotation></semantics></math>. By minimality of <math id="I1.i7.p4.m21" class="ltx_Math" alttext="\alpha" display="inline"><semantics><mi>α</mi><annotation encoding="application/x-tex">\alpha</annotation></semantics></math>,
we have <math id="I1.i7.p4.m22" class="ltx_Math" alttext="{|\operatorname{cf}^{V}(\alpha)|}^{V[G]}={|\operatorname{cf}^{V}(\alpha)|}^{V}" display="inline"><semantics><mrow><msup><mrow><mo stretchy="false">|</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">{|\operatorname{cf}^{V}(\alpha)|}^{V[G]}={|\operatorname{cf}^{V}(\alpha)|}^{V}</annotation></semantics></math> and
<math id="I1.i7.p4.m23" class="ltx_Math" alttext="{|X_{\beta}|}^{V[G]}={|X_{\beta}|}^{V}" display="inline"><semantics><mrow><msup><mrow><mo stretchy="false">|</mo><msub><mi>X</mi><mi>β</mi></msub><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><msub><mi>X</mi><mi>β</mi></msub><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">{|X_{\beta}|}^{V[G]}={|X_{\beta}|}^{V}</annotation></semantics></math>. Then
<math id="I1.i7.p4.m24" class="ltx_Math" alttext="{|\alpha|}^{V[G]}={|\operatorname{cf}^{V}(\alpha)|}^{V[G]}\sup_{\beta&lt;%
\operatorname{cf}^{V}(\alpha)}{|X_{\beta}|}^{V[G]}={|\operatorname{cf}^{V}(%
\alpha)|}^{V}\sup_{\beta&lt;\operatorname{cf}^{V}(\alpha)}{|X_{\beta}|}^{V}={|%
\alpha|}^{V}" display="inline"><semantics><mrow><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>=</mo><mrow><msup><mrow><mo stretchy="false">|</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁢</mo><mrow><msub><mo>sup</mo><mrow><mi>β</mi><mo>&lt;</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></msub><mo>⁡</mo><msup><mrow><mo stretchy="false">|</mo><msub><mi>X</mi><mi>β</mi></msub><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup></mrow></mrow><mo>=</mo><mrow><msup><mrow><mo stretchy="false">|</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo stretchy="false">|</mo></mrow><mi>V</mi></msup><mo>⁢</mo><mrow><msub><mo>sup</mo><mrow><mi>β</mi><mo>&lt;</mo><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow></msub><mo>⁡</mo><msup><mrow><mo stretchy="false">|</mo><msub><mi>X</mi><mi>β</mi></msub><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow></mrow><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">{|\alpha|}^{V[G]}={|\operatorname{cf}^{V}(\alpha)|}^{V[G]}\sup_{\beta&lt;%
\operatorname{cf}^{V}(\alpha)}{|X_{\beta}|}^{V[G]}={|\operatorname{cf}^{V}(%
\alpha)|}^{V}\sup_{\beta&lt;\operatorname{cf}^{V}(\alpha)}{|X_{\beta}|}^{V}={|%
\alpha|}^{V}</annotation></semantics></math>, a contradiction. Finally, we get
<math id="I1.i7.p4.m25" class="ltx_Math" alttext="\operatorname{cf}^{V}(\alpha)=\alpha={|\alpha|}^{V}&gt;{|\alpha|}^{V[G]}\geq%
\operatorname{cf}^{V[G]}(\alpha)" display="inline"><semantics><mrow><mrow><msup><mo>cf</mo><mi>V</mi></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mi>α</mi><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup><mo>&gt;</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>≥</mo><mrow><msup><mo>cf</mo><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup><mo>⁡</mo><mrow><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="application/x-tex">\operatorname{cf}^{V}(\alpha)=\alpha={|\alpha|}^{V}&gt;{|\alpha|}^{V[G]}\geq%
\operatorname{cf}^{V[G]}(\alpha)</annotation></semantics></math>. This is again a contradiction and so
<math id="I1.i7.p4.m26" class="ltx_Math" alttext="\forall\alpha,{|\alpha|}^{V[G]}={|\alpha|}^{V}" display="inline"><semantics><mrow><mrow><mrow><mo>∀</mo><mi>α</mi></mrow><mo>,</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mrow><mi>V</mi><mo>⁢</mo><mrow><mo stretchy="false">[</mo><mi>G</mi><mo stretchy="false">]</mo></mrow></mrow></msup></mrow><mo>=</mo><msup><mrow><mo stretchy="false">|</mo><mi>α</mi><mo stretchy="false">|</mo></mrow><mi>V</mi></msup></mrow><annotation encoding="application/x-tex">\forall\alpha,{|\alpha|}^{V[G]}={|\alpha|}^{V}</annotation></semantics></math>.</p>
</div>
</li>
</ol>
</div>


{% endraw %}
