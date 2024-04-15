---
layout: post
title: "S[α] for strings of ordinals"
tags: maths
---

{% raw %}

  <p><strong>Update 2020/03/10: Added complexity analysis for S.substr(α, N)</strong></p>

<p>In a <a href="https://frederic-wang.fr/ordinal-as-strings-of-emptyset-commas-and-braces.html">previous blog post</a>, I defined for each ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> a string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math> (made of the characters for the empty set, comma, opening brace and closing brace) that enumerates the element of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>. I gave a simple formulas to calculate the length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mi>α</mi></msub><annotation encoding="TeX">L_\alpha</annotation></semantics></math> of this string.</p>

<p>My colleague <a href="https://www.igalia.com/igalian/idimitriou">Ioanna</a> was a bit disappointed that I didn’t provide a script for calculating the infinite <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math> strings. Obviously, the complexity would be “<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi mathvariant="normal">Ω</mi><mo stretchy="false">(</mo><mi>ω</mi><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">\Omega(\omega)</annotation></semantics></math>” but it is still possible to evaluate the string at a given position: Given <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>&lt;</mo><msub><mi>L</mi><mi>α</mi></msub></mrow><annotation encoding="TeX">\beta &lt; L_\alpha</annotation></semantics></math>, what is the character of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math> at position <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>β</mi><annotation encoding="TeX">\beta</annotation></semantics></math>?</p>

<p>Since the initial segments of the strings are compatible, another way to express this is by introducing the class <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo>=</mo><munder><mo>⋃</mo><mrow><mi>α</mi><mo>∊</mo><mrow><mi mathvariant="normal">O</mi><mi mathvariant="normal">r</mi><mi mathvariant="normal">d</mi></mrow></mrow></munder><msub><mi>S</mi><mi>α</mi></msub></mrow><annotation encoding="TeX">S = \bigcup_{\alpha \in {\mathrm{Ord}}} S_\alpha</annotation></semantics></math> corresponding to a giant string enumerating the class <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi mathvariant="normal">O</mi><mi mathvariant="normal">r</mi><mi mathvariant="normal">d</mi></mrow><annotation encoding="TeX">\mathrm{Ord}</annotation></semantics></math> of all ordinals. Given an ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>, what is <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math>?</p>

<p>A small generalization of this S.charAt(α) operation is S.substr(α, N) calculating the substring of length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>N</mi><annotation encoding="TeX">N</annotation></semantics></math> starting at <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>.</p>

<h2 id="example">Example</h2>

<ul>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>2</mn></msub><annotation encoding="TeX">S_{2}</annotation></semantics></math> is "∅,{∅}", so
<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mn>0</mn><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[0]</annotation></semantics></math> is the character ∅, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mn>1</mn><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[1]</annotation></semantics></math> is a comma,
<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mn>2</mn><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[2]</annotation></semantics></math> is an opening brace and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mn>4</mn><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[4]</annotation></semantics></math> is a closing brace.
</li>
<li>
 <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>ω</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{\omega+1}</annotation></semantics></math> is made of
 of an <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ω</mi><annotation encoding="TeX">\omega</annotation></semantics></math>-concatenation of finite strings
 (the character ∅, a comma,
 <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>1</mn></msub><annotation encoding="TeX">S_1</annotation></semantics></math> surrounded by braces, a comma,
 <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>2</mn></msub><annotation encoding="TeX">S_2</annotation></semantics></math> surrounded by braces, a comma,
 <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>4</mn></msub><annotation encoding="TeX">S_4</annotation></semantics></math> surrounded by braces, a comma, etc), followed
 by a comma, an opening brace, the same
 <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ω</mi><annotation encoding="TeX">\omega</annotation></semantics></math>-concatenation of finite strings and finally
 a closing brace.
 So <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>ω</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\omega]</annotation></semantics></math> is a comma,
 <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>ω</mi><mo>+</mo><mn>1</mn><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\omega+1]</annotation></semantics></math> is an opening brace,
 <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>ω</mi><mo>+</mo><mn>2</mn><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\omega+2]</annotation></semantics></math> is the character "∅"
 and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>ω</mi><mn>2</mn><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\omega2]</annotation></semantics></math> is a closing brace.
</li>
</ul>

<p>In the previous example, we have basically analyzed the string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{\alpha+1}</annotation></semantics></math> at a given successor ordinal, splitting it into two copies of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math>, comma and braces. This suggests some easy values of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math>:</p>

<h2 id="lemma">Lemma</h2>

<p>For any <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">n &lt; \omega</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta \geq 1</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> is:</p>
<ul>
<li>A comma if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> can be written <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>n</mi></msup><mo>−</mo><mn>3</mn></mrow><annotation encoding="TeX">2^n - 3</annotation></semantics></math> or <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi></mrow><annotation encoding="TeX">\omega^\beta 2^n + n</annotation></semantics></math></li>
<li>An opening brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> can be written <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>n</mi></msup><mo>−</mo><mn>2</mn></mrow><annotation encoding="TeX">2^n - 2</annotation></semantics></math> or <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">\omega^\beta 2^n + n + 1</annotation></semantics></math></li>
<li>A closing brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> can be written <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>4</mn></mrow><annotation encoding="TeX">2^{n+1} - 4</annotation></semantics></math> or <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>+</mo><mi>n</mi></mrow><annotation encoding="TeX">\omega^\beta 2^{n+1} + n</annotation></semantics></math></li>
</ul>

<p>Proof: For any ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>, by viewing the string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{\alpha+1}</annotation></semantics></math>
as a concatenation of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math>, a comma, an opening fence, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math> and
a closing fence, we deduce that:</p>

