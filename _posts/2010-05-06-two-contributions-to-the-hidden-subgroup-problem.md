---
layout: post
title: "Two contributions to the Hidden Subgroup Problem"
tags: maths cs
---

{% raw %}

<p>Today, I have finished the preliminary version of my report on the <a href="http://en.wikipedia.org/wiki/Hidden_subgroup_problem">Hidden Subgroup Problem</a> (HSP). For those who have never heard about it before, we are given a finite group <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>G</mi> </math>, a subgroup <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>H</mi> </math> and a function <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>f</mi> <mo>:</mo> <mrow> <mi>G</mi> <mo>→</mo> <mi>S</mi> </mrow> </math>. This function is constant on each (left) coset of <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>H</mi> </math> but takes different values on distinct cosets. Said otherwise we have:</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"> <mo>∀</mo> <msub> <mi>g</mi> <mn>1</mn> </msub> <mo>,</mo> <msub> <mi>g</mi> <mn>2</mn> </msub> <mo>∈</mo> <mi>G</mi> <mo>,</mo> <mi>f</mi> <mo stretchy="false">(</mo> <msub> <mi>g</mi> <mn>1</mn> </msub> <mo stretchy="false">)</mo> <mo>=</mo> <mi>f</mi> <mo stretchy="false">(</mo> <msub> <mi>g</mi> <mn>2</mn> </msub> <mo stretchy="false">)</mo> <mo>⇔</mo> <msub> <mi>g</mi> <mn>1</mn> </msub> <mi>H</mi> <mo>=</mo> <msub> <mi>g</mi> <mn>2</mn> </msub> <mi>H</mi> </math>The purpose is to identify the "hidden" subgroup <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>H</mi> </math> (for instance we can return a generating set) with a complexity polynomial in <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mi>log</mi> <mrow> <mo>∣</mo> <mi>G</mi> <mo>∣</mo> </mrow> </mrow> </math>. Although it may seem really abstract, this problem allows to describe various quantum algorithms exponentially faster than their known classical versions. This includes the famous <a href="http://en.wikipedia.org/wiki/Shor%27s_algorithm">Shor's algorithm</a> for integer factorization, which can break the ubiquitous RSA cryptosystem. Shor's algorithm uses a solution to HSP over a cyclic group but we have quantum algorithms for the larger class of <a href="http://en.wikipedia.org/wiki/Hamiltonian_group">dedekindian groups</a> as well as miscellaneous other groups. Unfortunately, these algorithms are not enough to solve HSP over the <a href="http://en.wikipedia.org/wiki/Dihedral_group">dihedral group</a> or the <a href="http://en.wikipedia.org/wiki/Symmetric_group">symmetric group</a>. These two cases are particularly interesting since the former could solve a <a href="http://en.wikipedia.org/wiki/Lattice_problem">lattice problem</a> used in cryptography to establish security proofs while a solution to the latter provides an efficient algorithm for the <a href="http://en.wikipedia.org/wiki/Graph_isomorphism_problem">graph isomorphism problem</a>.</p>

<p>For the moment, I have essentially reviewed the major results on dedekindian, dihedral and symmetric groups. Even if there is not many new things for researchers working on that topic, I hope it could serve as an introduction to the subject and be a useful review of the state-of-the-art. In particular, I plan to complete the <a href="http://www.cs.au.dk/~fwang/speciale/web/appendix_A.xhtml#appendix_A">Table of Hidden Subgroup Problems</a> which gives a good overview. There are at least two contributions I brought to the topic that I would like to discuss briefly in this blog post.</p>

<p>First, <a href="http://www.cs.au.dk/~fwang/speciale/web/dihedral_and_symmetric.xhtml#id5.3.">I have studied how Regev's algorithm works</a>. As stated in his paper, we have a solution to the <math xmlns="http://www.w3.org/1998/Math/MathML"> <mtext>poly</mtext> <mrow> <mo>(</mo> <mi>log</mi> <mi>N</mi> <mo>)</mo> </mrow> </math>-uniqueSVP if we can find a hidden subgroup <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>H</mi> <mo>=</mo> <mrow> <mo>⟨</mo> <mrow> <mo>(</mo> <mi>d</mi> <mo>,</mo> <mn>1</mn> <mo>)</mo> </mrow> <mo>⟩</mo> </mrow> </math> in the dihedral group <math xmlns="http://www.w3.org/1998/Math/MathML"> <msub> <mi>D</mi> <mi>N</mi> </msub> </math> using <em>coset sampling on the whole group</em>. This point is often overlooked in several papers, where the reader could understand that an arbitrary solution to the dihedral HSP works. Fortunately, Regev's algorithm is sufficiently close to the coset sampling procedure so that we can modify it to include some kinds of <em>recursive</em> algorithm. With such a modification, a solution like Kuperberg's algorithm (where we apply coset sampling on subgroups of <math xmlns="http://www.w3.org/1998/Math/MathML"> <msub> <mi>D</mi> <mi>N</mi> </msub> </math>) becomes acceptable. Actually, we can also modify the algorithm to work with the <a href="http://en.wikipedia.org/wiki/Dihedral_group#Generalized_dihedral_group">generalized dihedral group</a>. Another remark is about the degree of the approximation given by Regev's algorithm: I have shown that we have a solution to the <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>Θ</mi> <mrow> <mo>(</mo> <msup> <mi>n</mi> <mrow> <mfrac> <mn>1</mn> <mn>2</mn> </mfrac> <mo>+</mo> <mn>2</mn> <mi>D</mi> </mrow> </msup> <mo>)</mo> </mrow> </math>-uniqueSVP if the query complexity of the HSP algorithm used is <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mi>O</mi> <mrow> <mo>(</mo> <msup> <mrow> <mo>(</mo> <mrow> <mi>log</mi> <mi>N</mi> </mrow> <mo>)</mo> </mrow> <mi>D</mi> </msup> <mo>)</mo> </mrow> </mrow> </math>, thus providing a more accurate statement.</p>

<p>Recently, I have considered a <a href="http://www.cs.au.dk/~fwang/speciale/web/appendix_G.xhtml#appendix_G">general approach to the HSP</a> using the classical description of finite group via <a href="http://en.wikipedia.org/wiki/Composition_series#For_groups">composition series</a> and <a href="http://en.wikipedia.org/wiki/List_of_finite_simple_groups">simple groups</a>. The idea is that if <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>N</mi> </math> is a non-trivial normal subgroup of <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>G</mi> </math> we can split the problems on two HSPs over <math xmlns="http://www.w3.org/1998/Math/MathML"> <mfrac bevelled="true"> <mi>G</mi> <mi>N</mi> </mfrac> </math> and <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>N</mi> </math>. We can repeat the procedure until we reach simple groups. Because the length of a composition series is polynomial in <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mi>log</mi> <mrow> <mo>∣</mo> <mi>G</mi> <mo>∣</mo> </mrow> </mrow> </math>, we get a solution to the general HSP under two conditions: we have algorithms for HSP over simple groups and we can build efficient oracles on the "reduced" groups. I've succeeded to find an alternative algorithm for the abelian case based on that framework but for the dihedral/symmetric, it seems that the two previous assumptions are exactly what we are stuck on. However, it could still be useful to solve HSP over other groups.</p>

<p>Now, my priority is to review the results we have for some semidirect products but I hope to have time to study various open issues such that HSP over simple groups, HSP-based algorithms etc</p>


{% endraw %}