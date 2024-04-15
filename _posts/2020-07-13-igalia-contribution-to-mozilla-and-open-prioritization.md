---
layout: post
title: "Igalia's contribution to the Mozilla project and Open Prioritization"
tags: igalia mozilla
---

{% raw %}

  <p>As many web platform developer and Firefox users, I believe <a href="https://www.mozilla.org/en-US/mission/">Mozilla’s mission</a> is instrumental for a better Internet. In a recent <a href="https://www.igalia.com/chats/ecosystem-health">Igalia’s chat about the Web Ecosystem Health</a>, participants made the usual observation regarding this important role played by Mozilla on the one hand and the limited development resources and small Firefox’s usage share on the other hand. In this blog post, I’d like to explain an experimental idea we are launching at Igalia to try and make browser development better match the interest of the web developer and user community.</p>

<div>
  <a href="https://www.igalia.com/open-prioritization/">
    <img src="/images/open-prioritization.png" style="margin-left: auto; margin-right: auto; max-width: 100%; height: auto;" width="750" height="255" alt="Open Prioritization by Igalia. An experiment in crowd-funding prioritization." />
  </a>
</div>

<h2 id="igalias-contribution-to-browser-repositories">Igalia’s contribution to browser repositories</h2>

<p>As mentioned in the past in this blog, Igalia has contributed to different part of Firefox such as multimedia (e.g. &lt;video&gt; support), layout (e.g. Stylo, WebRender, CSS, MathML), scripts (e.g. BigInt, WebAssembly) or accessibility (e.g. ARIA). But is it enough?</p>

<p>Although commit count is an imperfect metric it is also one of the easiest to obtain. Let’s take a look at how Igalia’s commits repositories of the Chromium (chromium, v8), Mozilla (mozilla-central, servo, servo-web-render) and WebKit projects were distributed last year:</p>

<figure>
  <img style="margin-left: auto; margin-right: auto; max-width: 100%; height: auto;" width="374" height="305" src="https://frederic-wang.fr/images/distribution-of-igalia-commits-2019.png" alt="pie chart" />
  <figcaption><small>Diagram showing, the distribution of Igalia's contributions to browser repositories in 2019 (~5200 commits). Chromium (~73%), Mozilla (~4%) and WebKit (~23%).</small>
  </figcaption>
</figure>

<p>As you can see, in absolute value Igalia contributed roughly 3/4 to Chromium, 1/4 to WebKit, with a small remaining amount to Mozilla. This is not surprising since Igalia is a consulting company and our work depends on the importance of browsers in the market where Chromium dominates and WebKit is also quite good for iOS devices and embedded systems.</p>

<p>This suggests a different way to measure our contribution by considering, for each project, the percentage relative to the total amount of commits:</p>

<figure>
  <img style="margin-left: auto; margin-right: auto; max-width: 100%; height: auto" width="436" height="339" src="https://frederic-wang.fr/images/igalia-commit-percentage-per-project-2019.png" alt="Bar graph" />
  <figcaption><small>Diagram showing, for each project, the percentage of Igalia's commits in 2019 relative to the total amount of the project. From left to right:
  Chromium (~3.96%), Mozilla (~0.43%) and WebKit (~10.92%).</small>
  </figcaption>
</figure>

<p>In the WebKit project, where ~80% of the contributions were made by Apple, Igalia was second with ~10% of the total. In the Chromium project, the huge Google team made more than 90% of the contributions and many more companies are involved, but Igalia was second with about 4% of the total. In the Mozilla project, Mozilla is also doing ~90% of the contributions but Igalia only had ~0.5% of the total. Interestingly, the second contributing organization was… the community of unindentified gmail.com addresses! Of course, this shows the importance of volunteers in the Mozilla project where a great effort is done to encourage participation.</p>

<h2 id="open-prioritization">Open Prioritization</h2>

<p>From the commit count, it’s clear Igalia is not contributing as much to the Mozilla project as to Chromium or WebKit projects. But this is expected and is just reflecting the priority set by large companies. The solid base of Firefox users as well as the large amount of volunteer contributors show that the Mozilla project is nevertheless still attractive for many people. Could we turn this into browser development that is not funded by advertising or selling devices?</p>

