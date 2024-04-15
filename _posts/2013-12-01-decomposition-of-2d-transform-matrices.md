---
layout: post
title: "Decomposition of 2D-transform matrices"
tags: maths css mozilla chromium
---

{% raw %}

  
<script type="text/javascript">
       var TransformName = null;
       var CSSdecomposition, SVGdecomposition, MatrixDecomposition;

       function initTransformName()
       {
          // Initialize TransformName with the appropriate CSS property name.
          if (TransformName) return true;
          var test = document.getElementById("test");

          var nameList = ["transform", "-moz-transform", "-webkit-transform",
                          "-o-transform"];
          for (var i in nameList) {
            TransformName = nameList[i];
            if (getComputedStyle(test)[TransformName] === "none") return true;
          }

          return false;
       }

       function radToDeg(a)
       {
         // Radian to degree.
         return 180 * a / Math.PI;
       }

       function mn(x)
       {
         // MathML Number.
         if (x < 0)
           return "<mrow><mo>&#x2212;</mo><mn>"+Math.abs(x)+"</mn></mrow>";
         return "<mn>"+x+"</mn>";
       }

       function trig(func, arg)
       {
         // MathML trigonometric function.
         return "<mrow><mi>"+func+"</mi><mo>&#x2061;</mo><mrow><mo>(</mo>"+
                mn(arg / Math.PI)+"<mi>&#x3c0;</mi><mo>)</mo></mrow></mrow>";
       }

       function matrix(a, b, c, d, e, f)
       {
         // MathML 2D matrix.
         return "<mrow><mo>(</mo><mtable><mtr><mtd>"+a+"</mtd><mtd>"+c+"</mtd><mtd>"+e+"</mtd></mtr><mtr><mtd>"+b+"</mtd><mtd>"+d+"</mtd><mtd>"+f+"</mtd></mtr><mtr><mtd><mn>0</mn></mtd><mtd><mn>0</mn></mtd><mtd><mn>1</mn></mtd></mtr></mtable><mo>)</mo></mrow>"
       }

       function newTranslate(tx, ty)
       {
         // Add a translate.
         if (tx == 0 && ty == 0) return;
         MatrixDecomposition +=
           matrix(mn(1), mn(0), mn(0), mn(1), mn(tx), mn(ty));
         if (ty == 0) {
           SVGdecomposition += "translate(" + tx + ") ";
           CSSdecomposition += "translate(" + tx + "px) ";
         } else {
           SVGdecomposition += "translate(" + tx + ", " + ty + ") ";
           CSSdecomposition += "translate(" + tx + "px, " + ty + "px) ";
         }
       }

       function newScale(sx, sy)
       {
         // Add a scale.
         if (sx == 1 && sy == 1) return;
         MatrixDecomposition +=
           matrix(mn(sx), mn(0),
                  mn(0), mn(sy), mn(0), mn(0));
         var s = "scale(" + sx + (sx == sy ? "" : "," + sy) + ") ";
         SVGdecomposition += s;
         CSSdecomposition += s;
       }

       function newRotate(a)
       {
         // Add a rotation.
         if (a == 0) return "";
         MatrixDecomposition +=
             matrix(trig("cos", a), trig("sin", a),
                    trig("sin", -a), trig("cos", a), mn(0), mn(0));
         a = radToDeg(a);
         SVGdecomposition += "rotate(" + a + ") ";
         CSSdecomposition += "rotate(" + a + "deg) ";
       }

       function newSkewX(a)
       {
         // Add a skewX.
         if (a == 0) return;
         MatrixDecomposition +=
           matrix(mn(1), mn(0),
                  trig("tan", a), mn(1), mn(0), mn(0), mn(0));
         a = radToDeg(a);
         SVGdecomposition += "skewX(" + a + ") ";
         CSSdecomposition += "skewX(" + a + "deg) ";
       }

       function newSkewY(a)
       {
         // Add a skewY.
         if (a == 0) return;
         MatrixDecomposition +=
           matrix(mn(1), trig("tan", a),
                  mn(0), mn(1), mn(0), mn(0), mn(0));
         a = radToDeg(a);
         SVGdecomposition += "skewY(" + a + ") ";
         CSSdecomposition += "skewY(" + a + "deg) ";
       }
 
       function decompose()
       {
         // Verify if a CSS transform is available.
         if (!initTransformName())
           throw "Your browser does not support CSS transforms."

         // Apply the transform specified by the user.
         var cssRect1 = document.getElementById("cssRect1");
         var CSS2Dtransform = document.getElementById("CSS2Dtransform").value;
         cssRect1.style[TransformName] = "none";
         cssRect1.style[TransformName] = CSS2Dtransform;
         
         // Get the matrix computed by the rendering engine.
         var CSS2Dmatrix = getComputedStyle(cssRect1)[TransformName];
         var regexp = /matrix\((.*),(.*),(.*),(.*),(.*),(.*)\)/;
         var match = regexp.exec(CSS2Dmatrix);
         if (match === null)
            throw "Syntax Error. Please enter a valid CSS 2D transform."
         var a = parseFloat(match[1]);
         var b = parseFloat(match[2]);
         var c = parseFloat(match[3]);
         var d = parseFloat(match[4]);
         var e = parseFloat(match[5]);
         var f = parseFloat(match[6]);
         document.getElementById("CSS2Dmatrix").innerHTML = CSS2Dmatrix;
         document.getElementById("CSS2DmatrixMathML").innerHTML =
           "<math display='block'>" + 
           matrix(mn(a), mn(b), mn(c), mn(d), mn(e), mn(f)) + "</math>"

         // Apply the decomposition algorithm.
         CSSdecomposition = ""; SVGdecomposition = ""; MatrixDecomposition = "";
         newTranslate(e, f);

         var Delta = a * d - b * c;

         if (document.getElementById("decompo").value == "QR-like") {
           // Apply the QR-like decomposition.
           if (a != 0 || b != 0) {
             var r = Math.sqrt(a*a+b*b);
             newRotate(b > 0 ? Math.acos(a/r) : -Math.acos(a/r));
             newScale(r, Delta/r);
             newSkewX(Math.atan((a*c+b*d)/(r*r)));
           } else if (c != 0 || d != 0) {
             var s = Math.sqrt(c*c+d*d);
             newRotate(Math.PI/2 - (d > 0 ? Math.acos(-c/s) : -Math.acos(c/s)));
             newScale(Delta/s, s);
             newSkewY(Math.atan((a*c+b*d)/(s*s)));
           } else { // a = b = c = d = 0
             newScale(0, 0);
           }
         } else {
           // Apply the LU-like decomposition.
           if (a != 0) {
             newSkewY(Math.atan(b/a));
             newScale(a, Delta/a);
             newSkewX(Math.atan(c/a));
           } else if (b != 0) {
             newRotate(Math.PI / 2);
             newScale(b, Delta/b);
             newSkewX(Math.atan(d/b));
           } else { // a = b = 0
             newScale(c, d);
             newSkewX(Math.PI/4);
             newScale(0, 1);
           }
         }

         // Display something if the transform is the identity.
         if (MatrixDecomposition === "") {
           MatrixDecomposition =
             matrix(mn(1), mn(0), mn(0), mn(1), mn(0), mn(0));
           CSSdecomposition = SVGdecomposition = "scale(1)";
         }

         // Display the result.
         document.getElementById("SVGdecomposition").innerHTML =
           SVGdecomposition;
         document.getElementById("CSSdecomposition").innerHTML =
           CSSdecomposition;
         document.getElementById("MatrixDecomposition").innerHTML =
           "<math display='block'>"+MatrixDecomposition+"</math>"

         // Apply the (decomposed) transformation to the SVG and CSS elements.
         document.getElementById("svgRect").
           setAttribute("transform", SVGdecomposition);
         cssRect2.style[TransformName] = CSSdecomposition;
       }

       function run()
       {
         var error = document.getElementById("error");
         try {
           error.innerHTML = "";
           decompose();
         } catch (e) {
           error.innerHTML = e;
         }
       }

       function update(v)
       {
          if (v === "") return;
          document.getElementById("CSS2Dtransform").value = v;
          run();
       }
    </script>

