---
layout: post
title: "A Zeno paradox to prove the reals are uncountable"
tags: maths
---

{% raw %}

  <h2 id="a-simple-zenos-paradox">A simple Zeno’s paradox</h2>

<p>A simple variant of <a href="https://en.wikipedia.org/wiki/Zeno's_paradoxes">Zeno’s paradoxes</a> can be described as follows. <a href="https://en.wikipedia.org/wiki/Atalanta">Atalanta</a> wishes to walk to the end of a path. When she gets halfway, she still have to walk the remaining half of the path ; When she gets halfway of that remaining half, she still needs to walk the remaining quarter of the path ; When she gets halfway of that remaining quarter, she still needs to walk the remaining eight of the path ; and so on. Hence it seems she will never reach the end of the path, which is paradoxical.</p>

<p><img src="/images/classical_zeno_paradox.svg" style="width: 100%; max-height: 200px;" alt="Schema for classical Zeno's paradox" /></p>

<p>Obviously, this is not true: Atalanta is going to reach the end of the path after a certain amount of time. The issue in the previous reasoning is that (assuming she walks at constant velocity) walking these subpaths also takes her respectively half, a quarter, a eight, etc of the total time she actually needs to arrive to her destination… and the observations are only done for a total time that is less than the one needed.</p>

<h2 id="a-modern-variant">A modern variant</h2>

<p>Now suppose the ground is an infinite <a href="https://en.wikipedia.org/wiki/Real_line">real line</a>, itself covered by an infinite treadmill on which Atalanta is walking. This treadmill brings Atalanta in the opposite direction by twice her velocity. She can decide to turn the treadmill on or off, but its state must remain the same during the whole walk of a subpath. In the following schema, the treadmill was enabled when she was on the second subpath:</p>

<p><img src="/images/modern_zeno_variant.svg" style="width: 100%; max-height: 200px;" alt="Schema for modern variant of Zeno's paradox" /></p>

<p>After the total duration considered in the previous problem, Atalanta has walked exactly the same total distance on the treadmill. The conveyor belt also moves by summing up distances that are twice the distances on subpaths. Because the treadmill can be on or off, the conveyor’s belt position is not following a simple linear function of the time. Let’s admit for a while it still converges to a certain distance when getting closer to the total duration, I will come back to this at the end of the blog post.</p>

<p>With respect to the ground, Atalanta’s position is basically given by her departure position, moved backward by the distance of the conveyor belt with respect to the ground and moved forward by the distance she walked on the treadmill. As a consequence of the previous paragraph, Atalanta is also converging to a destination with respect to the ground.</p>

<h2 id="modern-zenos-paradox-with-a-flaw">Modern Zeno’s paradox (with a flaw)</h2>

<p>Now consider an enumeration of all the points of the real line. At the beginning the treadmill is off. Before walking the first half of the path, Atalanta picks the first point in that enumeration and enables the treadmill if she can see that point in front of her. Before walking the next quarter of the path, she picks the second point and enables or disables the treadmill according to whether she can see that second point in front of her. She continues that way for each subpath and each point of the real line.</p>

<p>When a given point is picked there are two options. Either it is not in front of her and so she will just walk forward to a certain distance ; or otherwise the the treamill will additionnaly take her backward by twice that distance. In any case, with respect to the ground, she is moving away from the picked point by the distance she walks during that subpath.</p>

<p><img src="/images/modern_zeno_variant_picking_a_point.svg" style="width: 100%; max-height: 200px;" alt="Schema for modern variant of Zeno's paradox (picking a point behind or in front of Atalanta)" /></p>

<p>At some step, the point of the real line corresponding to Atalanta’s destination will be picked and she will move away from that destination by a certain distance. But the remaining subpaths are half, a quarter, a eight, etc that distance. To have a chance to converge to the destination again she must now always keep the same direction. But so far, only finitely many points have been picked and so there is at least one point beyond the destination that has not been chosen yet (actually infinitely many). This means she will have to change her direction at least once in the future and so will never be able to reach her destination!</p>

<h2 id="uncountability-of-the-real-line">Uncountability of the real line</h2>

<p>How to solve the paradox in this modern variant?</p>

<p>First, let’s go back to why the distance of the conveyor belt with respect to the ground is convergent. Consider the binary number whose digits describe the sequences of states of the treadmill: 0 if turned off and 1 if turned on. Place the binary point after the first digit to obtain a real number. Then one can check that the distance of the conveyor belt is given by that real number multiplied by Atalanta’s total distance on the treadmill. Of course, one must admit that such a binary number with infinitely many digits after the binary point is well defined!</p>

<p>For a rigorous proof, note that the conveyor belt is always going in the same direction and at most twice Atalanta’s total walking distance on the treadmill. So the convergence of the conveyor belt just comes from the <a href="https://en.wikipedia.org/wiki/Monotone_convergence_theorem">monotone convergence theorem</a>. This assumption was correct.</p>

<p>However, reading more carefully the argumentation, we actually assumed that there is a countable enumeration of all the points of the real line. But Cantor proved at the end of the 19th century that this is wrong, the real line is <a href="https://en.wikipedia.org/wiki/Uncountable_set">uncountable</a>!</p>

<p>It is interesting to actually turn this modern Zeno’s paradox into an apparently “elementary” alternative of <a href="https://en.wikipedia.org/wiki/Cantor's_diagonal_argument">Cantor’s diagonal argument</a>, in a way that involves only concepts understandable by the Ancient Greeks and no advanced mathematical formalisms. In particular, this is not mentioning explicitly the <a href="https://en.wikipedia.org/wiki/Positional_notation">positional notation</a> invented by Indian mathematicians. As a comparison, Cantor’s proof assumes that a decimal notation with infinitely many digits after the decimal point is well defined (similar to what we used for our proof with binary numbers) ; or it must deal with the edge case of a real number with two different decimal notations (e.g. 0.4999999… = 0.5).</p>

<h2 id="for-completeness">For completeness</h2>

<p>Nevertheless, we still had to use some kind of <a href="https://en.wikipedia.org/wiki/Completeness_of_the_real_numbers">completeness property</a> in order to prove that the moving distance of the conveyor belt is convergent. Actually, <a href="https://en.wikipedia.org/wiki/Completeness_of_the_real_numbers#Cauchy_completeness">Cauchy completeness is enough</a>.</p>

<p>It is also interesting to note that all the moves as well as Atalanta’s total distance on the treadmill are rational numbers. Since the rational numbers are countable, this modern Zeno’s paradox can also be performed by considering only rational points on the ground. In that case, the flaw is then in the assumption that the conveyor belt converges to a rational point: <a href="https://en.wikipedia.org/wiki/Construction_of_the_real_numbers#On_the_least_upper_bound_property">the set of rational numbers is not complete</a>.</p>

<p>More generally, we can also applie this modern Zeno’s paradox to any <a href="https://en.wikipedia.org/wiki/Ordered_field">ordered field</a> since they include a subset isomorphic to the rational numbers. The conclusion becomes that if the field is Cauchy-complete then it is uncountable.</p>

{% endraw %}