<p>Another related question is whether the internet can really be shaped by the global community as defended by the Mozilla’s mission? Is the web doomed to be controlled by big corporations doing technology’s “evangelism” or lobbying at standardization committees? Are there prioritization issues that can be addressed by moving to a more collective decision process?</p>

<p>At <a href="https://www.igalia.com/about/">Igalia</a>, we internally try and follow <a href="https://wingolog.org/tags/cooperatives">a more democratic organization</a> and, at our level, intend to make the world a better place. Today, we are launching a new <a href="https://www.igalia.com/open-prioritization/">Open Prioritization</a> experiment to verify whether crowdfunding could be a way to influence how browser development is prioritized. Below is a short (5 min) <a href="https://www.youtube.com/embed/xCRxNVbUqhk">introductory video</a>:</p>

<iframe width="850" height="508" src="https://www.youtube.com/embed/xCRxNVbUqhk" frameborder="0" allowfullscreen=""></iframe>

<p>I strongly recommend you to take a look at the proposed projects and <a href="https://www.igalia.com/open-prioritization/#faq">read the FAQ</a> to understand how this is going to work. But remember <em>this is an experiment</em> so we are starting with a few ideas that we selected and tasks that are relatively small. We know there are tons of user reports in bug trackers and suggestions of standards, but we are not going to solve everything in one day !</p>

<p>If the process is successful, we can consider generalizing this approach, but we need to test it first, check what works and what doesn’t, consider whether it is worth pursuing, analyze how it can be improved, etc</p>

<h2 id="two-crowdfunding-tasks-for-firefox">Two Crowdfunding Tasks for Firefox</h2>

<figure>
  <img style="margin-left: auto; margin-right: auto; max-width: 100%; height: auto" src="https://upload.wikimedia.org/wikipedia/commons/0/06/CIELAB_color_space_top_view.png" alt="CIELAB color space*" />
  <figcaption><small>Representation of the CIELAB color space (top view)
  <a href="https://commons.wikimedia.org/wiki/File:CIELAB_color_space_top_view.png">by Holger Everding, under CC-SA 4.0</a>.</small>
  </figcaption>
</figure>

<p>As explained in the previous paragraph, we are starting with small tasks. For Firefox, we selected the following ones:</p>

<ul>
  <li>
    <p>CSS <code class="language-plaintext highlighter-rouge">lab()</code> colors. This is about giving web developers a way to express colors using the <a href="https://en.wikipedia.org/wiki/CIELAB_color_space">CIELAB color space</a> which approximates better the human perception. My colleague Brian Kardell wrote a <a href="https://bkardell.com/blog/Unlocking-Colors.html">blog with more details</a>. Some investigations have been made by <a href="https://bugs.webkit.org/show_bug.cgi?id=205675">Apple</a> and <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=1026287">Google</a>. Let’s see what we can do for Firefox !</p>
  </li>
  <li>
    <p>SVG path <code class="language-plaintext highlighter-rouge">d</code> attribute. This is about expressing <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1571119">SVG path using the corresponding CSS syntax</a> for example <code class="language-plaintext highlighter-rouge">&lt;path style="d: path('M0,0 L10,10,...')"&gt;</code>. This will likely involve a refactoring to use the same parser for both SVG and CSS paths. It’s a small feature but part of a more general <a href="https://www.youtube.com/watch?v=1d--S_wgAJA">convergence effort between SVG and CSS</a> that Igalia has been involved in.</p>
  </li>
</ul>

<h2 id="conclusion">Conclusion</h2>

<p>Is this crowd-funded experiment going to work? Can this approach solve the prioritization problems or at least help a bit? How can we improve that idea in the future?…</p>

<p>There are many open questions but we will only be able to answer them if we have enough people participating. I’ll personally pledge for the two Firefox projects and I invite you to at least take a look and decide whether there is something there that is interesting for you. Let’s try and see!</p>

{% endraw %}
