---
layout: post
title: "Contributions to Web Platform Interoperability (First Half of 2020)"
tags: igalia
---

{% raw %}

  <p><strong>Note: This blog post was co-authored by AMP and Igalia teams.</strong></p>

<p>Web developers continue to face challenges with web interoperability issues and a lack of implementation of important features. As an open-source project, <a href="https://www.ampproject.org/">the AMP Project</a>  can help represent developers and aid in addressing these challenges.  In the last few years, we have partnered with <a href="https://www.igalia.com/">Igalia</a> to collaborate on helping advance predictability and interoperability among browsers.  Standards and the degree of interoperability that we want can be a long process.  New features frequently require experimentation to get things rolling, course corrections along the way and then, ultimately as more implementations and users begin exploring the space, doing really interesting things and finding issues at the edges we continue to advance interoperability.</p>

<p>Both AMP and Igalia are very pleased to have been able to play important roles at all stages of this process and help drive things forward.  During the first half of this year, here’s what we’ve been up to…</p>

<h2 id="default-aspect-ratio-of-images">Default Aspect Ratio of Images</h2>

<p>In our<a href="https://blog.amp.dev/2019/12/16/our-2019-contributions-to-web-platform-interoperability/"> previous blog post</a> we mentioned our experiment to implement the<a href="https://github.com/WICG/intrinsicsize-attribute"> intrinsic size attribute</a> in WebKit. Although this was a useful prototype for standardization discussions, at the end there was a consensus to switch to an alternative approach. This new approach addresses the same use case without the need of a new attribute. The idea is pretty simple: use specified width and height attributes of an image to determine the default aspect ratio. If additional CSS is used e.g. “width: 100%; height: auto;”, browsers can then compute the final size of the image, without waiting for it to be downloaded. This avoids any relayout that could cause bad user experience. This was implemented in<a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1547231"> Firefox</a> and<a href="https://bugs.chromium.org/p/chromium/issues/detail?id=979891"> Chromium</a> and we did the<a href="https://bugs.webkit.org/show_bug.cgi?id=201641"> same in WebKit</a>. We implemented this under a flag which is currently on by default in Safari Tech Preview and the latest iOS 14 beta.</p>

<h2 id="scrolling">Scrolling</h2>

<p>We continued our efforts to enhance scroll features. In WebKit, we began with<a href="https://bugs.webkit.org/show_bug.cgi?id=188043"> scroll-behavior</a>, which provides the ability to do smooth scrolling. Based on our previous patch, it has landed and is guarded by an experimental flag “CSSOM View Smooth Scrolling” which is disabled by default. Smooth scrolling currently has a generic platform-independent implementation controlled by a timer in the web process, and we continue working on a more efficient alternative relying on the native iOS UI interfaces to perform scrolling.</p>

<p>We have also started to work on overscroll and overscroll customization, especially for the scrollend event. The scrollend event, as you might expect, is fired when the scroll is finished, but it lacked interoperability and required some additional tests. We added web platform tests for<a href="https://github.com/web-platform-tests/wpt/pull/22768"> programmatic scroll</a> and<a href="https://github.com/web-platform-tests/wpt/pull/23753"> user scroll</a> including scrollbar, dragging selection and keyboard scrolling. With these in place, we are now working on a patch in WebKit which supports scrollend for programmatic scroll and Mac user scroll.</p>

<p>On the Chrome side, we continue working on the standard scroll values in non-default writing modes. This is an interesting set of challenges surrounding the scroll API and how it works with writing modes which was previously not entirely interoperable or well defined.  Gaining interoperability requires changes, and we have to be sure that those changes are safe.  Our current changes are implemented and guarded by a runtime flag “CSSOM View Scroll Coordinates”. With the help of Google engineers, we are trying to collect user data to decide whether it is safe to enable it by default.</p>

<p>Another minor interoperability fix that we were involved in was to ensure that the scrolling attribute of frames recognizes values “noscroll” or “off”. That was already the case in Firefox and this is now the case in<a href="https://chromium-review.googlesource.com/c/chromium/src/+/2083595"> Chromium</a> and<a href="https://bugs.webkit.org/show_bug.cgi?id=208570"> WebKit</a> too.</p>

<h2 id="intersection-and-resize-observers">Intersection and Resize Observers</h2>