<p>I recently took a look at the description of the CSS 2D / SVG transform <code>matrix(a, b, c, d, e, f)</code> on MDN and I added a <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/transform#General_Transformation">concrete example</a> showing the effect of such a transform on an SVG line, in order to make this clearer for people who are not familiar with affine transformations or matrices.</p>

<div id="test" style="transform: none; -moz-transform: none; -webkit-transform: none; -o-transform: none;"> </div>

<p>This also recalled me a small algorithm to decompose an arbitrary SVG transform into a composition of basic transforms (Scale, Rotate, Translate and Skew) that I wrote 5 years ago for the Amaya SVG editor. I translated it into Javascript and I make it available here. Feel free to copy it on MDN or anywhere else. The convention used to represent transforms as 3-by-3 matrices is the one of the <a href="http://www.w3.org/TR/SVG/coords.html#TransformMatrixDefined">SVG specification</a>.</p>

<h2>Live demo</h2>

<p>Enter the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/transform#CSS_transform_functions">CSS 2D transform</a> you want to reduce and decompose or pick one example from the list <select id="examples" onchange="update(this.value);"><option selected="selected" value="">-- select a transform --</option><option value="matrix(1, 0, 0, 1, -40, 0)">Translate 1</option><option value="matrix(1, 0, 0, 1, 20, -30)">Translate 2</option><option value="matrix(-2, 0, 0, 1, 0, 0)">Scale 1</option><option value="matrix(1, 0, 0, .5, 0, 0)">Scale 2</option><option value="matrix(1.5, 0, 0, 1.5, 0, 0)">Scale 3</option><option value="matrix(.75, 0, 0, -1.5, 0, 0)">Scale 4</option><option value="matrix(0, 1, -1, 0, 0, 0)">Rotate 1</option><option value="matrix(0.7071067811865476, -0.7071067811865475, 0.7071067811865475, 0.7071067811865476, 0, 0)">Rotate 2</option><option value="matrix(0.5000000000000001, 0.8660254037844386, -0.8660254037844386, 0.5000000000000001, -15.98076211353316, -32.320508075688764)">Rotate 3</option><option value="matrix(1, 1, 0, 1, 0, 0)">Skew 1</option><option value="matrix(1, 0, -1, 1, 0, 0)">Skew 2</option><option value="matrix(15, 3, 10, 2, 40, -5)">NonInvertible</option><option value="matrix(.5, 0, 0, 1.5, 30, -20)">Example 1</option><option value="matrix(0, .75, 1.5, 0, 10, 15)">Example 2</option><option value="matrix(0.5, -1, 1, 0.5, 10, -20)">Example 3</option><option value="matrix(1, .25, -.125, 2, 20, 5)">Example 4</option><option value="matrix(1, -.125, .25, 2, 10, 0)">Example 5</option><option value="matrix(1, 0.17632698070846498, 0.36397023426620234, 1.064177772475912, 0, 0)">Example 6</option><option value="matrix(0, .5, -1, 1, 10, 5)">Example 7</option><option value="translate(25px,60px) skewX(20deg) matrix(1,3,.5,.2,1,6) rotate(20deg) translate(-20px,5px) scale(.5, .75)">Complex 1</option><option value="scale(1,-1) translate(5px,-50px) scale(1,.6) rotate(30deg) scale(.5,1) matrix(2, -.3, .7, 1,90, 20) translate(-17px,33px) skewX(30deg) matrix(1,2,3,4,5,6) skewX(-67deg)">Complex 2</option><option value="scale(.5,.8) translate(20px,-10px) matrix(-4, 2, 3, -1, -3, 17) matrix(1, 2, 3, 4, 5, 6)">Complex 3</option><option value="translate(50px,-10px) scaleX(1.1) matrix(0.819152, 0.573576, -0.573576, 0.819152, -20, 15) translateX(-20px) scaleY(.8) rotate(20deg) translateY(15px) scale(1.5,1.1)">Complex 4</option> </select>. You can also choose between LU-like or QR-like decomposition: <select id="decompo" onchange="run();"><option selected="selected" value="QR-like">QR-like</option><option value="LU-like">LU-like</option> </select>.</p>