<ul>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo>[</mo><msub><mi>L</mi><mi>α</mi></msub><mo>]</mo></mrow></mrow><annotation encoding="TeX">{S\left[L_{\alpha}\right]}</annotation></semantics></math> is a comma.</li>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo>[</mo><mrow><msub><mi>L</mi><mi>α</mi></msub><mo>+</mo><mn>1</mn></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">{S\left[L_{\alpha} + 1 \right]}</annotation></semantics></math> is an opening brace.</li>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">L_{\alpha+1}</annotation></semantics></math> is a successor ordinal and
    <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo>[</mo><mrow><msub><mi>L</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>−</mo><mn>1</mn></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">{S\left[L_{\alpha+1} - 1 \right]}</annotation></semantics></math> is a closing brace.</li>
</ul>

<p>The lemma follows immediately from the calculation of string lengths performed in the previous blog post. □</p>

<div style="border: 1px dashed black; padding: .5em; margin: 1em">
Warning: The rest of the blog post gives the solution to this puzzle, so you
might want to have fun solving it yourself first and then go back checking
my proposed solution later 😉...
</div>

<p>More generally, the proof of the lemma can be extended by saying that if we find <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>n</mi><annotation encoding="TeX">n</annotation></semantics></math> such that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><msup><mn>2</mn><mi>n</mi></msup><mo>−</mo><mn>1</mn></mrow><mo>≤</mo><mi>α</mi><mo>≤</mo><mrow><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>5</mn></mrow></mrow><annotation encoding="TeX">{2^n - 1} \leq \alpha \leq {2^{n+1} - 5}</annotation></semantics></math> then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>δ</mi><mo>=</mo><mrow><mi>α</mi><mo>−</mo><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>n</mi></msup><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><msup><mn>2</mn><mi>n</mi></msup><mo>−</mo><mn>4</mn></mrow></mrow><annotation encoding="TeX">\delta = {\alpha - {(2^n - 1)}} \leq {2^n - 4}</annotation></semantics></math> is the index of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">{S[\alpha]}</annotation></semantics></math> in the second substring <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math> of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{\alpha+1}</annotation></semantics></math> and so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>δ</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="TeX">{S[\alpha]} = {S[\delta]}</annotation></semantics></math>.</p>

<p>Details will be provided in the theorem below but one can already write a simple JavaScript recursive program to evalute <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math> at finite ordinals:</p>

<h2 id="script-for-αltωalpha-lt-omega">Script for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">\alpha &lt; \omega</annotation></semantics></math></h2>

<div id="javascript_character_at_finite_alpha" style="border: 1px dashed black; padding: .5em; margin: 1em">
The character of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math> at position <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo></mrow><annotation encoding="TeX">\alpha = </annotation></semantics></math><br />
<input id="alpha_input" size="72" type="text" onchange="calculateCharacterAtIndex()" value="123456789" /><br />
is <input id="s_alpha_output" type="text" value="BigInt not supported" />
<script>
  function charAtIndex(alpha) {
    if (alpha == BigInt(0))
       return "∅";
    // Not sure whether there is an efficient native BigInt operation, so just
    // serialize in binary and count the digits.
    var m = BigInt(2) ** BigInt((alpha + BigInt(3)).toString(2).length - 1);

    if (alpha == m - BigInt(3))
       return ",";
    if (alpha == m - BigInt(2))
       return "{";
    if (alpha == BigInt(2) * m  - BigInt(4))
       return "}";
    var d = alpha - (m - BigInt(1));
    return charAtIndex(d);
  }

  function calculateCharacterAtIndex() {
    if (!window.BigInt)
        return;
    var output = document.getElementById("s_alpha_output");
    try {
      var alpha = BigInt(document.getElementById("alpha_input").value);
      output.value = charAtIndex(alpha);
    } catch(e) {
      output.value = e.message;
      throw e;
    }
  }
  calculateCharacterAtIndex();
</script>
</div>

<p>The following intermediary step will be helpful to evaluate <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math> at infinite ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>:</p>

<h2 id="proposition">Proposition</h2>

<p>Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> is infinite and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>=</mo><msub><mo lspace="0em" rspace="0em">log</mo><mi>ω</mi></msub><mo stretchy="false">(</mo><mi>α</mi><mo stretchy="false">)</mo><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta = \log_{\omega}(\alpha) \geq 1</annotation></semantics></math>.
Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>q</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">1 \leq q &lt; \omega</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>0</mn><mo>≤</mo><mi>ρ</mi><mo>&lt;</mo><msup><mi>ω</mi><mi>β</mi></msup></mrow><annotation encoding="TeX">0 \leq \rho &lt; \omega^\beta</annotation></semantics></math> be the quotient
and remainder of the euclidean division of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> by <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msup><mi>ω</mi><mi>β</mi></msup><annotation encoding="TeX">\omega^\beta</annotation></semantics></math>.
Let’s define:</p>

<p>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mi>n</mi><mo>=</mo><mrow><mo>{</mo><mtable displaystyle="false" columnalign="left left"><mtr><mtd><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo></mrow><mo>⌋</mo></mrow></mtd><mtd><mtext> if </mtext><mi>q</mi><mtext> is not a power of 2 or this value is </mtext><mo>≤</mo><mi>ρ</mi></mtd></mtr><mtr><mtd><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo></mrow><mo>⌋</mo></mrow><mo>−</mo><mn>1</mn></mtd><mtd><mtext> otherwise.</mtext></mtd></mtr></mtable></mrow></mrow><annotation encoding="TeX">n = \begin{cases}
    \left\lfloor {\log_2(q)} \right\rfloor &amp; \text{ if } q \text{ is not a power of 2 or this value is } \leq \rho \\
    \left\lfloor {\log_2(q)} \right\rfloor - 1 &amp; \text{ otherwise.}
 \end{cases}</annotation></semantics></math>
</p>

<p>Then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> is:</p>

<ul>
  <li>A comma if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="TeX">\alpha = {\omega^{\beta} 2^n + n}</annotation></semantics></math></li>
  <li>An opening brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow></mrow><annotation encoding="TeX">\alpha = {\omega^{\beta} 2^n + n + 1}</annotation></semantics></math></li>
   <li>An closing brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="TeX">\alpha = {\omega^{\beta} 2^{n+1} + n}</annotation></semantics></math></li>
   <li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>δ</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\delta]</annotation></semantics></math> otherwise where <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>δ</mi><annotation encoding="TeX">\delta</annotation></semantics></math> is the unique
   ordinal such that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi><mo>+</mo><mn>2</mn><mo>+</mo><mi>δ</mi></mrow></mrow><annotation encoding="TeX">\alpha = {\omega^\beta 2^n + n + 2 + \delta}</annotation></semantics></math>
   and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>δ</mi><mo>&lt;</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="TeX">\delta &lt; {\omega^{\beta} 2^n + n}</annotation></semantics></math>.
   </li>
 </ul>

<p>Proof: First by construction we have <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><mrow><msup><mi>ω</mi><mi>β</mi></msup><mi>q</mi></mrow><mo>+</mo><mi>ρ</mi></mrow></mrow><annotation encoding="TeX">\alpha = { {\omega^\beta q } + \rho}</annotation></semantics></math>.</p>

<p>If the first case of the definition of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>n</mi><annotation encoding="TeX">n</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>n</mi></msup><mo>≤</mo><mi>q</mi><mo>&lt;</mo><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow><annotation encoding="TeX">2^n \leq q &lt; 2^{n+1}</annotation></semantics></math> so we always have <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>&lt;</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mrow><mo stretchy="false">(</mo><mi>q</mi><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>≤</mo><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msub></mrow><annotation encoding="TeX">\alpha &lt; {\omega^\beta {(q+1)}} \leq \omega^\beta 2^{n+1} \leq L_{\omega{\beta} + n + 1}</annotation></semantics></math>.
If additionnaly <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>q</mi><annotation encoding="TeX">q</annotation></semantics></math> is not a power then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>n</mi></msup><mo>&lt;</mo><mi>q</mi></mrow><annotation encoding="TeX">2^n &lt; q</annotation></semantics></math> and so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≥</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mi>q</mi></mrow><mo>≥</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></mrow><mo>≥</mo><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub></mrow><annotation encoding="TeX">\alpha \geq {\omega^{\beta}q} \geq {\omega^{\beta}{(2^n+1)}} \geq L_{\omega{\beta} + n}</annotation></semantics></math>. Otherwise <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>q</mi><mo>=</mo><msup><mn>2</mn><mi>n</mi></msup></mrow><annotation encoding="TeX">q = 2^n</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>≤</mo><mi>ρ</mi></mrow><annotation encoding="TeX">n \leq \rho</annotation></semantics></math> and so again <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≥</mo><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub></mrow><annotation encoding="TeX">\alpha \geq L_{\omega{\beta} + n}</annotation></semantics></math>.</p>

<p>In the second case of the definition of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>n</mi><annotation encoding="TeX">n</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo></mrow><mo>⌋</mo></mrow><mo>≥</mo><mi>ρ</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">\left\lfloor {\log_2(q)} \right\rfloor \geq \rho + 1</annotation></semantics></math> so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>≥</mo><mi>ρ</mi><mo>≥</mo><mn>0</mn></mrow><annotation encoding="TeX">n \geq \rho \geq 0</annotation></semantics></math>. <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>q</mi><annotation encoding="TeX">q</annotation></semantics></math> is a power of 2 and more precisely <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>q</mi><mo>=</mo><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>&gt;</mo><msup><mn>2</mn><mi>n</mi></msup></mrow><annotation encoding="TeX">q = 2^{n+1} &gt; 2^n</annotation></semantics></math> so we deduce the same way as in the previous case that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≥</mo><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub></mrow><annotation encoding="TeX">\alpha \geq L_{\omega{\beta} + n}</annotation></semantics></math>. Moreover, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ρ</mi><mo>&lt;</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">\rho &lt; n + 1</annotation></semantics></math> so again <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>+</mo><mi>ρ</mi></mrow><mo>&lt;</mo><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msub></mrow><annotation encoding="TeX">\alpha = {\omega^\beta 2^{n+1} + \rho} &lt; L_{\omega{\beta} + n + 1}</annotation></semantics></math>.</p>

<p>We can thus view <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{\omega \beta + n + 1}</annotation></semantics></math> as a concatenation of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub><annotation encoding="TeX">S_{\omega \beta+n}</annotation></semantics></math>, a comma, an opening brace, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub><annotation encoding="TeX">S_{\omega \beta+n}</annotation></semantics></math> and
a closing brace. We assume that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup></mrow><mo>+</mo><mi>n</mi><mo>+</mo><mn>2</mn></mrow><mo>≤</mo><mi>α</mi><mo>&lt;</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>+</mo><mi>n</mi></mrow></mrow><annotation encoding="TeX"> { {\omega^{\beta} {2^n}} + n + 2} \leq \alpha &lt;
{\omega^{\beta} 2^{n+1} + n}</annotation></semantics></math> as the three other cases are handled by the lemma. Then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>δ</mi><annotation encoding="TeX">\delta</annotation></semantics></math> is well-defined and is actually the index of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> in the second copy of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub><annotation encoding="TeX">S_{\omega \beta + n}</annotation></semantics></math> so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mi>S</mi><mrow><mo stretchy="false">[</mo><mi>δ</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="TeX">{S[\alpha]} = S{[\delta]}</annotation></semantics></math>. □</p>

<p>We are now ready to give a nice way to evaluate <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math> at any ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>:</p>

<h2 id="theorem">Theorem</h2>

<p><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> can be calculated inductively as follows:</p>

<ul>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">\alpha = 0</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> is the character "∅".</li>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>0</mn><mo>&lt;</mo><mi>α</mi><mo>≤</mo><mi>ω</mi></mrow><annotation encoding="TeX">0 &lt; \alpha \leq \omega</annotation></semantics></math> then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><msup><mn>2</mn><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></msup><mo>−</mo><mn>3</mn></mrow><mo>≤</mo><mi>α</mi><mo>≤</mo><mrow><msup><mn>2</mn><mrow><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>4</mn></mrow></mrow><annotation encoding="TeX">
 \right\rfloor}} - 3} \leq
\alpha \leq  \right\rfloor + 1}} - 4}</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> is equal to:
  <ul>
    <li>A comma if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mn>2</mn><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></msup><mo>−</mo><mn>3</mn></mrow></mrow><annotation encoding="TeX">\alpha = {2^{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor} - 3}</annotation></semantics></math></li>
    <li>An opening brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mn>2</mn><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></msup><mo>−</mo><mn>2</mn></mrow></mrow><annotation encoding="TeX">\alpha = {2^{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor} - 2}</annotation></semantics></math></li>
    <li>A closing brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><msup><mn>2</mn><mrow><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>4</mn></mrow><annotation encoding="TeX">\alpha = {2^{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor + 1}} - 4</annotation></semantics></math></li>
    <li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>δ</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\delta]</annotation></semantics></math> otherwise where
     <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>δ</mi><mo>=</mo><mrow><mi>α</mi><mo>−</mo><mrow><mo>(</mo><mrow><msup><mn>2</mn><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></msup><mo>−</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow><mo>≤</mo><mrow><msup><mn>2</mn><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></msup><mo>−</mo><mn>4</mn></mrow><mo>≤</mo><mi>α</mi><mo>−</mo><mn>3</mn></mrow><annotation encoding="TeX">\delta = {\alpha - \left( 2^{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor} - 1 \right)} \leq {2^{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor} - 4} \leq \alpha - 3</annotation></semantics></math>.<br />
     Moreover <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>δ</mi><annotation encoding="TeX">\delta</annotation></semantics></math> compares against <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> as follows:
     <math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mfrac><mi>δ</mi><mi>α</mi></mfrac><mo>≤</mo><mfrac><mn>1</mn><mn>2</mn></mfrac><mo>+</mo><mfrac><mn>1</mn><msup><mn>2</mn><mrow><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow><mo>+</mo><mn>1</mn></mrow></msup></mfrac><mo>≤</mo><mfrac><mn>3</mn><mn>4</mn></mfrac></mrow><annotation encoding="TeX">\frac{\delta}{\alpha} \leq \frac{1}{2} + \frac{1}{2^{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor + 1}} \leq \frac{3}{4}</annotation></semantics></math>
     and
     <math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>δ</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow><mo>&lt;</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></mrow><annotation encoding="TeX">
{\left\lfloor {\log_2{(\delta+3)}} \right\rfloor} &lt;
{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor}</annotation></semantics></math>
     </li>
  </ul>
</li>
  <li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> is infinite, let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>0</mn><mo>&lt;</mo><msub><mi>c</mi><mn>1</mn></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">0 &lt; c_1 &lt; \omega</annotation></semantics></math> be the coefficient
  in its <a href="https://en.wikipedia.org/wiki/Ordinal_arithmetic#Cantor_normal_form">Cantor normal form</a> corresponding to the smallest infinite term
  and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">c_0 &lt; \omega</annotation></semantics></math> be finite term if there is one, or zero otherwise.
  Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>k</mi><annotation encoding="TeX">k</annotation></semantics></math> be the exponent corresponding to the smallest nonzero
  term in the binary decomposition of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math>.
  Then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> is equal to:
  <ul>
  <li>A closing brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>≤</mo><mi>k</mi><mo>−</mo><mn>1</mn></mrow><annotation encoding="TeX">c_0 \leq k - 1</annotation></semantics></math>.</li>
  <li>A comma if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>=</mo><mi>k</mi></mrow><annotation encoding="TeX">c_0 = k</annotation></semantics></math>.</li>
  <li>An opening brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>=</mo><mi>k</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">c_0 = k + 1</annotation></semantics></math>.</li>
  <li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>−</mo><mrow><mo stretchy="false">(</mo><mi>k</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[{c_0 - {(k+2)}}]</annotation></semantics></math> if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>≥</mo><mi>k</mi><mo>+</mo><mn>2</mn></mrow><annotation encoding="TeX">c_0 \geq k + 2</annotation></semantics></math>.</li>
  </ul>
</li>

</ul>

<p>Proof:</p>

<p>The case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">\alpha = 0</annotation></semantics></math> is clear. Suppose <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>0</mn><mo>&lt;</mo><mi>α</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">0 &lt; \alpha &lt; \omega</annotation></semantics></math> and let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>l</mi><mo>=</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></mrow><annotation encoding="TeX">l = {\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor}</annotation></semantics></math>. By definition <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>≤</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo>&lt;</mo><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow><annotation encoding="TeX">2^l \leq \alpha + 3 &lt; 2^{l+1}</annotation></semantics></math> so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>3</mn><mo>≤</mo><mi>α</mi><mo>≤</mo><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>4</mn></mrow><annotation encoding="TeX">2^l - 3 \leq \alpha \leq 2^{l+1} - 4</annotation></semantics></math>. Let’s consider the case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn><mo>≤</mo><mi>α</mi><mo>≤</mo><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>5</mn></mrow><annotation encoding="TeX">2^l - 1 \leq \alpha \leq 2^{l+1} - 5</annotation></semantics></math> as the three other cases are already known from the Lemma. <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{l+1}</annotation></semantics></math> is made of the concatenation of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>l</mi></msub><annotation encoding="TeX">S_l</annotation></semantics></math>, a comma and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>l</mi></msub><annotation encoding="TeX">S_l</annotation></semantics></math> surrounded by braces. <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>δ</mi><annotation encoding="TeX">\delta</annotation></semantics></math> is actually the index of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> in the second copy of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>l</mi></msub><annotation encoding="TeX">S_l</annotation></semantics></math> so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mi>S</mi><mrow><mo stretchy="false">[</mo><mi>δ</mi><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="TeX">{S[\alpha]} = S{[\delta]}</annotation></semantics></math>. The first equality is straighforward:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mi>δ</mi><mo>=</mo><mrow><mi>α</mi><mo>−</mo><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></mrow><mo>≤</mo><mrow><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>5</mn><mo>−</mo><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>4</mn></mrow><mo>=</mo><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn><mo>−</mo><mn>3</mn></mrow><mo>≤</mo><mi>α</mi><mo>−</mo><mn>3</mn></mrow><annotation encoding="TeX">\delta = {\alpha - {(2^l -1)}} \leq
{2^{l+1} - 5 - {(2^l -1)}} = {2^l - 4} = {2^l - 1 - 3}\leq \alpha - 3</annotation></semantics></math></p>

<p>Morever we have:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mfrac><mi>δ</mi><mi>α</mi></mfrac><mo>≤</mo><mrow><mn>1</mn><mo>−</mo><mfrac><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn></mrow><mrow><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>+</mo><mn>5</mn></mrow></mfrac></mrow><mo>≤</mo><mrow><mn>1</mn><mo>−</mo><mfrac><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn></mrow><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup></mfrac></mrow><mo>≤</mo><mrow><mfrac><mn>1</mn><mn>2</mn></mfrac><mo>+</mo><mfrac><mn>1</mn><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup></mfrac></mrow></mrow><annotation encoding="TeX">
\frac{\delta}{\alpha} \leq {1 - \frac{2^l - 1}{2^{l+1}+5}} \leq
{1 - \frac{2^l - 1}{2^{l+1}}} \leq {\frac{1}{2} + \frac{1}{2^{l+1}}}
</annotation></semantics></math></p>

<p>and so the second inequality follows from the fact that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>l</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">l \geq 1</annotation></semantics></math>. Finally, the third inequality comes from:</p>

<p>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msup><mn>2</mn><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>δ</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></msup><mo>≤</mo><mrow><mi>δ</mi><mo>+</mo><mn>3</mn></mrow><mo>≤</mo><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>4</mn><mo>+</mo><mn>3</mn></mrow><mo>&lt;</mo><msup><mn>2</mn><mi>l</mi></msup></mrow><annotation encoding="TeX">
2^{\left\lfloor {\log_2{(\delta+3)}} \right\rfloor} \leq {\delta + 3}
\leq {2^l - 4 + 3} &lt; 2^l</annotation></semantics></math>
</p>

<p>Let’s consider the case of an infinite <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>. For some <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>N</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">N \geq 1</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>β</mi><mi>N</mi></msub><mo>&gt;</mo><msub><mi>β</mi><mrow><mi>N</mi><mo>−</mo><mn>1</mn></mrow></msub><mo>&gt;</mo><mo>…</mo><mo>&gt;</mo><msub><mi>β</mi><mn>1</mn></msub><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta_N &gt; \beta_{N-1} &gt; \dots &gt; \beta_1 \geq 1</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">c_0 &lt; \omega</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>0</mn><mo>&lt;</mo><msub><mi>c</mi><mn>1</mn></msub><mo>,</mo><msub><mi>c</mi><mn>2</mn></msub><mo>,</mo><msub><mi>c</mi><mi>N</mi></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">0 &lt; c_1, c_2, c_N &lt; \omega</annotation></semantics></math>, we can write Cantor’s Normal form as:</p>

<p>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mi>N</mi></msub></msup><msub><mi>c</mi><mi>N</mi></msub></mrow><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mrow><mi>N</mi><mo>−</mo><mn>1</mn></mrow></msub></msup><msub><mi>c</mi><mrow><mi>N</mi><mo>−</mo><mn>1</mn></mrow></msub></mrow><mo>+</mo><mo>…</mo><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msub><mi>c</mi><mn>1</mn></msub></mrow><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">\alpha = { \omega^{\beta_N} c_N} + { \omega^{\beta_{N-1}} c_{N-1} } + \dots
+  { \omega^{\beta_{1}} c_{1} } + c_0</annotation></semantics></math>
</p>

<p>With the notation of the proposition, we have <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>=</mo><msub><mi>β</mi><mi>N</mi></msub></mrow><annotation encoding="TeX">\beta = \beta_N</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>q</mi><mo>=</mo><msub><mi>c</mi><mi>N</mi></msub></mrow><annotation encoding="TeX">q = c_N</annotation></semantics></math> and</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mi>ρ</mi><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mrow><mi>N</mi><mo>−</mo><mn>1</mn></mrow></msub></msup><msub><mi>c</mi><mrow><mi>N</mi><mo>−</mo><mn>1</mn></mrow></msub></mrow><mo>+</mo><mo>…</mo><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msub><mi>c</mi><mn>1</mn></msub></mrow><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">
\rho = { \omega^{\beta_{N-1}} c_{N-1} } + \dots
+ { \omega^{\beta_{1}} c_{1} } + c_0
</annotation></semantics></math></p>

<p>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>N</mi><mo>≥</mo><mn>2</mn></mrow><annotation encoding="TeX">N \geq 2</annotation></semantics></math>, then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ρ</mi><annotation encoding="TeX">\rho</annotation></semantics></math> is infinite and so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>=</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo></mrow><mo>⌋</mo></mrow></mrow><annotation encoding="TeX">n = \left\lfloor {\log_2(q)} \right\rfloor</annotation></semantics></math> and we are in the fouth bullet of the proposition. Moreover <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>q</mi><mo>≥</mo><msup><mn>2</mn><mi>n</mi></msup></mrow><annotation encoding="TeX">q \geq 2^n</annotation></semantics></math> and we can write:</p>

<p>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mi>α</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup></mrow><mo>+</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mrow><mo>(</mo><mrow><mi>q</mi><mo>−</mo><msup><mn>2</mn><mi>n</mi></msup></mrow><mo>)</mo></mrow></mrow><mo>+</mo><mi>ρ</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup></mrow><mo>+</mo><mi>n</mi><mo>+</mo><mn>2</mn><mo>+</mo><mi>δ</mi></mrow><annotation encoding="TeX">\alpha = { \omega^{\beta} 2^n} + {\omega^{\beta} \left(q-2^n\right)} + \rho = { \omega^{\beta} 2^n} + n + 2 + \delta
</annotation></semantics></math>
</p>

<p>where <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>δ</mi><mo>=</mo><mrow><msup><mi>ω</mi><mi>β</mi></msup><mrow><mo>(</mo><mrow><mi>q</mi><mo>−</mo><msup><mn>2</mn><mi>n</mi></msup></mrow><mo>)</mo></mrow></mrow><mo>+</mo><mi>ρ</mi></mrow><annotation encoding="TeX">\delta = {\omega^{\beta} \left(q-2^n\right)} + \rho</annotation></semantics></math> is infinite and so cancels out the <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>+</mo><mn>2</mn></mrow><annotation encoding="TeX">n + 2</annotation></semantics></math> term. It follows that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mi>S</mi><mrow><mo>[</mo><mrow><mrow><msup><mi>ω</mi><mi>β</mi></msup><mrow><mo>(</mo><mrow><mi>q</mi><mo>−</mo><msup><mn>2</mn><mi>n</mi></msup></mrow><mo>)</mo></mrow></mrow><mo>+</mo><mi>ρ</mi></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">S{[\alpha]} = S\left[ {\omega^{\beta} \left(q-2^n\right)} + \rho \right]</annotation></semantics></math>. Essentially, we have just removed from <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mi>N</mi></msub><annotation encoding="TeX">c_{N}</annotation></semantics></math> its term of highest exponent in its binary decomposition!</p>

<p>By repeated application of the theorem, we can remove each binary digit of the <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mi>i</mi></msub><annotation encoding="TeX">c_i</annotation></semantics></math> for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>i</mi><annotation encoding="TeX">i</annotation></semantics></math> going from <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>N</mi><annotation encoding="TeX">N</annotation></semantics></math> to <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mn>2</mn><annotation encoding="TeX">2</annotation></semantics></math>. When then arrive at <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>i</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="TeX">i = 1</annotation></semantics></math>:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mi>S</mi><mrow><mo>[</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msub><mi>c</mi><mn>1</mn></msub><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">{S[\alpha]} = S\left[ \omega^{\beta_1} c_1 + c_0\right]</annotation></semantics></math></p>

<p>With the notation of the proposition, we now have <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>=</mo><msub><mi>β</mi><mn>1</mn></msub></mrow><annotation encoding="TeX">\beta = \beta_1</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>q</mi><mo>=</mo><msub><mi>c</mi><mn>1</mn></msub></mrow><annotation encoding="TeX">q = c_1</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ρ</mi><mo>=</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">\rho = c_0</annotation></semantics></math>. If the binary decomposition of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math> has more than one nonzero digit then so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>q</mi><annotation encoding="TeX">q</annotation></semantics></math> is not a power of 2. So although <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ρ</mi><annotation encoding="TeX">\rho</annotation></semantics></math> is now finite, we are still in the first case of the proposition and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>δ</mi><annotation encoding="TeX">\delta</annotation></semantics></math> remains infinite. So we can remove all but the last digit of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math> by repeated application of the proposition:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mi>S</mi><mrow><mo>[</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msup><mn>2</mn><mi>k</mi></msup><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">{S[\alpha]} = S\left[ \omega^{\beta_1} 2^k + c_0\right]</annotation></semantics></math></p>

<p>where <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>k</mi><annotation encoding="TeX">k</annotation></semantics></math> is the exponent corresponding to the smallest nonzero term in the binary decomposition of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math>.</p>

<p>Using the lemma, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> is a comma if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>=</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">k = c_0</annotation></semantics></math>, an opening brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>=</mo><msub><mi>c</mi><mn>0</mn></msub><mo>−</mo><mn>1</mn></mrow><annotation encoding="TeX">k = c_0 - 1</annotation></semantics></math> and a closing brace if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>=</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">k = c_0 + 1</annotation></semantics></math>.</p>

<p>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>≤</mo><msub><mi>c</mi><mn>0</mn></msub><mo>−</mo><mn>2</mn></mrow><annotation encoding="TeX">k \leq c_0 - 2</annotation></semantics></math> then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>=</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mo stretchy="false">(</mo><msup><mn>2</mn><mi>k</mi></msup><mo stretchy="false">)</mo></mrow><mo>⌋</mo></mrow><mo>≤</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">k = \left\lfloor {\log_2(2^k)} \right\rfloor \leq c_0</annotation></semantics></math> and writing</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msup><mn>2</mn><mi>k</mi></msup><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><mo>=</mo><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msup><mn>2</mn><mi>k</mi></msup><mo>+</mo><mi>k</mi><mo>+</mo><mn>2</mn><mo>+</mo><mrow><mo>(</mo><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>−</mo><mrow><mo stretchy="false">(</mo><mi>k</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo>)</mo></mrow></mrow><annotation encoding="TeX">{\omega^{\beta_1} 2^k + c_0} = \omega^{\beta_1} 2^k + k + 2 + \left(c_0 - {(k + 2)}\right)</annotation></semantics></math></p>

<p>we deduce from the proposition that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mrow><mi>S</mi><mo stretchy="false">[</mo><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>−</mo><mrow><mo stretchy="false">(</mo><mi>k</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo stretchy="false">]</mo></mrow></mrow><annotation encoding="TeX">{S[\alpha]} = {S[{c_0 - {(k+2)}}]}</annotation></semantics></math>.</p>

<p>Finally, if <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>≥</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mn>2</mn></mrow><annotation encoding="TeX">k \geq c_0 + 2</annotation></semantics></math> then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>=</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mo stretchy="false">(</mo><msup><mn>2</mn><mi>k</mi></msup><mo stretchy="false">)</mo></mrow><mo>⌋</mo></mrow><mo>&gt;</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">k = \left\lfloor {\log_2(2^k)} \right\rfloor &gt; c_0</annotation></semantics></math> and writing</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msup><mn>2</mn><mi>k</mi></msup><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><mo>=</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msup><mn>2</mn><mrow><mi>k</mi><mo>−</mo><mn>1</mn></mrow></msup></mrow><mo>+</mo><mi>k</mi><mo>−</mo><mn>1</mn><mo>+</mo><mn>2</mn><mo>+</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msup><mn>2</mn><mrow><mi>k</mi><mo>−</mo><mn>1</mn></mrow></msup></mrow><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">{\omega^{\beta_1} 2^k + c_0} = {\omega^{\beta_1} 2^{k-1}} + k - 1 + 2 +
{\omega^{\beta_1} 2^{k-1}} + c_0</annotation></semantics></math></p>

<p>we deduce from the proposition that</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><mo>=</mo><mi>S</mi><mrow><mo>[</mo><mrow><msup><mi>ω</mi><msub><mi>β</mi><mn>1</mn></msub></msup><msup><mn>2</mn><mrow><mi>k</mi><mo>−</mo><mn>1</mn></mrow></msup><mo>+</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">{S[\alpha]} = S\left[ \omega^{\beta_1} 2^{k-1} + c_0\right]</annotation></semantics></math></p>

<p>We have essentially decremented <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>k</mi><annotation encoding="TeX">k</annotation></semantics></math> and we can repeat this until we reach the case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>=</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">k = c_0 + 1</annotation></semantics></math> for which we already said that the character is a closing brace. □</p>

<p>As an application of this theorem, here is a few simple exercises:</p>

<h2 id="exercise-1">Exercise 1</h2>

<ol>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo>[</mo><mrow><msup><mn>2</mn><mn>72</mn></msup><mo>+</mo><mn>2</mn></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">S\left[2^72 + 2\right]</annotation></semantics></math> is an empty set.</li>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo>[</mo><msup><mi>ω</mi><mn>72</mn></msup><mo>]</mo></mrow></mrow><annotation encoding="TeX">S\left[\omega^72\right]</annotation></semantics></math> is a comma.</li>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo>[</mo><mrow><msup><mi>ω</mi><mn>72</mn></msup><mn>72</mn><mo>+</mo><mn>72</mn></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">S\left[\omega^72 72 + 72\right]</annotation></semantics></math> is a closing brace.</li>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mrow><mo>[</mo><mrow><msup><mi>ω</mi><mn>72</mn></msup><mn>72</mn><mo>+</mo><msup><mi>ω</mi><mn>42</mn></msup><mn>42</mn><mo>+</mo><mn>12</mn></mrow><mo>]</mo></mrow></mrow><annotation encoding="TeX">S\left[\omega^72 72 + \omega^42 42 + 12\right]</annotation></semantics></math> is an opening brace.</li>
</ol>

<h2 id="exercise-2">Exercise 2</h2>

<p>The evaluation of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math> at</p>

<ul>
  <li><a href="https://en.wikipedia.org/wiki/Limit_ordinal">Limit ordinals</a> is either a comma or a closing brace.</li>
  <li><a href="https://en.wikipedia.org/wiki/Epsilon_numbers_(mathematics)">Epsilon numbers</a> is a comma.</li>
  <li><a href="https://en.wikipedia.org/wiki/Additively_indecomposable_ordinal">Indecomposable ordinals</a> is a comma.</li>
</ul>

<h2 id="corollary-1-time-complexity">Corollary 1: Time complexity</h2>

<p>Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> be an ordinal. Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>1</mn></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">c_1 &lt; \omega</annotation></semantics></math> be the coefficient in its <a href="https://en.wikipedia.org/wiki/Ordinal_arithmetic#Cantor_normal_form">Cantor normal form</a> corresponding to the smallest infinite term if there is one, or zero otherwise. Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">c_0 &lt; \omega</annotation></semantics></math> be its finite term if there is one, or zero otherwise. Then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>S</mi><mo stretchy="false">[</mo><mi>α</mi><mo stretchy="false">]</mo></mrow><annotation encoding="TeX">S[\alpha]</annotation></semantics></math> can be evaluated in:</p>

<ul>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mrow><mo>(</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><msup><mrow><mo stretchy="false">(</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow><mn>2</mn></msup><mo>+</mo><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><msub><mi>c</mi><mn>1</mn></msub><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo>)</mo></mrow></mrow><annotation encoding="TeX">O\left( \log_2{(c_0+2)}^2 + \log_2{(c_1+2)} \right)</annotation></semantics></math> elementary arithmetic operations and comparisons on integers.</li>
<li><math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mrow><mo>(</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo>)</mo></mrow></mrow><annotation encoding="TeX">O\left( \log_2{(c_0+2)}\right)</annotation></semantics></math> elementary operations if integers are represented in binary and <a href="https://en.wikipedia.org/wiki/Find_first_set">leading/trailing zero counting</a> and <a href="https://en.wikipedia.org/wiki/Bitwise_operation#Bit_shifts">bit shifts</a> are elementary operations.</li>
</ul>

<p>Proof: First note that the “+ 2” is just to workaround for the edge cases <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">c_0 = 0</annotation></semantics></math> or <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>1</mn></msub><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">c_1 = 0</annotation></semantics></math>.</p>

<p>For the infinite case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>1</mn></msub><mo>&gt;</mo><mn>0</mn></mrow><annotation encoding="TeX">c_1 &gt; 0</annotation></semantics></math> we need to calculate <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>k</mi><annotation encoding="TeX">k</annotation></semantics></math> that is performing the <a href="https://en.wikipedia.org/wiki/Find_first_set">find first set</a>. A naive implementation can be done in <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><msub><mi>c</mi><mn>1</mn></msub><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(\log_2{(c_1+2)})</annotation></semantics></math> steps by browsing the digits of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math> to find the first nonzero for example by calculating the remainder modulo increasing power of 2. Each iteration requires only <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(1)</annotation></semantics></math> elementary integer operations %, * and comparisons. Then returning the result of moving to the finite case requires <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(1)</annotation></semantics></math> integer operations +, − and comparisons.</p>

<p>For the finite case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>1</mn></msub><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">c_1 = 0</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><msub><mi>c</mi><mn>0</mn></msub></mrow><annotation encoding="TeX">\alpha = c_0</annotation></semantics></math>, first notice that we only require <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mrow><mo>(</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo>)</mo></mrow></mrow><annotation encoding="TeX">O\left( \log_2{(c_0+2)}\right)</annotation></semantics></math> recursive calls given the inequality:</p>

<p>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>δ</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow><mo>&lt;</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></mrow><annotation encoding="TeX">
{\left\lfloor {\log_2{(\delta+3)}} \right\rfloor} &lt;
{\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor}
</annotation></semantics></math>
</p>

<p>The case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">\alpha = 0</annotation></semantics></math> only requires one comparison. For the case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>&gt;</mo><mn>0</mn></mrow><annotation encoding="TeX">\alpha &gt; 0</annotation></semantics></math>, we need to calculate <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>l</mi><mo>=</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></mrow><annotation encoding="TeX">l = {\left\lfloor {\log_2{(\alpha+3)}} \right\rfloor}</annotation></semantics></math> which is <a href="https://en.wikipedia.org/wiki/Binary_logarithm#Integer_rounding">integer rounding of the binary logarithm</a> or even just <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msup><mn>2</mn><mi>l</mi></msup><annotation encoding="TeX">2^l</annotation></semantics></math>. As above, we can provide a naive implementation by calculating the quotient modulo increasing power of 2 in <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(l)</annotation></semantics></math> comparisons and elementary integer operations /, *. Then returning the result of moving to a <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>δ</mi><mo>&lt;</mo><mi>α</mi></mrow><annotation encoding="TeX">\delta &lt; \alpha</annotation></semantics></math> requires only <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(1)</annotation></semantics></math> integer operations and comparisons. In total, complexity is <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mrow><mo>(</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><msup><mrow><mo stretchy="false">(</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow><mn>2</mn></msup></mrow><mo>)</mo></mrow></mrow><annotation encoding="TeX">O\left( \log_2{(c_0+2)}^2\right)</annotation></semantics></math>.</p>

<p>Finally, this can be simplified if one calculates <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>k</mi><annotation encoding="TeX">k</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>l</mi><annotation encoding="TeX">l</annotation></semantics></math> by a simple leading/trailing zero counting (or similar) and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msup><mn>2</mn><mi>l</mi></msup><annotation encoding="TeX">2^l</annotation></semantics></math> by a bit shift. □</p>

<h2 id="script-based-on-cantor-normal-form">Script based on Cantor normal form</h2>

<div id="javascript_character_at_alpha" style="border: 1px dashed black; padding: .5em; margin: 1em">
If the coefficients of Cantor normal form of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> corresponding the smallest infinite term and finite term are<br />
<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math> = <input id="c1_input" size="72" type="text" onchange="calculateCharacterAtIndex2()" value="123456789" /><br />
<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>0</mn></msub><annotation encoding="TeX">c_0</annotation></semantics></math> = <input id="c0_input" size="72" type="text" onchange="calculateCharacterAtIndex2()" value="123456789" /><br />
Then the character of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math> at position <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> is<br />
<input id="s_alpha_output_2" type="text" value="BigInt not supported" />
<script>
  function charAtIndex2(c0, c1) {
      if (c1 == BigInt(0)) {
         // Finite case
         return charAtIndex(c0);
      }

      // Not sure whether there is an efficient native BigInt operation, so just
      // use a naive implementation with % and *.
      var k = BigInt(0);
      var quotient = BigInt(2);
      while (!(c1 % quotient)) {
        k++;
        quotient *= BigInt(2);
      }

      if (k == c0)
          return ",";
      if (k == c0 - BigInt(1))
          return "{";
      if (k >= c0 + BigInt(1))
          return "}";
      return charAtIndex(c0 - (k + BigInt(2)))
  }

  function calculateCharacterAtIndex2() {
    if (!window.BigInt)
        return;
    var output = document.getElementById("s_alpha_output_2");
    try {
      var c0 = BigInt(document.getElementById("c0_input").value);
      var c1 = BigInt(document.getElementById("c1_input").value);
      output.value = charAtIndex2(c0, c1);
    } catch(e) {
      output.value = e.message;
      throw e;
    }
  }
  calculateCharacterAtIndex2();
</script>
</div>

<p>Once we have an algorithm for S.charAt(α), it is easy to get an algorithm of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>N</mi><annotation encoding="TeX">N</annotation></semantics></math> times that complexity for S.substr(α, N) calculating the substring of length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>N</mi><annotation encoding="TeX">N</annotation></semantics></math> starting at position <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> by repeated calls to S.charAt(α). Let’s analyze a bit more carefully how we can make this recursive and more efficient:</p>

<h2 id="corollary-2-algorithm-for-ssubstrα-n">Corollary 2: Algorithm for S.substr(α, N)</h2>

<p>Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> be an ordinal and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>N</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">N &lt; \omega</annotation></semantics></math>. Then S.substr(α, N) can be calculated as follows:</p>

<ul>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>N</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">N = 0</annotation></semantics></math> then it is the empty string.</li>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">\alpha = 0</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>N</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="TeX">N = 1</annotation></semantics></math> then it is the character "∅".</li>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>0</mn><mo>&lt;</mo><mi>α</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">0 &lt; \alpha &lt; \omega</annotation></semantics></math>, let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>l</mi><mo>=</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mi>N</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></mrow><annotation encoding="TeX">l = \left\lfloor {\log_2{(\alpha+N+2)}} \right\rfloor</annotation></semantics></math>. We have <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>3</mn><mo>≤</mo><mrow><mi>α</mi><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn></mrow><mo>≤</mo><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>4</mn></mrow><annotation encoding="TeX">2^l-3 \leq {\alpha + N - 1} \leq 2^{l+1} - 4</annotation></semantics></math> and the result is obtained by concatenating the following strings:
<ol>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≤</mo><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>4</mn></mrow><annotation encoding="TeX">\alpha \leq  2^l - 4</annotation></semantics></math>, the substring at offset <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> and length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>3</mn><mo>−</mo><mi>α</mi></mrow><annotation encoding="TeX">2^l - 3 - \alpha</annotation></semantics></math>.</li>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≤</mo><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>3</mn></mrow></mrow><annotation encoding="TeX">\alpha \leq {2^l - 3}</annotation></semantics></math>, a comma.</li>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≤</mo><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>2</mn></mrow><mo>≤</mo><mrow><mi>α</mi><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn></mrow></mrow><annotation encoding="TeX">\alpha \leq {2^l - 2} \leq {\alpha + N - 1}</annotation></semantics></math>, an opening brace.</li>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>α</mi><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn></mrow><mo>≥</mo><mrow><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn></mrow></mrow><annotation encoding="TeX">{\alpha + N - 1} \geq {2^l - 1}</annotation></semantics></math>, the substring at offset <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>δ</mi><mo>=</mo><mrow><mi mathvariant="normal">m</mi><mi mathvariant="normal">a</mi><mi mathvariant="normal">x</mi></mrow><mrow><mo stretchy="false">(</mo><mn>0</mn><mo>,</mo><mi>α</mi><mo>−</mo><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">\delta = \mathrm{max}{(0, \alpha - {(2^l - 1)})}</annotation></semantics></math> and length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>1</mn><mo>+</mo><mrow><mi mathvariant="normal">m</mi><mi mathvariant="normal">i</mi><mi mathvariant="normal">n</mi></mrow><mrow><mo stretchy="false">(</mo><mrow><mi>α</mi><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn></mrow><mo>,</mo><mrow><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>5</mn></mrow><mo stretchy="false">)</mo></mrow><mo>−</mo><mrow><mi mathvariant="normal">m</mi><mi mathvariant="normal">a</mi><mi mathvariant="normal">x</mi></mrow><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>,</mo><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>l</mi></msup><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">1 + \mathrm{min}{({\alpha + N - 1}, {2^{l+1} - 5})} - \mathrm{max}{(\alpha, {(2^l - 1)})}</annotation></semantics></math>.</li>
<li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>α</mi><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn></mrow><mo>=</mo><mrow><msup><mn>2</mn><mrow><mi>l</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>4</mn></mrow></mrow><annotation encoding="TeX">{\alpha + N - 1} = {2^{l+1} - 4}</annotation></semantics></math>, a closing brace.</li>
</ol>
</li>
  <li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> is infinite, let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>0</mn><mo>&lt;</mo><msub><mi>c</mi><mn>1</mn></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">0 &lt; c_1 &lt; \omega</annotation></semantics></math> be the coefficient
  in its <a href="https://en.wikipedia.org/wiki/Ordinal_arithmetic#Cantor_normal_form">Cantor normal form</a> corresponding to the smallest infinite term
  and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">c_0 &lt; \omega</annotation></semantics></math> be finite term if there is one, or zero otherwise.
  Let <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>k</mi><annotation encoding="TeX">k</annotation></semantics></math> be the exponent corresponding to the smallest nonzero
  term in the binary decomposition of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math>. Then the result is obtained by a concatenating the following strings:
  <ol>
  <li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>≤</mo><mi>k</mi><mo>−</mo><mn>1</mn></mrow><annotation encoding="TeX">c_0 \leq k - 1</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi mathvariant="normal">m</mi><mi mathvariant="normal">i</mi><mi mathvariant="normal">n</mi></mrow><mrow><mo stretchy="false">(</mo><mi>N</mi><mo>,</mo><mi>k</mi><mo>−</mo><msub><mi>c</mi><mn>0</mn></msub><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">{\mathrm{min}{(N, k - c_0)}}</annotation></semantics></math> closing braces.</li>
  <li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>≤</mo><mi>k</mi><mo>≤</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn></mrow><annotation encoding="TeX">c_0 \leq k \leq c_0 + N - 1</annotation></semantics></math>, a comma.</li>
  <li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>≤</mo><mi>k</mi><mo>+</mo><mn>1</mn><mo>≤</mo><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn></mrow><annotation encoding="TeX">c_0 \leq k + 1 \leq c_0 + N - 1</annotation></semantics></math>, an opening brace.</li>
  <li>If <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mi>N</mi><mo>−</mo><mn>1</mn><mo>≥</mo><mi>k</mi><mo>+</mo><mn>2</mn></mrow><annotation encoding="TeX">c_0 + N - 1 \geq k + 2</annotation></semantics></math>, the substring at offset <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>δ</mi><mo>=</mo><mrow><mi mathvariant="normal">m</mi><mi mathvariant="normal">a</mi><mi mathvariant="normal">x</mi></mrow><mrow><mo stretchy="false">(</mo><mrow><mn>0</mn><mo>,</mo><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>−</mo><mrow><mo stretchy="false">(</mo><mi>k</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow></mrow><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">\delta = \mathrm{max}{({0, {c_0 - {(k + 2)}}})}</annotation></semantics></math> and length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>c</mi><mn>0</mn></msub><mo>+</mo><mi>N</mi><mo>−</mo><mrow><mrow><mi mathvariant="normal">m</mi><mi mathvariant="normal">a</mi><mi mathvariant="normal">x</mi></mrow><mrow><mo stretchy="false">(</mo><msub><mi>c</mi><mn>0</mn></msub><mo>,</mo><mi>k</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="TeX">c_0 + N - {\mathrm{max}{(c_0, k + 2)}}</annotation></semantics></math>.</li>
  </ol>
  </li>
</ul>

<p>Moreover, this only adds <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(N)</annotation></semantics></math> compared to the complexity of evaluating to a single offset.</p>

<p>Proof: The algorithm is just direct application of the Theorem. For the case where <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≥</mo><mi>ω</mi></mrow><annotation encoding="TeX">\alpha \geq \omega</annotation></semantics></math>, the only change is that we add at most <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>N</mi><annotation encoding="TeX">N</annotation></semantics></math> characters before moving to the finite case. The case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">\alpha &lt; \omega</annotation></semantics></math> is essentially a divide-and-conquer algorithm and we have a relation of the form:</p>

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><mi>T</mi><mo stretchy="false">(</mo><mi>L</mi><mo stretchy="false">)</mo></mrow><mo>=</mo><mn>2</mn><mrow><mi>T</mi><mrow><mo>(</mo><mfrac><mi>L</mi><mn>2</mn></mfrac><mo>)</mo></mrow></mrow><mo>+</mo><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>L</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">{T(L)} = 2{T\left(\frac{L}{2}\right)} + {f(L)}</annotation></semantics></math>

<p>where <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>L</mi><mo>=</mo><msup><mn>2</mn><mi>l</mi></msup><mo>=</mo><mrow><mi mathvariant="normal">Θ</mi><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mi>N</mi><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="TeX">L = 2^l = {\Theta{(\alpha + N)}}</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>f</mi><mrow><mo stretchy="false">(</mo><mi>L</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">f{(L)}</annotation></semantics></math> is <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(1)</annotation></semantics></math> or <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mi>L</mi><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(\log_2{L})</annotation></semantics></math> depending on available operations, but in any case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mrow><mo stretchy="false">(</mo><msqrt><mi>L</mi></msqrt><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">O{(\sqrt{L})}</annotation></semantics></math>. So from the <a href="https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms)">master theorem</a>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>T</mi><mrow><mo stretchy="false">(</mo><mi>L</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>L</mi><mo stretchy="false">)</mo></mrow><mo>=</mo><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mi>N</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">{T{(L)}} = {O(L)} = {O(\alpha+N)}</annotation></semantics></math>. In general, this bound is not as good as repeating <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>N</mi><annotation encoding="TeX">N</annotation></semantics></math> calls to S.charAt!</p>

<p>However, we note that if we assume that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>&gt;</mo><mi>N</mi><mo>−</mo><mn>4</mn></mrow><annotation encoding="TeX">\alpha &gt; N - 4</annotation></semantics></math> then <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mrow><mi>α</mi><mo>+</mo><mn>2</mn><mo>+</mo><mi>N</mi></mrow><mo>&lt;</mo><mrow><mn>2</mn><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="TeX">{\alpha + 2 + N} &lt; {2{(\alpha+3)}}</annotation></semantics></math> and so</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo>(</mo><mrow><mi>α</mi><mo>+</mo><mn>2</mn><mo>+</mo><mi>N</mi></mrow><mo>)</mo></mrow><mo>&lt;</mo><mrow><mn>1</mn><mo>+</mo><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="TeX">\log_2\left(\alpha + 2 + N\right) &lt; {1 + \log_2{(\alpha+3)}}</annotation></semantics></math></p>

<p>We can easily discard the edge case where these start/end offsets point to a brace surrounding the right substring of the iterative step and so we get:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mi>N</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow><mo>=</mo><mrow><mo>⌊</mo><mrow><msub><mo lspace="0em" rspace="0em">log</mo><mn>2</mn></msub><mrow><mo stretchy="false">(</mo><mi>α</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo></mrow></mrow><mo>⌋</mo></mrow></mrow><annotation encoding="TeX">\left\lfloor {\log_2{(\alpha+N+2)}} \right\rfloor = \left\lfloor {\log_2{(\alpha+3)}} \right\rfloor</annotation></semantics></math></p>

<p>which means that the left substring is just empty and so the complexity is not changed compared to S.charAt. Finally, when <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≤</mo><mi>N</mi><mo>−</mo><mn>4</mn></mrow><annotation encoding="TeX">\alpha \leq N - 4</annotation></semantics></math> the previous bound tells us that the steps are done in <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">O(N)</annotation></semantics></math>. □</p>

<h2 id="script-for-ssubstrα-n">Script for S.substr(α, N)</h2>

<div id="javascript_substring" style="border: 1px dashed black; padding: .5em; margin: 1em">
If the coefficients of Cantor normal form of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> corresponding the smallest infinite term and finite term are<br />
<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>1</mn></msub><annotation encoding="TeX">c_1</annotation></semantics></math> = <input id="c1_input_2" size="72" type="text" onchange="calculateSubstring()" value="1" /><br />
<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>c</mi><mn>0</mn></msub><annotation encoding="TeX">c_0</annotation></semantics></math> = <input id="c0_input_2" size="72" type="text" onchange="calculateSubstring()" value="0" /><br />
Then the character of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>S</mi><annotation encoding="TeX">S</annotation></semantics></math> substring of length
<math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>N</mi><annotation encoding="TeX">N</annotation></semantics></math> = <input id="N_input_2" type="number" onchange="calculateSubstring()" value="72" /><br />
and offset <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> is<br />
<input id="s_substring_output" size="72" type="text" value="BigInt not supported" />
<script>
  function BigIntMin(a, b) {
    return a <= b ? a : b;
  }
  function substringAt(c0, c1, N) {
    var result = "", len, delta;
    if (N == BigInt(0)) {
      return result;
    }
    if (c1 > BigInt(0)) {
      // Infinite case
      // Not sure whether there is an efficient native BigInt operation, so
      // just use a naive implementation with % and *.
      var k = BigInt(0);
      var quotient = BigInt(2);
      while (!(c1 % quotient)) {
        k++;
        quotient *= BigInt(2);
      }
      while (c0 <= k - BigInt(1)) {
        result += "}";
        c0++;
        N--;
      }
      if (c0 <= k && N > 0) {
         result += ",";
         c0++;
         N--;
      }
      if (c0 <= k + BigInt(1) && N > 0) {
         result += "{";
         c0++;
         N--;
      }
      if (N > 0) { // c0 >= k + 2
         delta = c0 - (k + BigInt(2));
         result += substringAt(delta, BigInt(0), N);
      }
      return result;
    }

    // Finite case.
    // Not sure whether there is an efficient native BigInt operation, so just
    // serialize in binary and count the digits.
    if (c0 == BigInt(0) && N == 1)
       return "∅";

    var m = BigInt(2) ** BigInt((c0 + N + BigInt(2)).toString(2).length - 1);
    if (c0 <= m - BigInt(4)) {
      delta = c0;
      len = m - BigInt(3) - c0;
      result += substringAt(delta, c1, len);
      c0 += len;
      N -= len;
    }
    if (c0 == m - BigInt(3) && N > 0) {
      result += ",";
      c0++;
      N--;
    }
    if (c0 == m - BigInt(2) && N > 0) {
      result += "{";
      c0++;
      N--;
    }
    if (N > 0) { // c0 >= m - 1
      delta = c0 - (m - BigInt(1));
      len = BigIntMin(N, BigInt(2) * m - BigInt(4) - c0);
      result += substringAt(delta, c1, len);
      c0 += len;
      N -= len;
    }
    if (N > 0) // c0 == 2*m - 4
      result += "}";
    return result;
  }

  function calculateSubstring() {
    if (!window.BigInt)
        return;
    var output = document.getElementById("s_substring_output");
    try {
      var c0 = BigInt(document.getElementById("c0_input_2").value);
      var c1 = BigInt(document.getElementById("c1_input_2").value);
      var N = BigInt(document.getElementById("N_input_2").value);
      output.value = substringAt(c0, c1, N);
    } catch(e) {
      output.value = e.message;
      throw e;
    }
  }
  calculateSubstring();
</script>
</div>


{% endraw %}
