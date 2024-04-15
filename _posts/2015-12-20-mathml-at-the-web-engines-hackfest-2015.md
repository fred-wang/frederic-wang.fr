---
layout: post
title: "MathML at the Web Engines Hackfest 2015"
tags: mathml igalia
---

{% raw %}

  <h2 id="hackfest">Hackfest</h2>

<p>Two weeks ago, I travelled to Spain to participate to the second <a href="http://www.webengineshackfest.org/">Web Engines
Hackfest</a> which was sponsored by 
<a href="http://www.igalia.com/">Igalia</a> and <a href="https://www.collabora.com/">Collabora</a>.
Such an event has been organized by Igalia since 2009 and used to be focused on
WebkitGTK+. It is great to see that it has now been extended to any Web engines &amp;
platforms and that a large percentage of non-igalian developers has been
involved this year. If you did not get the opportunity to attend this event
or if you are curious about what happened there, take a look at the
<a href="https://github.com/Igalia/webengineshackfest/wiki">wiki page</a> or
<a href="https://www.flickr.com/photos/webhackfest/sets/72157660108679713/">flickr album</a>.</p>

<div style="width: 500px; margin-left: auto; margin-right: auto; text-align: center;">
<a href="https://www.flickr.com/photos/webhackfest/23662778162/in/album-72157660108679713/" title="Last day of the hackfest"><img src="https://farm6.staticflickr.com/5659/23662778162_34eff30b58.jpg" width="500" height="375" alt="Last day of the hackfest" /></a><br />
<small>Photo from <a href="https://www.flickr.com/photos/webhackfest/">@webengineshackfest</a> licensed under
<a href="http://creativecommons.org/licenses/by-sa/2.0/">
<img alt="Creative Commons Attribution-ShareAlike" src="https://i.creativecommons.org/l/by-sa/2.0/80x15.png" style="border: 0;" /></a></small></div>

<p>I really like this kind of hacking-oriented and participant-driven event where developers can meet face to face, organize themselves in small collaboration
groups to efficiently make progress on a task or give passionate talk about
what they have recently been working on.
The only small bemol I have is that it is still mainly focused on WebKit/Blink
developments. Probably, the lack of Mozilla/Microsoft participants is
probably due to
<a href="https://wiki.mozilla.org/Coincidental_work_weeks/2014_Portland">Mozilla Coincidental</a>
<a href="https://wiki.mozilla.org/Coincidental_work_weeks/2015_Orlando">Work Weeks</a>
happening at the same period and to the proprietary nature of
<a href="https://blogs.windows.com/msedgedev/tag/edgehtml/">EdgeHTML</a>
(although <a href="https://blogs.windows.com/msedgedev/2015/12/05/open-source-chakra-core/">this is changing</a>?). However, I am
confident that Igalia will try and address this issue and I am looking
forward to coming back next year!</p>

<h2 id="mathml-developments">MathML developments</h2>

<p>This year, Igalia developer <a href="http://www.igalia.com/nc/igalia-247/igalian/item/alex/">Alejandro G. Castro</a> wanted to work with me on WebKit’s MathML layout code and more specifically on his <a href="https://github.com/alexgcastro/webkit/tree/MathMLLayout">MathML refactoring branch</a>. Indeed, as many people (including Google developers) who have tried to work on WebKit’s code in the past, he arrived to the conclusion that the WebKit’s MathML layout code has many design issues that make it a burden for the rest of the layout team and too complex to allow future improvements. I was quite excited about the work he has done with <a href="http://www.igalia.com/nc/igalia-247/igalian/item/jfernandez/">Javier Fernández</a> to try and move to a simple box model closer to what exists in Gecko and thus I actually extended my stay to work one whole week with them. We already submitted 
<a href="https://lists.webkit.org/pipermail/webkit-dev/2015-December/027840.html">our proposal to the webkit-dev mailing list</a> and received positive feedback, so we
will now start merging what is ready.
At the end of the week, we were quite satisfied about the new approach and confident it will facilitate future maintenance and developements :-)</p>

<div style="width: 500px; margin-left: auto; margin-right: auto; text-align: center;">
<a href="https://www.flickr.com/photos/webhackfest/23403316889/" title="Main room"><img src="https://farm1.staticflickr.com/709/23403316889_a32cffd144.jpg" width="500" height="375" alt="Main room" /></a><br />
<small>Photo from <a href="https://www.flickr.com/photos/webhackfest/">@webengineshackfest</a> licensed under
<a href="http://creativecommons.org/licenses/by-sa/2.0/">
<img alt="Creative Commons Attribution-ShareAlike" src="https://i.creativecommons.org/l/by-sa/2.0/80x15.png" style="border: 0;" /></a></small></div>

