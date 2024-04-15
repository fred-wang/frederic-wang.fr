---
layout: post
title: "Ordinals as strings of ∅, commas and braces"
tags: maths
---

{% raw %}

  <p>This week, my colleagues at Igalia were talking about cutting text at a 72-characters limit for word-wrapping emails. One might say that the <a href="https://en.wikipedia.org/wiki/Construction_of_the_real_numbers">real</a> question is whether 72 is a <a href="https://en.wikipedia.org/wiki/Construction_of_the_real_numbers#Construction_by_Dedekind_cuts">cut</a> or a <a href="https://en.wikipedia.org/wiki/Construction_of_the_real_numbers#Construction_from_Cauchy_sequences">limit</a>. Or wonder how one has decided to <a href="https://en.wikipedia.org/wiki/Set-theoretic_definition_of_natural_numbers#Definition_as_von_Neumann_ordinals">set</a> that particular value?</p>

<p>The latter link explains the recursive definition of 72 as a finite set, which can be written with only braces, commas and the empty set <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>∅</mi><annotation encoding="TeX">\empty</annotation></semantics></math>:</p>

<p>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mn>0</mn><mo>=</mo><mrow><mo stretchy="false">{</mo><mo stretchy="false">}</mo></mrow><mo>=</mo><mi>∅</mi></mrow><annotation encoding="TeX">0 = {\{\}} = \empty</annotation></semantics></math>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mn>1</mn><mo>=</mo><mn>0</mn><mo>∪</mo><mrow><mo stretchy="false">{</mo><mn>0</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mrow><mo stretchy="false">{</mo><mn>0</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mrow><mo stretchy="false">{</mo><mi>∅</mi><mo stretchy="false">}</mo></mrow></mrow><annotation encoding="TeX">1 = 0 \union {\{0\}} = {\{0\}} = {\{\empty\}}</annotation></semantics></math>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mn>2</mn><mo>=</mo><mn>1</mn><mo>∪</mo><mrow><mo stretchy="false">{</mo><mn>1</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mrow><mo stretchy="false">{</mo><mn>0</mn><mo>,</mo><mn>1</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mrow><mo stretchy="false">{</mo><mi>∅</mi><mo>,</mo><mrow><mo stretchy="false">{</mo><mi>∅</mi><mo stretchy="false">}</mo></mrow><mo stretchy="false">}</mo></mrow></mrow><annotation encoding="TeX">2 = 1 \union {\{1\}} = {\{0,1\}} = {\{ \empty, {\{\empty\}} \}}</annotation></semantics></math>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mn>3</mn><mo>=</mo><mn>2</mn><mo>∪</mo><mrow><mo stretchy="false">{</mo><mn>2</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mrow><mo stretchy="false">{</mo><mn>0</mn><mo>,</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mrow><mo stretchy="false">{</mo><mi>∅</mi><mo>,</mo><mrow><mo stretchy="false">{</mo><mi>∅</mi><mo stretchy="false">}</mo></mrow><mo>,</mo><mrow><mo stretchy="false">{</mo><mi>∅</mi><mo>,</mo><mrow><mo stretchy="false">{</mo><mi>∅</mi><mo stretchy="false">}</mo></mrow><mo stretchy="false">}</mo></mrow><mo stretchy="false">}</mo></mrow></mrow><annotation encoding="TeX">3 = 2 \union {\{2\}} = {\{0,1,2\}} =
{\{ \empty, {\{\empty\}}, {\{ \empty, {\{\empty\}} \}} \}}</annotation></semantics></math>
</p>

<p>and so forth until</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mn>72</mn><mo>=</mo><mn>71</mn><mo>∪</mo><mrow><mo stretchy="false">{</mo><mn>71</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mrow><mo stretchy="false">{</mo><mn>0</mn><mo>,</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo>,</mo><mo>…</mo><mo>,</mo><mn>71</mn><mo stretchy="false">}</mo></mrow><mo>=</mo><mo>…</mo></mrow><annotation encoding="TeX">72 = 71 \union {\{71\}} = {\{0,1,2,\dots,71\}} = \dots</annotation></semantics></math></p>

<p>You can notice that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mn>1</mn><annotation encoding="TeX">1</annotation></semantics></math> has only one element <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>∅</mi><annotation encoding="TeX">∅</annotation></semantics></math> and for any <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">n \geq 1</annotation></semantics></math>, in order to enumerate the elements of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">n+1</annotation></semantics></math> using only the four characters <code class="language-plaintext highlighter-rouge">"∅"</code>, <code class="language-plaintext highlighter-rouge">","</code>, <code class="language-plaintext highlighter-rouge">"{"</code> and <code class="language-plaintext highlighter-rouge">"}"</code>, you first write the elements of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>n</mi><annotation encoding="TeX">n</annotation></semantics></math>, followed by a comma, followed by an opening brace, followed by the elements of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>n</mi><annotation encoding="TeX">n</annotation></semantics></math> and finally followed by a closing brace. One can write a simple JavaScript loop that initializes a variable <code>string = "∅"</code> and performs the concatenation <code>string += `,{${string}}`</code> at each step:</p>

<div id="javascript_calculate_string_recursively" style="border: 1px dashed black; padding: .5em; margin: 1em">
The elements of <input id="n_input" type="number" min="1" max="6" onchange="calculateNaturalAsSet()" value="3" /> are<br />
<input id="n_output" size="72" type="text" />
<script>
  function calculateNaturalAsSet() {
    var n = parseInt(document.getElementById("n_input").value, 10);
    var string = "∅";
    for (i = 1; i < n; i++) {
        string += `,{${string}}`;
    }
    document.getElementById("n_output").value = string;
  }
  calculateNaturalAsSet();
</script>
</div>

<h2 id="length-of-the-string">Length of the string</h2>

<p>You notice that the length of the string obtained for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>=</mo><mn>6</mn></mrow><annotation encoding="TeX">n=6</annotation></semantics></math> already exceeds the
72-character limit. From the previous recursive construction of the string one can deduce a recursive definition of its length:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mn>1</mn></msub><mo>=</mo><mn>1</mn></mrow><annotation encoding="TeX">L_1 = 1</annotation></semantics></math> <math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>=</mo><msub><mi>L</mi><mi>n</mi></msub><mo>+</mo><mn>2</mn><mo>+</mo><msub><mi>L</mi><mi>n</mi></msub><mo>+</mo><mn>1</mn><mo>=</mo><mn>2</mn><msub><mi>L</mi><mi>n</mi></msub><mo>+</mo><mn>3</mn></mrow><annotation encoding="TeX">L_{n+1} = L_n + 2 + L_n + 1 = 2L_n +3</annotation></semantics></math></p>

<p>It is easy to see that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mi>n</mi></msub><mo>=</mo><mrow><mi mathvariant="normal">Ω</mi><mrow><mo stretchy="false">(</mo><msup><mn>2</mn><mi>n</mi></msup><mo stretchy="false">)</mo></mrow></mrow></mrow><annotation encoding="TeX">L_n = {\Omega{(2^n)}}</annotation></semantics></math> so although the simple JavaScript loop above uses a time complexity of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>O</mi><mrow><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">{O{(n)}}</annotation></semantics></math> string concatenations, the space complexity is at least exponential. That’s why in the definition of 72 above I used dots instead of showing the whole string!</p>

<p>One can however easily modify the previous JavaScript loop to calculate the length of such a string. At Igalia, we have been working on a new native type called <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt">BigInt</a> which is particularly useful to accurately calculate large integers. The case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>=</mo><mn>72</mn></mrow><annotation encoding="TeX">n = 72</annotation></semantics></math> demonstrates why it is more appropriate than JavaScript Number:</p>

<div id="javascript_calculate_length_recursively" style="border: 1px dashed black; padding: .5em; margin: 1em">
The length of the strings enumerating the elements of <input id="n_input_bis" type="number" min="1" max="260" step="10" onchange="calculateLengthOfNaturalAsSet()" value="72" /> has the following length (first field uses Number, second field uses BigInt):<br />
<input id="n_output_bis_number" size="72" type="text" /><br />
<input id="n_output_bis_bigint" size="72" type="text" value="BigInt not supported" />
<script>
  function calculateLengthOfNaturalAsSet() {
    var n = parseInt(document.getElementById("n_input_bis").value, 10);
    var result_number = 1;
    for (i = 1; i < n; i++)
        result_number = 2 * result_number + 3;
    document.getElementById("n_output_bis_number").value = result_number;
    if (window.BigInt) {
        var result_bigint = BigInt(1);
        for (i = 1; i < n; i++)
            result_bigint = BigInt(2) * result_bigint + BigInt(3);
        document.getElementById("n_output_bis_bigint").value = result_bigint;
    }
  }
  calculateLengthOfNaturalAsSet();
</script>
</div>

<p>One can do better and try to calculate an explicit formula for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mi>n</mi></msub><annotation encoding="TeX">L_n</annotation></semantics></math> for any <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">n \geq 1</annotation></semantics></math>. Since for all <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>i</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">i \geq 1</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mrow><mi>i</mi><mo>+</mo><mn>2</mn></mrow></msub><mo>−</mo><msub><mi>L</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>=</mo><mn>2</mn><mrow><mo>(</mo><mrow><msub><mi>L</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>−</mo><msub><mi>L</mi><mi>i</mi></msub></mrow><mo>)</mo></mrow></mrow><annotation encoding="TeX">L_{i+2} - L_{i+1} = 2\left(L_{i+1} - L_i\right)</annotation></semantics></math> the sequence <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mrow><mo>(</mo><mrow><msub><mi>L</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>−</mo><msub><mi>L</mi><mi>i</mi></msub></mrow><mo>)</mo></mrow><mrow><mi>i</mi><mo>≥</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">\left(L_{i+1} - L_i\right)_{i \geq 1}</annotation></semantics></math> is a <a href="https://en.wikipedia.org/wiki/Geometric_progression">geometric sequence</a> with common ratio 2 and for all <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>i</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">i \geq 1</annotation></semantics></math> we can write</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><mrow><msub><mi>L</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>−</mo><msub><mi>L</mi><mi>i</mi></msub></mrow><mo>=</mo><mrow><msup><mn>2</mn><mrow><mi>i</mi><mo>−</mo><mn>1</mn></mrow></msup><mrow><mo>(</mo><mrow><msub><mi>L</mi><mn>2</mn></msub><mo>−</mo><msub><mi>L</mi><mn>1</mn></msub></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="TeX">{L_{i+1} - L_{i}} = {2^{i-1} \left( L_2 - L_1 \right)}</annotation></semantics></math></p>

<p>Summing this up for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mn>1</mn><mo>≤</mo><mi>i</mi><mo>≤</mo><mi>n</mi><mo>−</mo><mn>1</mn></mrow><annotation encoding="TeX">1 \leq i \leq n - 1</annotation></semantics></math>:</p>

<p>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mi>n</mi></msub><mo>−</mo><msub><mi>L</mi><mn>1</mn></msub><mo>=</mo><mrow><munderover><mo>∑</mo><mrow><mi>i</mi><mo>=</mo><mn>1</mn></mrow><mrow><mi>n</mi><mo>−</mo><mn>1</mn></mrow></munderover><msub><mi>L</mi><mrow><mi>i</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>−</mo><msub><mi>L</mi><mi>i</mi></msub></mrow><mo>=</mo><mrow><mrow><mo>(</mo><mrow><msub><mi>L</mi><mn>2</mn></msub><mo>−</mo><msub><mi>L</mi><mn>1</mn></msub></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><munderover><mo>∑</mo><mrow><mi>i</mi><mo>=</mo><mn>0</mn></mrow><mrow><mi>n</mi><mo>−</mo><mn>2</mn></mrow></munderover><msup><mn>2</mn><mi>i</mi></msup></mrow><mo>)</mo></mrow></mrow><mo>=</mo><mrow><mrow><mo>(</mo><mrow><msub><mi>L</mi><mn>2</mn></msub><mo>−</mo><msub><mi>L</mi><mn>1</mn></msub></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><msup><mn>2</mn><mrow><mi>n</mi><mo>−</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>1</mn></mrow><mo>)</mo></mrow></mrow></mrow><annotation encoding="TeX">
L_n - L_1 =
{\sum_{i=1}^{n-1} L_{i+1} - L_{i}} =
{\left( L_2 - L_1 \right)
\left(\sum_{i=0}^{n-2} 2^i \right)}=
{ {\left( L_2 - L_1 \right)} {\left(2^{n-1}-1\right)} }
</annotation></semantics></math>
</p>

<p>Finally, given that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mn>1</mn></msub><mo>=</mo><mn>1</mn></mrow><annotation encoding="TeX">L_1 = 1</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mn>2</mn></msub><mo>=</mo><mn>2</mn><msub><mi>L</mi><mn>1</mn></msub><mo>+</mo><mn>3</mn><mo>=</mo><mn>5</mn></mrow><annotation encoding="TeX">L_2 = 2L_1 + 3 = 5</annotation></semantics></math>, one can write for all <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">n \geq 1</annotation></semantics></math>:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mi>n</mi></msub><mo>=</mo><mo stretchy="false">(</mo><msup><mn>2</mn><mrow><mi>n</mi><mo>−</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo><mo stretchy="false">(</mo><mn>5</mn><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo><mo>+</mo><mn>1</mn><mo>=</mo><msup><mn>2</mn><mrow><mi>n</mi><mo>+</mo><mn>1</mn></mrow></msup><mo>−</mo><mn>3</mn></mrow><annotation encoding="TeX">L_n = (2^{n-1}-1) (5-1) + 1 = 2^{n+1} - 3</annotation></semantics></math></p>

<p>This formula can be used to calculate <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mi>n</mi></msub><annotation encoding="TeX">L_n</annotation></semantics></math> using built-in JavaScript exponentation instead of a loop, as done below.</p>

<div id="javascript_calculate_string_by_exponentiation" style="border: 1px dashed black; padding: .5em; margin: 1em">
The length of the strings enumerating the elements of <input id="n_input_ter" type="number" min="1" max="260" step="10" onchange="calculateLengthOfNaturalAsSetUsingExponentiation()" value="72" /> has the following length (first field uses Number, second field uses BigInt):<br />
<input id="n_output_ter_number" size="72" type="text" /><br />
<input id="n_output_ter_bigint" size="72" type="text" value="BigInt not supported" />
<script>
  function calculateLengthOfNaturalAsSetUsingExponentiation() {
    var n = parseInt(document.getElementById("n_input_ter").value, 10);
    document.getElementById("n_output_ter_number").value = 2 ** (n+1) - 3;
    if (window.BigInt)
        document.getElementById("n_output_ter_bigint").value = BigInt(2) ** (BigInt(n+1)) - BigInt(3);
  }
  calculateLengthOfNaturalAsSetUsingExponentiation();
</script>
</div>

<h2 id="order-type-of-infinite-strings">Order-type of infinite strings</h2>

<p>It is possible to generalize this problem to infinite <a href="https://en.wikipedia.org/wiki/Ordinal_number">ordinal numbers</a>.  The string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_{\alpha}</annotation></semantics></math> and its length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mi>α</mi></msub><annotation encoding="TeX">L_\alpha</annotation></semantics></math> are defined by induction for any ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>. <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>0</mn></msub><annotation encoding="TeX">S_0</annotation></semantics></math> is the empty string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mn>0</mn></msub><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">L_0 = 0</annotation></semantics></math>. <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>1</mn></msub><annotation encoding="TeX">S_1</annotation></semantics></math> is the string with one character <code class="language-plaintext highlighter-rouge">"∅"</code> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mn>1</mn></msub><mo>=</mo><mn>1</mn></mrow><annotation encoding="TeX">L_1 = 1</annotation></semantics></math>. For <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">\alpha \geq 1</annotation></semantics></math>, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{\alpha+1}</annotation></semantics></math> is the string obtained by concatenating the string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math>, a comma character <code class="language-plaintext highlighter-rouge">","</code>, an opening brace character <code class="language-plaintext highlighter-rouge">"{"</code>, the string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math> and finally a closing brace character <code class="language-plaintext highlighter-rouge">"}"</code>. It is of length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mrow><mi>α</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>=</mo><msub><mi>L</mi><mi>α</mi></msub><mo>+</mo><mn>2</mn><mo>+</mo><msub><mi>L</mi><mi>α</mi></msub><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">L_{\alpha+1} = L_\alpha + 2 + L_\alpha + 1</annotation></semantics></math>. Beware that ordinal operations are not commutative so this cannot be simplified a priori!</p>

<p>For any limit ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>λ</mi><annotation encoding="TeX">\lambda</annotation></semantics></math>, the string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>λ</mi></msub><annotation encoding="TeX">S_\lambda</annotation></semantics></math> is obtained by taking the union of the <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mi>α</mi></msub><annotation encoding="TeX">L_\alpha</annotation></semantics></math>-sequence <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>α</mi></msub><annotation encoding="TeX">S_\alpha</annotation></semantics></math> for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>α</mi><mo>&lt;</mo><mi>λ</mi></mrow><annotation encoding="TeX">\alpha &lt; \lambda</annotation></semantics></math>. This is still a well-defined sequence since these strings always agree on the character at a given index. <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>λ</mi></msub><annotation encoding="TeX">S_\lambda</annotation></semantics></math> is of length <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mi>λ</mi></msub><mo>=</mo><munder><mo lspace="0em" rspace="0em">sup</mo><mrow><mi>α</mi><mo>&lt;</mo><mi>λ</mi></mrow></munder><msub><mi>L</mi><mi>α</mi></msub></mrow><annotation encoding="TeX">L_\lambda = \sup_{\alpha &lt; \lambda} L_\alpha</annotation></semantics></math>.</p>

<p>By construction, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mi>α</mi></msub><annotation encoding="TeX">L_\alpha</annotation></semantics></math> is an increasing sequence of ordinals and so <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mi>α</mi></msub><mo>≥</mo><mi>α</mi></mrow><annotation encoding="TeX">L_\alpha \geq \alpha</annotation></semantics></math>. Can we calculate it more explicitly?</p>

<div style="border: 1px dashed black; padding: .5em; margin: 1em">
Warning: The rest of the blog post gives the solution to this puzzle, so you
might want to have fun solving it yourself first and then go back checking
my proposed solution later 😉...
</div>

<p>Let’s consider some examples. In the case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ω</mi><mo>=</mo><mi>ℕ</mi></mrow><annotation encoding="TeX">\omega = \mathbb N</annotation></semantics></math>, the string <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mi>ω</mi></msub><annotation encoding="TeX">S_\omega</annotation></semantics></math> can be more easily seen as the <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ω</mi><annotation encoding="TeX">\omega</annotation></semantics></math>-concatenation of finite strings: the empty set, a comma, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>1</mn></msub><annotation encoding="TeX">S_1</annotation></semantics></math> surrounded by braces, a comma, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>2</mn></msub><annotation encoding="TeX">S_2</annotation></semantics></math> surrounded by braces, a comma, <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mn>3</mn></msub><annotation encoding="TeX">S_3</annotation></semantics></math> surrounded by braces, a comma, etc So clearly <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><msub><mi>L</mi><mi>ω</mi></msub><mo>=</mo><mi>ω</mi></mrow><annotation encoding="TeX">L_{\omega} = \omega</annotation></semantics></math> and this aligns with the definition for limit ordinal.</p>

<p>In order to write <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>ω</mi><mo>+</mo><mn>1</mn></mrow></msub><annotation encoding="TeX">S_{\omega+1}</annotation></semantics></math>, you first write the elements of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ω</mi><annotation encoding="TeX">\omega</annotation></semantics></math>, followed by a comma, followed by an opening brace, followed by the elements of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ω</mi><annotation encoding="TeX">\omega</annotation></semantics></math> and finally followed by a closing brace. So really this is an <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ω</mi><mo>+</mo><mi>ω</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">\omega + \omega + 1</annotation></semantics></math> sequence. This aligns with the definition in the successor ordinal case, using the fact that <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>+</mo><mi>ω</mi><mo>=</mo><mi>ω</mi></mrow><annotation encoding="TeX">k + \omega = \omega</annotation></semantics></math> for any <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>k</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">k &lt; \omega</annotation></semantics></math>:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>=</mo><msub><mi>L</mi><mi>ω</mi></msub><mo>+</mo><mn>2</mn><mo>+</mo><msub><mi>L</mi><mi>ω</mi></msub><mo>+</mo><mn>1</mn><mo>=</mo><mi>ω</mi><mo>+</mo><mn>2</mn><mo>+</mo><mi>ω</mi><mo>+</mo><mn>1</mn><mo>=</mo><mi>ω</mi><mn>2</mn><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">L_{\omega+1} = L_\omega + 2 + L_\omega + 1 = \omega + 2 + \omega + 1 = \omega2 + 1</annotation></semantics></math></p>

<p>Continuing for other successor ordinals, one can write</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mn>2</mn></mrow></msub><mo>=</mo><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>+</mo><mn>2</mn><mo>+</mo><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>+</mo><mn>1</mn><mo>=</mo><mi>ω</mi><mn>2</mn><mo>+</mo><mn>1</mn><mo>+</mo><mn>2</mn><mo>+</mo><mi>ω</mi><mn>2</mn><mo>+</mo><mn>1</mn><mo>+</mo><mn>1</mn><mo>=</mo><mi>ω</mi><mn>4</mn><mo>+</mo><mn>2</mn></mrow><annotation encoding="TeX">L_{\omega+2} = L_{\omega+1} + 2 + L_{\omega+1} + 1 = \omega2 + 1 + 2 + \omega2 + 1 + 1 = \omega4 + 2</annotation></semantics></math>
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mn>3</mn></mrow></msub><mo>=</mo><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mn>2</mn></mrow></msub><mo>+</mo><mn>2</mn><mo>+</mo><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mn>2</mn></mrow></msub><mo>+</mo><mn>1</mn><mo>=</mo><mi>ω</mi><mn>4</mn><mo>+</mo><mn>1</mn><mo>+</mo><mn>2</mn><mo>+</mo><mi>ω</mi><mn>4</mn><mo>+</mo><mn>2</mn><mo>+</mo><mn>1</mn><mo>=</mo><mi>ω</mi><mn>8</mn><mo>+</mo><mn>3</mn></mrow><annotation encoding="TeX">L_{\omega+3} = L_{\omega+2} + 2 + L_{\omega+2} + 1 = \omega4 + 1 + 2 + \omega4 + 2 + 1 = \omega8 + 3</annotation></semantics></math></p>

<p>and more generally for all <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">n &lt; \omega</annotation></semantics></math>:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mi>n</mi></mrow></msub><mo>=</mo><mi>ω</mi><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi></mrow><annotation encoding="TeX">L_{\omega+n} = \omega{2^n} + n</annotation></semantics></math></p>

<p>To calculate <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>S</mi><mrow><mi>ω</mi><mn>2</mn></mrow></msub><annotation encoding="TeX">S_{\omega2}</annotation></semantics></math>, one takes the union for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">n &lt; \omega</annotation></semantics></math> of the <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><msub><mi>L</mi><mrow><mi>ω</mi><mo>+</mo><mi>n</mi></mrow></msub><annotation encoding="TeX">L_{\omega+n}</annotation></semantics></math>-sequence of characters describing <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ω</mi><mo>+</mo><mi>n</mi></mrow><annotation encoding="TeX">\omega+n</annotation></semantics></math>. Its length is</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mn>2</mn></mrow></msub><mo>=</mo><mrow><munder><mo lspace="0em" rspace="0em">sup</mo><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></munder><mrow><mo>(</mo><mrow><mi>ω</mi><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi></mrow><mo>)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mn>2</mn></msup></mrow><annotation encoding="TeX">L_{\omega2} = {\sup_{n &lt; \omega} \left(\omega{2^n} + n\right)} = \omega^2</annotation></semantics></math></p>

<p>Then the exact same calculation as above leads for all <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">n &lt; \omega</annotation></semantics></math> to</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mn>2</mn><mo>+</mo><mi>n</mi></mrow></msub><mo>=</mo><msup><mi>ω</mi><mn>2</mn></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi></mrow><annotation encoding="TeX">L_{\omega2+n} = \omega^2{2^n} + n</annotation></semantics></math></p>

<p>Continuing this kind of calculations for larger values <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ω</mi><mn>3</mn><mo>,</mo><mi>ω</mi><mn>4</mn><mo>,</mo><mo>…</mo><mo>,</mo><msup><mi>ω</mi><mn>2</mn></msup></mrow><annotation encoding="TeX">\omega3, \omega4, \dots, \omega^2</annotation></semantics></math> suggests the following conjecture: For every infinite ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math>, the order-type of the sequence describing its element is:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mi>α</mi></msub><mo>=</mo><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub><mo>=</mo><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi></mrow><annotation encoding="TeX">L_{\alpha} = L_{\omega \beta + n} = \omega^\beta 2^n + n</annotation></semantics></math></p>

<p>where <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta \geq 1</annotation></semantics></math> and <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow><annotation encoding="TeX">n &lt; \omega</annotation></semantics></math> are the quotient and remainder of the euclidean division of <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>α</mi><annotation encoding="TeX">\alpha</annotation></semantics></math> by <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>ω</mi><annotation encoding="TeX">\omega</annotation></semantics></math>.</p>

<p>Let’s sketch the proof by induction on <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>β</mi><annotation encoding="TeX">\beta</annotation></semantics></math>. We already explained the case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta = 1</annotation></semantics></math> in the example above. Similarly, for a given <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta \geq 1</annotation></semantics></math>, it is enough to prove the case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>=</mo><mn>0</mn></mrow><annotation encoding="TeX">n = 0</annotation></semantics></math>, the formula for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>n</mi><mo>&gt;</mo><mn>0</mn></mrow><annotation encoding="TeX">n &gt; 0</annotation></semantics></math> follows, using the property <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mo>∀</mo><mi>k</mi><mo>&lt;</mo><mi>ω</mi><mo>,</mo><mi>k</mi><mo>+</mo><msup><mi>ω</mi><mi>β</mi></msup><mo>=</mo><msup><mi>ω</mi><mi>β</mi></msup></mrow><annotation encoding="TeX">\forall k &lt; \omega, k + \omega^\beta = \omega^\beta</annotation></semantics></math> and the calculations we gave for the case <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>=</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta = 1</annotation></semantics></math>.</p>

<p>If the formula holds for some <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>≥</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta \geq 1</annotation></semantics></math> then because <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>ω</mi><mrow><mo stretchy="false">(</mo><mi>β</mi><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></mrow><annotation encoding="TeX">\omega{(\beta + 1)}</annotation></semantics></math>
is limit and the lengths are increasing, the formula holds for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mrow><mi>β</mi><mo>+</mo><mn>1</mn></mrow><annotation encoding="TeX">\beta + 1</annotation></semantics></math>:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mrow><mo stretchy="false">(</mo><mi>β</mi><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></mrow></msub><mo>=</mo><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>ω</mi></mrow></msub><mo>=</mo><mrow><munder><mo lspace="0em" rspace="0em">sup</mo><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></munder><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi><mo>+</mo><mi>n</mi></mrow></msub></mrow><mo>=</mo><mrow><munder><mo lspace="0em" rspace="0em">sup</mo><mrow><mi>n</mi><mo>&lt;</mo><mi>ω</mi></mrow></munder><mrow><mo stretchy="false">(</mo><msup><mi>ω</mi><mi>β</mi></msup><msup><mn>2</mn><mi>n</mi></msup><mo>+</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></mrow><mo>=</mo><msup><mi>ω</mi><mrow><mi>β</mi><mo>+</mo><mn>1</mn></mrow></msup></mrow><annotation encoding="TeX">L_{\omega {(\beta + 1)}} =
L_{\omega\beta + \omega} = {\sup_{n &lt; \omega} L_{\omega \beta + n}} =
{\sup_{n &lt; \omega} {(\omega^\beta 2^n + n)} } = \omega^{\beta+1}</annotation></semantics></math></p>

<p>Finally, if the formula holds for all <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>β</mi><annotation encoding="TeX">\beta</annotation></semantics></math> below a limit ordinal <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>λ</mi><annotation encoding="TeX">\lambda</annotation></semantics></math> then because the lengths are increasing the formula holds for <math xmlns="http://www.w3.org/1998/Math/MathML"><semantics><mi>λ</mi><annotation encoding="TeX">\lambda</annotation></semantics></math> too:</p>

<p><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><semantics><mrow><msub><mi>L</mi><mrow><mi>ω</mi><mi>λ</mi></mrow></msub><mo>=</mo><mrow><munder><mo lspace="0em" rspace="0em">sup</mo><mrow><mi>β</mi><mo>&lt;</mo><mi>λ</mi></mrow></munder><msub><mi>L</mi><mrow><mi>ω</mi><mi>β</mi></mrow></msub></mrow><mo>=</mo><mrow><munder><mo lspace="0em" rspace="0em">sup</mo><mrow><mi>β</mi><mo>&lt;</mo><mi>λ</mi></mrow></munder><msup><mi>ω</mi><mi>β</mi></msup></mrow><mo>=</mo><msup><mi>ω</mi><mi>λ</mi></msup></mrow><annotation encoding="TeX">L_{\omega \lambda} =
{\sup_{\beta &lt; \lambda} L_{\omega \beta}} =
{\sup_{\beta &lt; \lambda} \omega^{\beta}} = \omega^{\lambda}</annotation></semantics></math></p>

<p>Q.E.D.</p>

<div style="border: 1px dashed black; padding: .5em; margin: 1em">
Sorry, no JavaScript program to calculate these infinite strings 😇...
</div>


{% endraw %}