<div><input id="CSS2Dtransform" onchange="run()" size="50" type="text" value="matrix(1, 0, 0, 1, 0, 0)" /><button onclick="run()">Reduce and Decompose</button></div>

<div> </div>

<div style="width: 200px; height: 200px; background: red; margin: auto;">
<div style="transform: translate(50px, 50px);
                  -moz-transform: translate(50px, 50px);
                  -webkit-transform: translate(50px, 50px);
                  -o-transform: translate(50px, 50px);
                  width: 100px; height: 100px;
                  transform-origin: 50px, 50px;
                  -moz-transform-origin: translate(50px, 50px);
                  -webkit-transform-origin: translate(50px, 50px);
                  -o-transform-origin: translate(50px, 50px);">
<div id="cssRect1">
<div style="width: 100px; height: 100px; background: blue;"><span style="font-size: 40px; color: #ff0;">CSS</span></div>
</div>
</div>
</div>

<p>Here is the reduced CSS/SVG matrix as computed by your rendering engine <strong id="CSS2Dmatrix">?</strong> and its matrix representation:</p>

<p id="CSS2DmatrixMathML"> </p>

<p>After simplification (and modulo rounding errors), an SVG decomposition into simple transformations is <strong id="SVGdecomposition">?</strong> and it renders like this:</p>

