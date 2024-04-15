---
layout: post
title: "Thoughts on the Dihedral Hidden Subgroup Problem (part 3)"
tags: maths cs
---

{% raw %}

  <p>Back to the DHSP again (see <a href="?post/2010/06/16/Thoughts-on-the-Dihedral-Hidden-Subgroup-Problem">part 1</a> and <a href="?post/2010/06/20/Thoughts-on-the-Dihedral-Hidden-Subgroup-Problem-%28part-2%29">part 2</a> in previous blog posts)... This time, I've tried to approximate the value of <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>d</mi> </math> rather than finding its parity. For convenience, we assume <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>N</mi> </math> to be even and define <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>N</mi> <mo>'</mo> <mo>=</mo> <mn>2</mn> <mi>M</mi> <mo>=</mo> <mfrac> <mi>N</mi> <mn>2</mn> </mfrac> </math>. We consider for <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mi>a</mi> <mo>∈</mo> <msub> <mi>ℤ</mi> <mi>N</mi> </msub> </mrow> </math> and <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mi>b</mi> <mo>∈</mo> <msub> <mi>ℤ</mi> <mn>2</mn> </msub> </mrow> </math> the sets of <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>N</mi> <mo>'</mo> </math> successive values<math display="block" xmlns="http://www.w3.org/1998/Math/MathML"> <msubsup> <mi>F</mi> <mi>a</mi> <mi>b</mi> </msubsup> <mo>=</mo> <mo stretchy="false">{</mo> <mrow> <mi>f</mi> <mrow> <mo>(</mo> <mrow> <mi>a</mi> <mo>+</mo> <mi>i</mi> </mrow> <mo>,</mo> <mi>b</mi> <mo>)</mo> </mrow> </mrow> <mo>,</mo> <mi>i</mi> <mo>∈</mo> <msub> <mi>ℤ</mi> <mrow> <mi>N</mi> <mo>′</mo> </mrow> </msub> <mo stretchy="false">}</mo> </math></p>

<p>We suppose that we can efficiently create uniform superposition over these states. As in <a href="?post/2010/06/20/Thoughts-on-the-Dihedral-Hidden-Subgroup-Problem-%28part-2%29">part 2</a>, we have <math xmlns="http://www.w3.org/1998/Math/MathML"> <msubsup> <mi>F</mi> <mi>a</mi> <mn>1</mn> </msubsup> <mo>=</mo> <msubsup> <mi>F</mi> <mrow> <mi>a</mi> <mo>−</mo> <mi>d</mi> </mrow> <mn>0</mn> </msubsup> <mo>=</mo> <msubsup> <mi>F</mi> <mi>s</mi> <mn>0</mn> </msubsup> </math> with <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mo>−</mo> <mi>N</mi> </mrow> <mo>&lt;</mo> <mi>s</mi> <mo>&lt;</mo> <mi>N</mi> </math> and we measure the tensor product of the uniform superpositions over <math xmlns="http://www.w3.org/1998/Math/MathML"> <msubsup> <mi>F</mi> <mi>a</mi> <mn>1</mn> </msubsup> <mo>=</mo> <msubsup> <mi>F</mi> <mi>s</mi> <mn>0</mn> </msubsup> </math> and <math xmlns="http://www.w3.org/1998/Math/MathML"> <msubsup> <mi>F</mi> <mn>0</mn> <mn>0</mn> </msubsup> </math> in the basis <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"> <msub> <mrow> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> </mrow> <mrow> <mi>x</mi> <mo>∈</mo> <msub> <mi>ℤ</mi> <mi>N</mi> </msub> </mrow> </msub> </math>, <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"> <msub> <mrow> <mfrac> <mn>1</mn> <msqrt> <mn>2</mn> </msqrt> </mfrac> <mrow> <mo>(</mo> <mrow> <mrow> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mi>y</mi> <mo stretchy="false">⟩</mo> </mrow> <mo>+</mo> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mi>y</mi> <mo stretchy="false">⟩</mo> </mrow> </mrow> </mrow> <mo>)</mo> </mrow> </mrow> <mrow> <mi>x</mi> <mi>&lt;</mi> <mi>y</mi> <mo>∈</mo> <msub> <mi>ℤ</mi> <mi>N</mi> </msub> </mrow> </msub> </math>, <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"> <msub> <mrow> <mfrac> <mn>1</mn> <msqrt> <mn>2</mn> </msqrt> </mfrac> <mrow> <mo>(</mo> <mrow> <mrow> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mi>y</mi> <mo stretchy="false">⟩</mo> </mrow> <mo>−</mo> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mi>y</mi> <mo stretchy="false">⟩</mo> </mrow> </mrow> </mrow> <mo>)</mo> </mrow> </mrow> <mrow> <mi>x</mi> <mi>&lt;</mi> <mi>y</mi> <mo>∈</mo> <msub> <mi>ℤ</mi> <mi>N</mi> </msub> </mrow> </msub> </math>. We define <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>l</mi> <mo>=</mo> <mrow> <mo>∣</mo> <mrow> <msubsup> <mi>F</mi> <mn>0</mn> <mn>0</mn> </msubsup> <mo>∩</mo> <msubsup> <mi>F</mi> <mi>a</mi> <mn>1</mn> </msubsup> <mo>∣</mo> </mrow> </mrow> </math> the number of common elements.</p>