<p>As mentioned in our<a href="https://blog.amp.dev/2019/12/16/our-2019-contributions-to-web-platform-interoperability/"> previous blog post</a>, we drove the implementation of<a href="https://webkit.org/blog/8582/intersectionobserver-in-webkit/"> IntersectionObserver</a> (enabled in iOS 12.2) and <a href="https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver">ResizeObserver</a> (enabled in iOS 14 beta) in WebKit. We have made a few enhancements to these useful developer APIs this year.</p>

<p>Users reported difficulties with<a href="https://github.com/w3c/IntersectionObserver/issues/372"> observe root of inner iframe</a> and the specification was modified to accept an explicit document as a root parameter. This was<a href="https://bugs.chromium.org/p/chromium/issues/detail?id=1015183"> implemented in Chromium</a> and we implemented the same change in<a href="https://bugs.webkit.org/show_bug.cgi?id=208047"> WebKit</a> and<a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1617154"> Firefox</a>. It is currently available Safari Tech Preview, iOS 14 beta and Firefox 75.</p>

<p>A bug was also reported with <a href="https://bugs.webkit.org/show_bug.cgi?id=209947">ResizeObserver incorrectly computing size for non-default zoom levels</a>, which was in particular causing a bug on twitter feeds. We landed a patch last April and the fix is available in the latest Safari Tech Preview and iOS 14 beta.</p>

<h2 id="resource-loading">Resource Loading</h2>

<p>Another thing that we have been concerned with is how we can give more control and power to authors to more effectively tell the browser how to manage the loading of resources and improve performance.</p>

<p>The <a href="https://blog.amp.dev/2019/12/16/our-2019-contributions-to-web-platform-interoperability/">work that we started in 2019 </a>on lazy loading has matured a lot along with the <a href="https://github.com/whatwg/html/pull/3752#issuecomment-585202516">specification</a>.</p>

<p>The lazy image loading <a href="https://bugs.webkit.org/show_bug.cgi?id=196698">implementation</a> in WebKit therefore passes the related WPT tests and is functional and comparable to the Firefox and Chrome implementations. However, as you might expect, as we compare uses and implementation notes it becomes apparent that determining the moment when the <a href="https://bugs.webkit.org/show_bug.cgi?id=203557">lazy image load should start</a> is not defined well enough.  Before this can be enabled in releases some more work has to be done on improving that. The related frame lazy loading work has not started yet since the specification is not in place.</p>

<p>We also added an <a href="https://bugs.webkit.org/show_bug.cgi?id=201461">implementation</a> for stale-while-revalidate. The<a href="https://web.dev/stale-while-revalidate/"> stale-while-revalidate</a> Cache-Control directive allows a grace period in which the browser is permitted to serve a stale asset while the browser is checking for a newer version. This is useful for non-critical resources where some degree of staleness is acceptable, like fonts. The feature has been enabled recently in WebKit trunk, but it is still disabled in the latest iOS 14 beta.</p>

<p>Contributions were made to improve prefetching in WebKit taking into account its cache partitioning mechanism. Before this work can be enabled some more patches have to be landed and possibly specified (for example, prenavigate) in more detail. Finally, various general Fetch improvements have been done, improving the fetch WPT score. Examples are:</p>

<ul>
  <li><a href="https://trac.webkit.org/changeset/261821">Remove certain headers when a redirect causes a request method change</a></li>
  <li><a href="https://trac.webkit.org/changeset/258330">Implement wildcard behavior for Cross-Origin-Expose-Headers” </a></li>
  <li><a href="https://trac.webkit.org/changeset/258194">Align with Origin header changes</a></li>
  <li><a href="https://trac.webkit.org/changeset/254672">Fetch: URL parser not always using UTF-8</a></li>
</ul>

<h2 id="whats-next">What’s next</h2>

<p>There is still a lot to do in scrolling and resource loading improvements and we will continue to focus on the features mentioned such as scrollend event, overscroll behavior and scroll behavior, lazy loading, stale-while-revalidate and prefetching.</p>

<p>As a continuation of the work done for aspect ratio calculation of images, we will consider the more general<a href="https://drafts.csswg.org/css-sizing-4/#aspect-ratio"> CSS aspect-ratio property</a>. Performance metrics such as the ones provided by the<a href="https://web.dev/vitals/"> Web Vitals</a> project is also critical for web developers to ensure that their websites provide a good user experience and we are willing to investigate support for these in Safari.</p>

<p>We love doing this work to improve the platform and we’re happy to be able to collaborate in ways that contribute to bettering the web commons for all of us.</p>

{% endraw %}