<div style="width: 200px; height: 200px; background: red; margin: auto;"><svg height="200px" width="200px"> <g transform="translate(100,100)"> <g id="svgRect"> <g transform="translate(-50,-50)"> <rect fill="blue" height="100px" stroke="none" width="100px"></rect> <text style="font-size: 40px; fill: #ff0;" y="40">SVG</text> </g> </g> </g> </svg></div>

<p>After simplification (and modulo rounding errors), a CSS decomposition into simple transformations is <strong id="CSSdecomposition">?</strong> and it renders like this:</p>

<div style="width: 200px; height: 200px; background: red; margin: auto;">
<div style="transform: translate(50px, 50px);
                  -moz-transform: translate(50px, 50px);
                  -webkit-transform: translate(50px, 50px);
                  -o-transform: translate(50px, 50px);
                  width: 100px; height: 100px;
                  transform-origin: 50px, 50px;
                  -moz-transform-origin: translate(50px, 50px);
                  -webkit-transform-origin: translate(50px, 50px);
                  -o-transform-origin: translate(50px, 50px);">
<div id="cssRect2">
<div style="width: 100px; height: 100px; background: blue;"><span style="font-size: 40px; color: #ff0;">CSS</span></div>
</div>
</div>
</div>

<p>A matrix decomposition of the original transform is:</p>

<div id="MatrixDecomposition"> </div>

<p> </p>

<h2>Mathematical Description</h2>

<p>The decomposition algorithm is based on the classical <a href="https://en.wikipedia.org/wiki/LU_decomposition">LU</a> and <a href="https://en.wikipedia.org/wiki/QR_decomposition">QR</a> decompositions. First remember the SVG specification: the transform <code>matrix(a,b,c,d,e,f)</code> is represented by the matrix</p>
<math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd> <mtd><mi>e</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd> <mtd><mi>f</mi></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mn>0</mn></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math>

<p> </p>

<p>and corresponds to the affine transformation</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>x</mi></mtd></mtr> <mtr><mtd><mi>y</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>↦</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>x</mi></mtd></mtr> <mtr><mtd><mi>y</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>+</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>e</mi></mtd></mtr> <mtr><mtd><mi>f</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math></p>

<p>which shows the classical factorization into a composition of a linear transformation <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math> and a translation <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>e</mi></mtd></mtr> <mtr><mtd><mi>f</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math>. Now let's focus on the matrix <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math> and denote <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>Δ</mi><mo>=</mo><mi>a</mi><mi>d</mi><mo>−</mo><mi>b</mi><mi>c</mi></math> its determinant. We first consider the LDU decomposition. If <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>a</mi><mo>≠</mo><mn>0</mn></math>, we can use it as a pivot and apply one step of Gaussian's elimination:</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>1</mn></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>b</mi><mo stretchy="false">/</mo><mi>a</mi></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>Δ</mi><mo stretchy="false">/</mo><mi>a</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math></p>

