---
layout: post
title: "STIX Two in Gecko and WebKit"
tags: fonts mathml webkit mozilla
---

{% raw %}

  <p>On the 1st of December, the <a href="http://stixfonts.org/">STIX Fonts project</a>
announced the release of STIX 2. If you never heard about this project, it is
described <a href="http://stixfonts.org/abt_geninfo.html">as follows</a>:</p>

<blockquote>
  <p>The mission of the Scientific and Technical Information Exchange (STIX) font creation project is the preparation of a comprehensive set of fonts that serve the scientific and engineering community in the process from manuscript creation through final publication, both in electronic and print formats.</p>
</blockquote>

<p>This sounds a very exciting goal but the way it has been achieved has
made the STIX project infamous for its
<a href="https://en.wikipedia.org/wiki/STIX_Fonts_project#Development_process">numerous delays</a>,
for its <a href="https://sourceforge.net/p/stixfonts/tracking/2/">poor</a> or
<a href="https://sourceforge.net/p/stixfonts/tracking/45/">confusing</a> packaging,
for delivering math fonts with
<a href="https://sourceforge.net/p/stixfonts/tracking/59/">too</a>
<a href="https://sourceforge.net/p/stixfonts/tracking/49/">many</a>
<a href="https://sourceforge.net/p/stixfonts/tracking/33/">bugs</a> to be usable,
for its lack of
openness &amp; <a href="https://sourceforge.net/p/stixfonts/tracking/74/">communication</a>,
for its bad handling of third-party
feedback &amp; <a href="https://github.com/khaledhosny/xits-math">contribution</a>…</p>

<p>Because of these laborious travels towards unsatisfactory releases, some
snarky people claim that the project was actually named after
<em>Styx</em> (<a href="https://en.wiktionary.org/wiki/%CE%A3%CF%84%CF%8D%CE%BE">Στύξ</a>)
the river from Greek mythology that one has to cross to enter the Underworld.
Or that the <a href="http://stixfonts.org/proj_timeline.html">story of the project</a>
is summarized by Baudelaire’s verses from
<a href="http://fleursdumal.org/poem/163">L’Irrémédiable</a>:</p>

<div lang="fr">
<blockquote>
Une Idée, une Forme, un Être<br />
Parti de l’azur et tombé<br />
Dans un Styx bourbeux et plombé<br />
Où nul œil du Ciel ne pénètre ;<br />
</blockquote>
</div>

<p>More seriously, the good news is that the STIX
Consortium <em>finally</em> released text fonts with a beautiful design and a
companion math font that is usable in math rendering engines such as
Word Processors, LaTeX and Web Engines. Indeed,
WebKit and Gecko have supported OpenType-based MathML layout for more
than three years (with
<a href="https://frederic-wang.fr/mathml-improvements-in-webkit.html">recent</a>
<a href="https://frederic-wang.fr/fonts-at-the-web-engines-hackfest-2016.html">improvements</a> by Igalia) and STIX Two now has correct OpenType data and metrics!</p>

<p>Of course, the STIX Consortium did not
address all the technical or organizational issues
that have made its reputation but I count on
<a href="https://twitter.com/KhaledGhetas">Khaled Hosny</a> to maintain
his more open <a href="https://github.com/khaledhosny/xits-math">XITS fork</a>
with enhancements that have been ignored for STIX Two
(e.g. Arabic and RTL features) or
with fixes of
<a href="https://sourceforge.net/p/stixfonts/tracking/milestone/Release%202.0.0/">already reported bugs</a>.</p>

<p>As <a href="https://en.wikipedia.org/wiki/Jacques_Distler">Jacques Distler</a> wrote in a <a href="https://golem.ph.utexas.edu/~distler/blog/archives/002926.html#MMLf1">recent blog post</a>,
OS vendors should ideally bundle the STIX Two fonts in their default
installation. For now, users can
<a href="http://sourceforge.net/projects/stixfonts/files/Current%20Release/STIXv2.0.0.zip/download">download</a> and install the OTF fonts themselves.
Note however that the STIX Two archive contains WOFF and WOFF2 fonts that page
authors can <a href="https://fred-wang.github.io/MathFonts/">use as web fonts</a>.</p>

<p>I just landed patches in <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1322743">Gecko</a>
and <a href="https://bugs.webkit.org/show_bug.cgi?id=165676">WebKit</a> so that future
releases will
try and find STIX Two on your system for MathML rendering. However, you
can already do the proper font configuration via the preference
menu of your browser:</p>
<ul>
  <li>For Gecko-based applications (e.g. Firefox, Seamonkey or Thunderbird),
go to the font preference and select <code class="language-plaintext highlighter-rouge">STIX Two Math</code> as the
“font for mathematics”.</li>
  <li>For WebKit-based applications (e.g. Epiphany or Safari)
add the following rule to your user stylesheet:
<code class="language-plaintext highlighter-rouge">math { font-family: "STIX Two Math"; }</code>.</li>
</ul>

<p>Finally, here is a screenshot of MathML formulas rendered by
<a href="https://www.mozilla.org/en-US/firefox/">Firefox</a> 49 using STIX Two:</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/stix-two-firefox-49.png"><img width="500" src="https://frederic-wang.fr/images/stix-two-firefox-49.png" alt="Screenshot of MathML formulas rendered by Firefox using STIX 2" /></a>
  <small></small>
</div>

<p>And the same page rendered by
<a href="https://wiki.gnome.org/Apps/Web/">Epiphany</a> 3.22.3:</p>

<div style="text-align: center; width: 500px; margin-left: auto; margin-right: auto;">
  <a href="https://frederic-wang.fr/images/stix-two-epiphany-3.22.3.png"><img width="500" src="https://frederic-wang.fr/images/stix-two-epiphany-3.22.3.png" alt="Screenshot of MathML formulas rendered by Epiphany using STIX 2" /></a>
</div>

{% endraw %}