<p>While reading a <a href="https://lists.w3.org/Archives/Public/www-math/2015Dec/0000.html">recent thread on the Math WG mailing list</a>, I realized that many MathML people have only vague understanding of why Google (or to be more accurate, the 3 or 4 engineers who really spent some time reviewing and testing the WebKit code) considered the implementation to be unsafe and not ready for release. Even worse, 
<a href="https://kwarc.info/people/mkohlhase">Michael Kholhase</a> pointed out that for someone totally ignorant of the technical implementation details, the communication made some years ago around the “flexbox-based approach” gave the impression that it was “the right way” (indeed, it somewhat did improve the initial implementation) and the rationale to change that approach was not obvious. So let’s just try and give a quick overview of the main problems, even if I doubt someone can have good understanding of the situation without diving into the C++ code:</p>

<ol>
  <li>WebKit’s code to stretch operator was not efficient at all and was limited to
some basic fences buildable via Unicode characters.</li>
  <li>WebKit’s MathML code violated many layout invariants, making the code unreliable.</li>
  <li>WebKit’s MathML code relied heavily on the C++ renderer classes for flexboxes
and has to manage too many anonymous renderers.</li>
</ol>

<p>The main security concerns were addressed a long time ago by <a href="http://www.igalia.com/nc/igalia-247/igalian/item/mrobinson/">Martin Robinson</a> and me. Glyph assembly for stretchy operators are now drawn using low-level font painting primitive instead of creating one renderer object for each piece and the preferred width for them no longer depends on vertical metrics (although we still need some work to obtain Gecko’s good operator spacing). Also, during my <a href="http://www.ulule.com/mathematics-ebooks/">crowdfunding project</a>, I implemented partial support for the <a href="https://www.microsoft.com/typography/otspec/math.htm">OpenType MATH table</a> in WebKit and more specifically the MathVariant subtable, which allows to directly use construction of stretchy operators specified by the font designer and not only the few Unicode constructions.</p>

<p>However, the MathML layout code still modifies the renderer tree to force the presence of anonymous renderers and still applies specific CSS rules to them. It is also spending too much time trying to adapt the parent flexbox renderer class which has at the same time too much features for what is needed for MathML (essentially automatic box alignment) and not enough to get exact placement and measuring needed for high-quality rendering (the TeXBook rules are more complex, taking into account various parameters for box shifts, drops, gaps etc).</p>

<p>During the hackfest, we started to rewrite a clean implementation of some MathML renderer classes similar to Gecko’s one and based on the <a href="http://www.mathml-association.org/MathMLinHTML5/">MathML in HTML5 implementation note</a>.
The code now becomes very simple and understandable. It can be summarized into four main functions. For instance, to draw a fraction we need:</p>

<ul>
  <li><code class="language-plaintext highlighter-rouge">computePreferredLogicalWidths</code> which sets the preferred width of the
fraction during the first layout pass, by considering the widest between numerator and denominator.</li>
  <li><code class="language-plaintext highlighter-rouge">layoutBlock</code> and <code class="language-plaintext highlighter-rouge">firstLineBaseline</code> which calculate the final
width/height/ascent of the fraction element and position the numerator and
denominator.</li>
  <li><code class="language-plaintext highlighter-rouge">paint</code> which draws the fraction bar.</li>
</ul>

<p>Perhaps, the best example to illustrate how the complexity has been reduced 
is the case of the renderer of <code class="language-plaintext highlighter-rouge">mmultiscripts</code>/<code class="language-plaintext highlighter-rouge">msub</code>/<code class="language-plaintext highlighter-rouge">msup</code>/<code class="language-plaintext highlighter-rouge">msubsup</code> elements
(attaching an arbitrary number of subscripts and superscripts before or after a
base). In the current WebKit implementation, we have to create three anonymous wrappers
(a first one for the base, a second one for prescripts and a third one for postscripts) and an anonymous wrapper
for each subscript/superscript pair, add alignment styles for these wrappers
and spend a lot of time
maintaining the integrity of the renderer tree when dynamic changes happen.
With the new code, we just need to do arithmetic calculations to position the
base and script boxes. This is somewhat more complex than the fraction example above but still, it remains arithmetic calculations and we can not reduce any further if we wish quality comparable to TeXBook / MATH rules.
We actually take into account many parameters
from the OpenType MATH table to get much better placement of scripts. We were able to fix <a href="https://bugs.webkit.org/show_bug.cgi?id=130325">bug 130325</a> in about twenty minutes instead of fighting with a CSS “negative margin” hack on anonymous renderers.</p>

<h2 id="mathml-dicussions">MathML dicussions</h2>