<p>and thus the LDU decomposition is</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>1</mn></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mi>b</mi><mo stretchy="false">/</mo><mi>a</mi></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>Δ</mi><mo stretchy="false">/</mo><mi>a</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>1</mn></mtd> <mtd><mi>c</mi><mo stretchy="false">/</mo><mi>a</mi></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math></p>

<p>Hence if <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>a</mi><mo>≠</mo><mn>0</mn></math>, the transform <code>matrix(a,b,c,d,e,f)</code> can be written <code>translate(e,f) skewY(atan(b/a)) scale(a, Δ/a) skewX(c/a)</code>. If <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>a</mi><mo>=</mo><mn>0</mn></math> and <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>b</mi><mo>≠</mo><mn>0</mn></math> then we have <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>Δ</mi><mo>=</mo><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>c</mi><mi>b</mi></math> and we can write (this is approximately "LU with full pivoting"):</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>0</mn></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>0</mn></mtd> <mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mn>1</mn></mtd></mtr> <mtr><mtd><mn>1</mn></mtd> <mtd><mn>0</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>c</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>cos</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd> <mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>sin</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd></mtr> <mtr><mtd><mi>sin</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd> <mtd><mi>cos</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>b</mi></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>Δ</mi><mo stretchy="false">/</mo><mi>b</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>1</mn></mtd> <mtd><mi>d</mi><mo stretchy="false">/</mo><mi>b</mi></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math></p>

<p>and so the transform becomes <code>translate(e,f) rotate(90°) scale(b, Δ/b) skewX(d/b)</code>. Finally, if <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>a</mi><mo>=</mo><mi>b</mi><mo>=</mo><mn>0</mn></math>, then we already have an LU decomposition and we can just write</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>0</mn></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>c</mi></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>1</mn></mtd> <mtd><mn>1</mn></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>0</mn></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math></p>

<p>and so the transform is <code>translate(e,f) scale(c, d) skewX(45°) scale(0, 1)</code>.</p>

<p> </p>

<p>As a consequence, we have proved that any transform <code>matrix(a,b,c,d,e,f)</code> can be decomposed into a product of simple transforms. However, the decomposition is not always what we want, for example <code>scale(2) rotate(30°)</code> will be decomposed into a product that involves <code>skewX</code> and <code>skewY</code> instead of preserving the nice factors.</p>

<p> </p>

<p>We thus consider instead the QR decomposition. If <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>Δ</mi><mo>≠</mo><mn>0</mn></math>, then by applying the Gram–Schmidt process to the columns <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>,</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math> we obtain</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi><mo stretchy="false">/</mo><mi>r</mi></mtd> <mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>b</mi><mo stretchy="false">/</mo><mi>r</mi></mtd></mtr> <mtr><mtd><mi>b</mi><mo stretchy="false">/</mo><mi>r</mi></mtd> <mtd><mi>a</mi><mo stretchy="false">/</mo><mi>r</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>r</mi></mtd> <mtd><mo stretchy="false">(</mo><mi>a</mi><mi>c</mi><mo>+</mo><mi>b</mi><mi>d</mi><mo stretchy="false">)</mo><mo stretchy="false">/</mo><mi>r</mi></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>Δ</mi><mo stretchy="false">/</mo><mi>r</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi><mo stretchy="false">/</mo><mi>r</mi></mtd> <mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>b</mi><mo stretchy="false">/</mo><mi>r</mi></mtd></mtr> <mtr><mtd><mi>b</mi><mo stretchy="false">/</mo><mi>r</mi></mtd> <mtd><mi>a</mi><mo stretchy="false">/</mo><mi>r</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>r</mi></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>Δ</mi><mo stretchy="false">/</mo><mi>r</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>1</mn></mtd> <mtd><mo stretchy="false">(</mo><mi>a</mi><mi>c</mi><mo>+</mo><mi>b</mi><mi>d</mi><mo stretchy="false">)</mo><mo stretchy="false">/</mo><msup><mi>r</mi> <mn>2</mn></msup></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math></p>