<div><svg height="204" width="411" xmlns="http://www.w3.org/2000/svg"> <defs> <marker id="Arrow1Mstart_" orient="auto" refx="0.0" refy="0.0" style="overflow:visible;fill:inherit;stroke:inherit"> <path d="M 0.0,0.0 L 5.0,-5.0 L -12.5,0.0 L 5.0,5.0 L 0.0,0.0 z " style="fill-rule:evenodd;stroke-width:1.0pt;marker-start:none" transform="scale(0.4) translate(10,0)"></path> </marker> <marker id="Arrow1Mend_" orient="auto" refx="0.0" refy="0.0" style="overflow:visible;fill:inherit;stroke:inherit"> <path d="M 0.0,0.0 L 5.0,-5.0 L -12.5,0.0 L 5.0,5.0 L 0.0,0.0 z " style="fill-rule:evenodd;stroke-width:1.0pt;marker-start:none;" transform="scale(0.4) rotate(180) translate(10,0)"></path> </marker> </defs> <g transform="translate(-22,-30) "> <g transform="translate(24,34) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>f</mi> <mrow> <mo>(</mo> <mn>0</mn> <mo>,</mo> <mn>0</mn> <mo>)</mo> </mrow> </math></foreignobject> <text>f(0,0)</text> </switch> </g> <g transform="translate(177,34) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>f</mi> <mrow> <mo>(</mo> <mrow> <mi>N</mi> <mo>'</mo> </mrow> <mo>,</mo> <mn>0</mn> <mo>)</mo> </mrow> </math></foreignobject> <text>f(0,0)</text> </switch> </g> <g transform="translate(341,34) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>f</mi> <mrow> <mo>(</mo> <mi>N</mi> <mo>−</mo> <mn>1</mn> <mo>,</mo> <mn>0</mn> <mo>)</mo> </mrow> </math></foreignobject> <text>f(0,0)</text> </switch> </g> <g> <line style="stroke: black; stroke-opacity: 1; stroke-width: 1; " transform="translate(0,1.5) " x1="36" x2="369" y1="70" y2="70"></line> <line style="stroke: black; stroke-opacity: 1; stroke-width: 1; " transform="translate(-15) " x1="217" x2="217" y1="58" y2="84"></line> </g> <g> <path d="M 32,94 C 38,116 25,109 80,104 C 135,99 117,129 120,129 C 123,129 113,106 138,103 C 163,100 204,112 198,91 " style="stroke: black; stroke-opacity: 1; stroke-width: 1; fill:none" transform="translate(3,-1) "></path> <g transform="translate(113,125) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <msubsup> <mi>F</mi> <mn>0</mn> <mn>0</mn> </msubsup> </math></foreignobject> <text>F_0^0</text> </switch> </g> </g> <g transform="translate(119,1) "> <path d="M 32,94 C 38,116 25,109 80,104 C 135,99 117,129 120,129 C 123,129 113,106 138,103 C 163,100 204,112 198,91 " style="stroke: black; stroke-opacity: 1; stroke-width: 1; fill:none" transform="translate(3,-1) "></path> <g transform="translate(113,125) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <msubsup> <mi>F</mi> <mi>s</mi> <mn>0</mn> </msubsup> </math></foreignobject> <text>F_s^0</text> </switch> </g> </g> <g> <g transform="translate(84.5,169) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>s</mi> </math></foreignobject> <text>s</text> </switch> </g> <line marker-end="url(#Arrow1Mend_)" style="stroke: black; stroke-opacity: 1; stroke-width: 1; fill:none" transform="translate(-4,108) " x1="36" x2="151" y1="62" y2="62"></line> </g> <g> <g transform="translate(171.5,171) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>l</mi> </math></foreignobject> <text>l</text> </switch> </g> <line marker-end="url(#Arrow1Mend_)" marker-start="url(#Arrow1Mstart_)" style="stroke: black; stroke-opacity: 1; stroke-width: 1; fill:none" transform="translate(1) " x1="150" x2="198" y1="170" y2="170"></line> </g> <g> <g transform="translate(109.5,208) "> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>N</mi> <mo>'</mo> </math></foreignobject> <text>N'</text> </switch> </g> <line marker-end="url(#Arrow1Mend_)" marker-start="url(#Arrow1Mstart_)" style="stroke: black; stroke-opacity: 1; stroke-width: 1; fill:none" x1="30" x2="200" y1="206" y2="206"></line> </g> <g transform="translate(300,155)"> <switch> <foreignobject height="50px" requiredextensions="http://www.w3.org/1998/Math/MathML" width="100px"> <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mn>0</mn> <mo>≤</mo> <mi>s</mi> <mo>≤</mo> <mrow> <mi>N</mi> <mo>'</mo> </mrow> </mrow> </math></foreignobject> <text>0 ≤ s ≤ N'</text> </switch> </g> </g> </svg></div>

<p>The figure above shows that in the case <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mn>0</mn> <mo>≤</mo> <mi>s</mi> <mo>≤</mo> <mrow> <mi>N</mi> <mo>'</mo> </mrow> </mrow> </math>, we have <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>l</mi> <mo>=</mo> <mi>N</mi> <mo>'</mo> <mo>−</mo> <mi>s</mi> </math>. In general, the expression is</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"> <mi>l</mi> <mo>=</mo> <mrow> <mo>∣</mo> <mi>N</mi> <mo>'</mo> <mo>−</mo> <mrow> <mo>∣</mo> <mi>s</mi> <mo>∣</mo> </mrow> <mo>∣</mo> </mrow> <mo>=</mo> <mrow> <mo>∣</mo> <mi>N</mi> <mo>'</mo> <mo>−</mo> <mrow> <mo>∣</mo> <mi>d</mi> <mo>−</mo> <mi>a</mi> <mo>∣</mo> </mrow> <mo>∣</mo> </mrow> </math></p>

<p>Using an analysis similar to the one <a href="?post/2010/06/20/Thoughts-on-the-Dihedral-Hidden-Subgroup-Problem-%28part-2%29">part 2</a>, we get the probability to measure an element in <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"> <msub> <mrow> <mfrac> <mn>1</mn> <msqrt> <mn>2</mn> </msqrt> </mfrac> <mrow> <mo>(</mo> <mrow> <mrow> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mi>y</mi> <mo stretchy="false">⟩</mo> </mrow> <mo>−</mo> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mi>y</mi> <mo stretchy="false">⟩</mo> </mrow> </mrow> </mrow> <mo>)</mo> </mrow> </mrow> <mrow> <mi>x</mi> <mi>&lt;</mi> <mi>y</mi> <mo>∈</mo> <msub> <mi>ℤ</mi> <mi>N</mi> </msub> </mrow> </msub> </math>:</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"> <mi>P</mi> <mo>=</mo> <mfrac> <mn>1</mn> <mn>2</mn> </mfrac> <mrow> <mo>[</mo> <mn>1</mn> <mo>−</mo> <msup> <mrow> <mo>(</mo> <mfrac> <mi>l</mi> <mrow> <mi>N</mi> <mo>′</mo> </mrow> </mfrac> <mo>)</mo> </mrow> <mn>2</mn> </msup> <mo>]</mo> </mrow> </math></p>

<p>Repeating the measurements, we can approximate <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>P</mi> </math>, and consequently <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>l</mi> <mo>,</mo> <mi>s</mi> </math> and finally <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>d</mi> </math>. We can also play with the value <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>a</mi> </math>, to improve the approximation. Unfortunately, using a number of repetitions polynomial in <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>log</mi> <mi>N</mi> </math>, it does not seem possible to bound the error better than <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mi>O</mi> <mrow> <mo>(</mo> <mi>N</mi> <mo>)</mo> </mrow> </mrow> </math>. It seems however that it is still a better result than the one that I obtained with the standard Coset Sampling method. Hence it is another hint of the fact that using a superposition over several oracles values would yield improvement.</p>

<p>I'm still wondering how to create efficiently an uniform superposition over several oracle values. One thing I've read in many papers, is given a superposition over elements <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mo stretchy="false">∣</mo> <mi>x</mi> <mo stretchy="false">⟩</mo> </mrow> <mrow> <mo stretchy="false">∣</mo> <mrow> <mi>f</mi> <mo stretchy="false">(</mo> <mi>x</mi> <mo stretchy="false">)</mo> </mrow> <mo stretchy="false">⟩</mo> </mrow> </math>, <em>erase</em> or <em>uncompute</em> the first register to get a superposition over elements <math xmlns="http://www.w3.org/1998/Math/MathML"> <mrow> <mo stretchy="false">∣</mo> <mrow> <mi>f</mi> <mo stretchy="false">(</mo> <mi>x</mi> <mo stretchy="false">)</mo> </mrow> <mo stretchy="false">⟩</mo> </mrow> </math>. However, I'm not sure what are the requirements to apply such an operation. If it could work for the algorithm of <a href="?post/2010/06/20/Thoughts-on-the-Dihedral-Hidden-Subgroup-Problem-%28part-2%29">part 2</a>, then this would solve the case <math xmlns="http://www.w3.org/1998/Math/MathML"> <mi>N</mi> <mo>=</mo> <msup> <mn>2</mn> <mi>n</mi> </msup> </math>.</p>

{% endraw %}