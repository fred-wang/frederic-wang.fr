---
layout: post
title: "BlinkOn 9: Working on the Web Platform from a cooperative"
tags: igalia chromium
---

{% raw %}

  <p>Last week, I attended <a href="https://bit.ly/blinkon9-info">BlinkOn 9</a>. I was very happy to
spend some time with my colleagues working on Chromium, including a new
developer who will join my team next week (to be announced soon!).</p>

<p>This edition had the usual format with presentations, brainstorming,
lightning talks and informal chats with Chromium developers. I attended several
interesting presentations on web platform standardization,
implementation and testing.
It was also great to talk to Googlers in order to coordinate on some of
Igalia’s projects such as
<a href="https://frederic-wang.fr/amp-and-igalia-working-together-to-improve-the-web-platform.html">the collaboration with AMP</a> or
<a href="https://mathml.igalia.com/">MathML in Chromium</a>.</p>

<p>In the previous edition, I realized that one can propose non-technical
talks (e.g. the one about <a href="https://docs.google.com/presentation/d/1gZtzemj6g28G_cxm098m4UjdRCvkadk5oIWHdVZvPUM">inclusion and diversity</a>) and some people seemed
curious about Igalia. Hence I proposed a presentation
“<a href="https://people.igalia.com/fwang/blink-on-9/slides/?showNotes=true">Working on the Web Platform from a Cooperative</a>” that gives:</p>

<ul>
  <li>An introduction to Igalia and its activities.</li>
  <li>A description of our non-hierarchical model and benefits it brings.</li>
  <li>An overview of Igalia’s contribution to the Web Platform.</li>
</ul>

<p><img alt="Presenting my talk in West Sycamore" src="https://frederic-wang.fr/images/blinkon9-igalia-talk.jpg" /></p>

<p>From the feedback I got, people appreciated the presentation and liked to get more
insight on Igalia. Unfortunately, I was not able to record
the talk due to technical issues. Of course, thirty minutes is a bit short to
develop all the ideas and reply properly to all the questions. But for those who
are interested here are more pointers:</p>

<ul>
  <li>
    <p>About “equal salary” VS “cost of living”, you might want to read
Andy Wingo’s blog posts “<a href="https://wingolog.org/archives/2013/06/25/time-for-money">time for money</a>” and “<a href="https://wingolog.org/archives/2016/03/24/a-simple-local-solution-to-the-pay-gap">a simple (local) solution to the pay gap</a>”.
Several years ago, Robert O’Callahan had already wondered
<a href="https://robert.ocallahan.org/2011/08/cost-of-living.html">whether it really made sense to take into account the cost of living to
determine salaries</a>.
Personally, I believe that as long as our “target salary” is high enough
for all places where we work, we don’t really need to worry about this
issue and can instead spend time focusing on more interesting agreements
to keep making Igalia a great working place.</p>
  </li>
  <li>
    <p>About dependency on the customers, see the last
paragraph of “work groups” in Andy’s blog post “<a href="https://wingolog.org/archives/2013/06/13/but-that-would-be-anarchy">but that would be anarchy!</a>” especially
treating customers as partners. As I said during the talk, as long as we
have enough customers we have some freedom to accept contracts that are more
interesting for our strategy and aligned with our values or negociate
improvements to existing contracts ; without worrying about unstability
and uncertainty.</p>
  </li>
  <li>
    <p>About the meaning of “Igalia”, the simple answer is
“it does not mean anything”. If you join Igalia and get the opportunity to
learn about the company history, there is a more complete answer about how
the name was found…</p>
  </li>
  <li>
    <p>Regarding founders of Igalia in 2001: <a href="https://www.igalia.com/nc/igalia-247/igalian/item/dape/">Dape</a> (who attended BlinkOn), <a href="https://www.igalia.com/nc/igalia-247/igalian/item/alex/">Alex</a>, <a href="https://www.igalia.com/nc/igalia-247/igalian/item/juanjo/">Juanjo</a>, <a href="https://www.igalia.com/nc/igalia-247/igalian/item/xavi/">Xavi</a>, <a href="https://www.igalia.com/nc/igalia-247/igalian/item/berto/">Berto</a> and <a href="https://www.igalia.com/nc/igalia-247/igalian/item/chema/">Chema</a> are indeed still
working at Igalia and in general, very few people have left Igalia since its creation.</p>
  </li>
</ul>

<p>Finally we had two related tricky questions from Google employees:</p>

<ul>
  <li>
    <p>How do you sync with the browser vendors’ own agenda?</p>
  </li>
  <li>
    <p>What can Google (or any other browser vendor) could do to facilitate involvements of third-party contributors?</p>
  </li>
</ul>

<p>One could enumerate different situations but unfortunately there is not a
generic answer. In some cases collaboration worked very well and was
quite successful.
In other cases, things were more complicated and we had to “fight” to
convince browser vendors to keep some existing code or accept new features.</p>

<p>Communication is very important. We try to sync with browser vendors using video conferencing or by attending conferences, but some companies/teams are more or less inclined to reveal information (especially when strategic products
are involved). In general, I have the impression that the more the teams work
close to the Web Platform,
the more they are used to the democratic and open-source
culture and welcome third-party contributions.</p>

<p>Although the ideal is to work upstream, we have recently been developing skills
to manage separate forks and rebase them regularly against the main branch. This
is a good option to find a balance between the request of the customer to implement
features and the need of the browser vendors to focus on their own tasks.
<a href="https://github.com/Igalia/chromium/">Chromium for Wayland</a> is a good
example of that approach.</p>

<p>Hence probably one way to help third-party contributors is to improve
communication. We had some issues with developers not even willing to talk to us
or not taking time to review or comment on our patches/CLs. If browser vendors
could indicate that they don’t like an approach as soon as possible or that
they won’t accept patches until some refactoring is complete, that would help
us a lot to discuss with clients, properly schedule our tasks and consider the
option of an experimental branch.</p>

<p>Another way to help third-party contributors would be to advertize more
that such contributions are actually possible. Indeed, many people think that
“everything is implemented by browser vendors” which can make difficult to
find clients for web platform development. When companies rant about Google
not implementing feature X, fixing bug Y or participating to standard Z, instead
of ignoring them or denying the importance of the request, it would probably be
more constructive to mention that they can actually pay consulting companies to
do that job. As I indicated in the talk, we recently had such successful
collaborations with <a href="https://www.bloomberg.com/">Bloomberg</a>,
<a href="https://www.metrological.com/">Metrological</a> or
<a href="https://www.ampproject.org/">AMP</a> and we would be happy to find more!</p>

<p>There are probably more to reply to these questions, but that’s my quick
thought on the matter for now. I’ll try discussing with my
colleagues and see if we have more ideas to share.</p>

{% endraw %}