<p>where <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>r</mi><mo>=</mo><msqrt><mrow><msup><mi>a</mi> <mn>2</mn></msup><mo>+</mo><msup><mi>b</mi> <mn>2</mn></msup></mrow></msqrt><mo>≠</mo><mn>0</mn></math>. In that case, the transform becomes <code>translate(e,f) rotate(sign(b) * acos(a/r)) scale(r, Δ/r) skewX(atan((a c + b d)/r^2))</code>. In particular, a similarity transform preserves orthogonality and length ratio and so <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>a</mi><mi>c</mi><mo>+</mo><mi>b</mi><mi>d</mi><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>⋅</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mn>0</mn></math> and <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>Δ</mi><mo>=</mo><mrow><mo>∥</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>∥</mo></mrow><mrow><mo>∣</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>∥</mo></mrow><mi>cos</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo><mo>=</mo><msup><mi>r</mi> <mn>2</mn></msup></math>. Hence for a similarity transform we get <code>translate(e,f) rotate(sign(b) * acos(a/r)) scale(r)</code> as wanted. We also note that it is enough to assume the weaker hypothesis <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>r</mi><mo>≠</mo><mn>0</mn></math> (that is <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>a</mi><mo>≠</mo><mn>0</mn></math> or <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>b</mi><mo>≠</mo><mn>0</mn></math>) in the expression above and so the decomposition applies in that case too. Similarly, if we let <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>s</mi><mo>=</mo><msqrt><mrow><msup><mi>c</mi> <mn>2</mn></msup><mo>+</mo><msup><mi>d</mi> <mn>2</mn></msup></mrow></msqrt></math> and instead assume <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>c</mi><mo>≠</mo><mn>0</mn></math> or <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>d</mi><mo>≠</mo><mn>0</mn></math> we get</p>

<p><math display="block" xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>a</mi></mtd> <mtd><mi>c</mi></mtd></mtr> <mtr><mtd><mi>b</mi></mtd> <mtd><mi>d</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mo>=</mo><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>cos</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd> <mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>sin</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd></mtr> <mtr><mtd><mi>sin</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd> <mtd><mi>cos</mi><mo stretchy="false">(</mo><mi>π</mi><mo stretchy="false">/</mo><mn>2</mn><mo stretchy="false">)</mo></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mo>−</mo><mi>c</mi><mo stretchy="false">/</mo><mi>s</mi></mtd> <mtd><mi>d</mi><mo stretchy="false">/</mo><mi>s</mi></mtd></mtr> <mtr><mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>d</mi><mo stretchy="false">/</mo><mi>s</mi></mtd> <mtd><mo lspace="verythinmathspace" rspace="0em">−</mo><mi>c</mi><mo stretchy="false">/</mo><mi>s</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mi>Δ</mi><mo stretchy="false">/</mo><mi>s</mi></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mn>0</mn></mtd> <mtd><mi>s</mi></mtd></mtr></mtable></mrow><mo>)</mo></mrow><mrow><mo>(</mo><mrow><mtable rowspacing="0.5ex"><mtr><mtd><mn>1</mn></mtd> <mtd><mn>0</mn></mtd></mtr> <mtr><mtd><mo stretchy="false">(</mo><mi>a</mi><mi>c</mi><mo>+</mo><mi>b</mi><mi>d</mi><mo stretchy="false">)</mo><mo stretchy="false">/</mo><msup><mi>s</mi> <mn>2</mn></msup></mtd> <mtd><mn>1</mn></mtd></mtr></mtable></mrow><mo>)</mo></mrow></math></p>

<p>Hence in that case the transform is <code>translate(e,f) rotate(90° - sign(d) * acos(-c/s)) scale(Delta/s, s) skewY(atan((a c + b d)/s^2))</code>. Finally if <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>a</mi><mo>=</mo><mi>b</mi><mo>=</mo><mi>c</mi><mo>=</mo><mi>d</mi><mo>=</mo><mn>0</mn></math>, then the transform is just <code>scale(0,0)</code>.</p>

<p id="error"> </p>

<p>The decomposition algorithms are now easy to write. We note that none of them gives the best result in all the cases (compare for example how they factor Rotate2 and Skew1). Also, for completeness we have included the noninvertible transforms in our study (that is <math display="inline" xmlns="http://www.w3.org/1998/Math/MathML"><mi>Δ</mi><mo>=</mo><mn>0</mn></math>) but in practice they are not really useful (try NonInvertible).</p>



{% endraw %}