<p>The first day of the hackfest we also had an interesting “breakout session” to define the tasks to work on during the hackfest. Alejandro briefly presented the status of his refactoring branch and his plan for the hackfest. As said in the previous section, we have been quite successful in following this plan: Although it is not fully complete yet, we expect to merge the current changes soon. <a href="https://twitter.com/abrax5">Dominik Röttsches</a> who works on Blink’s font and layout modules was present at the MathML session and it was a good opportunity to discuss the future of MathML in Chrome. I gave him some references regarding the OpenType MATH table, math fonts and the <a href="http://www.mathml-association.org/MathMLinHTML5/">MathML in HTML5 implementation note</a>. Dominik said he will forward the references to his colleagues working on layout so that we can have deeper technical dicussion about MathML in Blink in the long term. Also, I mentioned <a href="https://github.com/googlei18n/noto-fonts/issues/330">noto-fonts issue 330</a>, which will be important for math rendering in Android and actually does not depend on the MathML issue, so that’s certainly something we could focus on in the short term.</p>

<div style="width: 500px; margin-left: auto; margin-right: auto; text-align: center;">
<a href="https://www.flickr.com/photos/webhackfest/23144428143/" title="Álex and Fred during the MathML breakout session"><img src="https://farm1.staticflickr.com/775/23144428143_1e0fa79fcc.jpg" width="500" height="375" alt="Álex and Fred during the MathML breakout session" /></a><br />
<small>Photo from <a href="https://www.flickr.com/photos/webhackfest/">@webengineshackfest</a> licensed under
<a href="http://creativecommons.org/licenses/by-sa/2.0/">
<img alt="Creative Commons Attribution-ShareAlike" src="https://i.creativecommons.org/l/by-sa/2.0/80x15.png" style="border: 0;" /></a></small></div>

<p>Alejandro also proposed to me to prepare a talk about <a href="http://www.webengineshackfest.org/slides/mathml-in-web-engines-by-frederic-wang/mathml/">MathML in Web Engines</a> and exciting stuff happening with the <a href="http://mathml-association.org/">MathML Association</a>. I thus gave a brief overview of MathML and presented some demos of native support in Gecko. I also explained how we are trying to start a constructive approach to solve miscommunication between users, spec authors and implementers ; and gather technical and financial resources to obtain a proper solution. In a slightly more technical part, I presented Microsoft’s OpenType MATH table and how it can be used for math rendering (and MathML in particular). Finally, I proposed my personal roadmap for MathML in Web engines. Although I do not believe I am a really great speaker, I received positive feedback from attendees. One of the thing I realized is that I do not know anything about the status and plan in EdgeHTML and so overlooked to mention it in my presentation. Its proprietary nature makes hard for external people to contribute to a MathML implementation and the fact that Microsoft is moving away from ActiveX <i>de facto</i> excludes <a href="http://www.dessci.com/en/products/mathplayer/">third-party plugin for good and fast math rendering</a> in the future. After I went back to Paris, I thus wrote to Microsoft employee <a href="https://www.christianheilmann.com/">Christian Heilmann</a> (previously working for Mozilla), mentioning at least the
<a href="http://www.mathml-association.org/MathMLinHTML5/">MathML in HTML5 Implementation Note</a> and its <a href="http://tests.mathml-association.org/">test suite</a> as a starting point. MathML is currently on the <a href="https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer/filters/top">first page of the most voted feature requested for Microsoft Edge</a> and given the new direction taken with Microsoft Edge,
I hope we could start a discussion on MathML in EdgeHTML…</p>

<h2 id="conclusion">Conclusion</h2>

<p>This was a great hackfest and I’d like to thank again all the participants and sponsors
for making it possible! As Alejandro wrote to me, “I think we have started a very interesting work regarding MathML and web engines in the future.”. The short term plan is now to land the WebKit MathML refactoring started during the hackfest and to finish the work. I hope people now understand the importance of fonts with an OpenType MATH table for good mathematical rendering and we will continue to encourage browser vendors and font designers to make such fonts wide spread.</p>

<p>The new approach for WebKit MathML support gives good reason to be optmimistic
in the long term and we hope we will be able to get high-quality rendering.
The fact that the new approach addresses all the issues formulated by Google and that we started a dialogue on math rendering, gives several options for MathML in Blink. It remains to get Microsoft involved in implementing its own OpenType table in EdgeHTML. Overall, I believe that we can now have a very constructive discussion with the individuals/companies who really want native math support, with the Math WG members willing to have their specification implemented in browsers and with the browser vendors who want a math implementation which is good, clean and compatible with the rest of their code base. Hopefully, the <a href="http://mathml-association.org/">MathML Association</a> will be instrumental in achieving that. If everybody get involved,
2016 will definitely be an exciting year for native MathML in Web engines!</p>

{% endraw %}
