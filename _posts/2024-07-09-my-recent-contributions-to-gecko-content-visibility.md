---
layout: post
title: "My recent contributions to Gecko (2/3)"
tags: mozilla igalia css
---

## Introduction

This is the second in a series of blog posts describing new web platform features Igalia has implemented in Gecko, as part of an effort to improve browser interoperability.
I'll talk about the task of implementing [‘content-visibility’](https://drafts.csswg.org/css-contain/#content-visibility), to which several Igalians have contributed since early 2022, and I’ll focus on two main roadblocks I had to overcome.

## The ‘content-visibility’ property

In the past, [Igalia worked on CSS containment](https://blogs.igalia.com/mrego/2019/01/11/an-introduction-to-css-containment/), a feature allowing authors to isolate a subtree from the rest of the document to improve rendering performance.
This is done using the [‘contain’ property](https://developer.mozilla.org/en-US/docs/Web/CSS/contain), which accepts four kinds of containment: `size`, `layout`, `style` and `paint`.

[‘content-visibility’](https://drafts.csswg.org/css-contain/#content-visibility) is a new property allowing authors to "hide" some content from the page, and save the browser unnecessary work by applying containment.
The most interesting one is probably `content-visibility: auto`, which hides content that is not [relevant to the user](https://drafts.csswg.org/css-contain/#relevant-to-the-user).
This is essentially native “virtual scrolling”, allowing you to build virtualized or “recycled” lists without breaking accessibility and find-in-page.

To explain this, consider the typical example of a page with a series of posts, as shown below.
By default, each post would have the four types of containment applied, plus it won't be painted, [won't respond to hit-testing](https://drafts.csswg.org/css-ui-4/#valdef-pointer-events-none), and would use the dimensions specified in the [‘contain-intrinsic-size’](https://developer.mozilla.org/en-US/docs/Web/CSS/contain-intrinsic-size) property.
It's only once a post becomes relevant to the user (e.g. when scrolled close enough to the viewport, or when focus is moved into the post) that the actual effort to properly render the content, and calculate its actual size, is performed:

```css
div.post {
  content-visibility: auto;
  contain-intrinsic-size: 500px 1000px;
}
```
```html
<div class="post">
...
</div>
<div class="post">
...
</div>
<div class="post">
...
</div>
<div class="post">
...
</div>
```

If a post later loses its relevance (e.g. when scrolled away, or when focus is lost) then it would use the dimensions specified by ‘contain-intrinsic-size’ again, discarding the content size that was obtained after layout.
One can also avoid that and use the [last remembered size](https://drafts.csswg.org/css-sizing-4/#last-remembered) instead:

```css
div.post {
  contain-intrinsic-size: auto 500px auto 1000px;
}
```

Finally, there is also a `content-visibility: hidden` value, which is the same as `content-visibility: auto` but never reveals the content, enhancing other methods to hide content such as `display: none` or `visibility: hidden`.

This is just a quick overview of the feature, but I invite you to read the [web.dev article on content-visibility](https://web.dev/articles/content-visibility?hl=en) for further details and thoughts.

## Viewport distance for `content-visibility: auto`

As is often the case, the feature looks straightforward to implement, but issues appear when you get into the details.

In [bug 1807253](https://bugzilla.mozilla.org/show_bug.cgi?id=1807253), my colleague [Oriol Brufau](https://www.igalia.com/team/obrufau) raised an interoperability bug with a very simple test case, reproduced below for convenience.
Chromium would report `0` and `42`, whereas Firefox would sometimes report `0` twice, meaning that the post did not become relevant after a rendering update:

```html
<!DOCTYPE html>
<div id="post" style="content-visibility: auto">
  <div style="height: 42px"></div>
</div>
<script>
console.log(post.clientHeight);
requestAnimationFrame(() => requestAnimationFrame(() => {
  console.log(post.clientHeight);
}));
</script>
```

It turned out that an early version of the specification [relied too heavily on an modified version of IntersectionObserver](https://github.com/w3c/csswg-drafts/issues/8542) to *synchronously* detect when an element is [close to the viewport](https://drafts.csswg.org/css-contain/#close-to-the-viewport), as this was how it was implemented in Chromium.
However, the initial implementation in Firefox relied on a standard IntersectionObserver (with asynchronous notifications of observers) and so failed to produce the behavior described in the specification.
This issue was showing up in several WPT failures.

To solve that problem, the moment when we determine an element's proximity to the viewport was moved into the HTML5 specification, at the step when the rendering is updated, more precisely [when the ResizeObserver notifications are broadcast](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model:content-visibility-auto).
My colleague [Alexander Surkov](https://www.igalia.com/team/asurkov) had started rewriting Firefox's implementation to align with this new behavior in early 2023, and I took over his work in November.

Since this touches the "update the rendering" step which is executed on every page, it was quite likely to break things...
and indeed many regressions were caused by my patch, for example:

* [One regression](https://bugzilla.mozilla.org/show_bug.cgi?id=1867042) was about white flickering of pages on every reload/navigation.
* [One more regression](https://bugzilla.mozilla.org/show_bug.cgi?id=1880928) was about `content-visibility: auto` nodes not being rendered at all.
* [Another regression](https://bugzilla.mozilla.org/show_bug.cgi?id=1866894) was about new [resize loop errors](https://drafts.csswg.org/resize-observer-1/#deliver-resize-error) appearing in tests.
* Some test cases were also found where the "update the rendering step" would repeat indefinitely, causing performance regressions.
* Last but not least, crashes were reported.

Some of these issues were due to the fact that support for the last remembered size in Firefox relied on an internal `ResizeObserver`.
However, the CSS Box Sizing spec only says that the last remembered size is updated when `ResizeObserver` events are delivered, not that such an internal `ResizeObserver` object is actually needed.
I removed this internal observer and ensured the last remembered size is computed directly in the "update the rendering" phase, making the whole thing simpler and more robust.

## Dynamic changes to CSS ‘contain’ and ‘content-visibility’

Before sending the intent-to-ship, we reviewed remaining issues and stumbled on [bug 1765615](https://bugzilla.mozilla.org/show_bug.cgi?id=1765615), which had been opened during the initial 2022 work.
Mozilla indicated this performance bug was important enough to consider an optimization, so I started tackling the issue.

Elaborating a bit about what was mentioned above, a non-visible ‘content-visibility’ implies layout, style and paint containment, and when the element is not relevant to the user, it also implies size containment [^1].
This has certain side effects, for example paint and layout containment establish an [independent formatting context](https://drafts.csswg.org/css-display-4/#establish-an-independent-formatting-context) and affect how the contained box [interacts with floats](https://bug1874826.bmoattachments.org/attachment.cgi?id=9373457) and [how margin collapsing applies](https://bug1765615.bmoattachments.org/attachment.cgi?id=9371959).
Style containment can even have more drastic consequences, since they [make `counter-*` and `*-quote` properties scoped to the subtree](https://drafts.csswg.org/css-contain/#containment-style).

When we dynamically modify the ‘contain’ or ‘content-visibility’ properties, or when the relevance of a `content-visibility: auto` element changes, browsers must make sure that the rendering is properly updated.
It turned out that there were almost no tests for that, and unsurprisingly, Chromium and WebKit had various invalidation bugs.
Firefox was always forcing a [rebuild of the tree used for rendering](https://bugzilla.mozilla.org/show_bug.cgi?id=1765515), which avoided such bugs but is not optimal.

I wrote a couple of web platform tests for [‘contain’](https://wpt.fyi/results/css/css-contain?label=master&label=experimental&aligned&q=dynamic) and [‘content-visibility’](https://wpt.fyi/results/css/css-contain/content-visibility?label=master&label=experimental&aligned&q=containment) [^2], and made sure that Firefox does the minimal invalidation effort needed, being careful not to cause any regressions.
As a result, except for style containment changes, we're now able to avoid the cost a rebuild of the tree used for rendering!


## Conclusion

Almost two years after the initial work on ‘content-visibility’, I was able to send the [intent-to-ship](https://groups.google.com/a/mozilla.org/g/dev-platform/c/kXp-yUvkNKQ), and the feature finally became available in Firefox 125.
Finishing the implementation work on this feature was challenging, but quite interesting to me.

I believe ‘content-visibility’ is a good example of why implementing a feature in different browsers is important to ensure that both the specification and tests are good enough.
The lack of details in the spec regarding when we determine viewport proximity, and the absence for WPT tests for invalidation, definitely made the Firefox work take longer than expected.
But finishing that implementation work was also useful for improving the spec, tests, and other implementations [^3].

I'll conclude this series of blog posts with **fetch priority**, which also has its own interesting story...

[^1]: In both cases, "implies" means the used value of ‘contain’ is modified accordingly.
[^2]: One of the thing I had to handle with care was the update of the accessibility tree, since content that is not relevant to the user must not be exposed. Unfortunately [it's not possible to write WPT tests for accessibility yet](https://github.com/Igalia/webengineshackfest/issues/30) so for now I had to write internal Firefox-specific non-regression tests.
[^3]: Another interesting report happened after the release and is [related to `content-visibility: auto` on elements drawn in a canvas](https://bugzilla.mozilla.org/show_bug.cgi?id=1894546).
