---
layout: post
title: "My recent contributions to Gecko (3/3)"
tags: mozilla igalia html dom http
---

**Note: This blog post was written on June 2024. As of September 2024, final work to ship the feature is still in progress. Please follow [bug 1797715](https://bugzilla.mozilla.org/show_bug.cgi?id=1797715) for the latest updates.**

## Introduction

This is the final blog post in a series about new web platform features implemented in Gecko, as part as an effort at Igalia to increase browser interoperability.

Let's take a look at [fetch priority attributes](https://html.spec.whatwg.org/multipage/urls-and-fetching.html#fetch-priority-attribute), which enable web developers to optimize resource loading by specifying the relative priority of resources to be fetched by the browser.

## Fetch priority

The [web.dev article on fetch priority](https://web.dev/articles/fetch-priority?hl=en#browser_priority_and_fetchpriority) explains in more detail how web developers can use fetch priority to optimize resource loading, but here’s a quick overview.

[`fetchpriority`](https://html.spec.whatwg.org/multipage/urls-and-fetching.html#fetch-priority-attributes) is a new attribute with the value `auto` (default behavior), `high`, or `low`.
Setting the attribute on a `script`, `link` or `img` element indicates whether the corresponding resource should be loaded with normal, higher, or lower priority [^1]:

```html
<head>
  <script src="high.js" fetchpriority="high"></script>
  <link rel="stylesheet" href="auto.css" fetchpriority="auto">
</head>
<body>
  <img src="low.png" alt="low" fetchpriority="low">
</body>
```

The priority can also be set in the [RequestInit](https://fetch.spec.whatwg.org/#requestinit) parameter of the [fetch() method](https://fetch.spec.whatwg.org/#fetch-method):

```js
await fetch("high.txt", {priority: "high"});
```

The &lt;link> element has some interesting features.
One of them is combining [`rel=preload` and `as`](https://html.spec.whatwg.org/multipage/links.html#link-type-preload) to fetch a resource with a particular [destination](https://fetch.spec.whatwg.org/#concept-request-destination) [^2]:

```html
<link rel="preload" as="font" href="high.woff2" fetchpriority="high">
```

You can even use [`Link` in HTTP response headers](https://html.spec.whatwg.org/multipage/semantics.html#processing-link-headers) and in particular [early hints](https://html.spec.whatwg.org/multipage/semantics.html#early-hints) sent before the final response:

```
103 Early Hint
Link: <high.js>; rel=preload; as=script; fetchpriority=high
```

These are basically all the places where a fetch priority attribute can be used.

Note that other parameters are also taken into account when deciding the priority to use for resources, such as the position of the element in the page (e.g. blocking resources in &lt;head>), other attributes on the element (&lt;script async>, &lt;script defer>, &lt;link media>, &lt;link rel>...) or the resource's [destination](https://fetch.spec.whatwg.org/#concept-request-destination).

Finally, some browsers implement [speculative HTML parsing](https://html.spec.whatwg.org/#speculative-html-parsing), allowing them to continue fetching resources declared in the HTML markup while the parser is blocked.
As far as I understand, Firefox has its own separate HTML parsing code for that purpose, which also has to take fetch priority attributes into account.

## Implementation-defined prioritization

If you have not run away after reading the complexity described in the previous section, let's talk a bit more about how fetch priority attributes are interpreted.
The spec contains the following step when [fetching a resource](https://fetch.spec.whatwg.org/#fetching) (emphasis mine):

> If *request*’s internal priority is null, then use *request*’s **priority**, initiator, **destination**, and render-blocking in an **implementation-defined manner** to set *request*’s **internal priority** to an **implementation-defined object**.

So browsers would use the `high`/`low`/`auto` hints as well as the [destination](https://fetch.spec.whatwg.org/#concept-request-destination) in order to calculate an internal priority value [^3], but the details of this value are not provided in the specification, and it's up to the browser to decide what to do.
This is a bit unfortunate for our interoperability goal, but that's probably the best we can do, given that each browser already has its own stategies to optimize resource loading.
I think this also gives browsers some flexibility to experiment with optimizations... which can be hard to predict when you realize that web devs also try to adapt their content to the behavior of (the most popular) browsers!

In any case, the spec authors were kind enough to provide a note with more suggestions (emphasis mine):

> The implementation-defined object could encompass **stream weight and dependency for HTTP/2**, priorities used in **Extensible Prioritization Scheme for HTTP** for transports where it applies (including HTTP/3), and equivalent information used to **prioritize dispatch and processing of HTTP/1 fetches**. [[RFC9218]](https://httpwg.org/specs/rfc9218.html)

OK, so what does that mean?
I'm not a networking expert, but this is what I could gather after discussing with the [Necko team](https://wiki.mozilla.org/Networking) and reading some HTTP specs:

* HTTP/1 does not have a dedicated prioritization mechanism, but Firefox uses its internal priority to order requests.
* [HTTP/2](https://www.rfc-editor.org/rfc/rfc9113.html) has a "stream priority" mechanism and Firefox uses its internal priority to implement that part of the spec.
  However, it was considered too complex and inefficient, and is likely poorly supported by existing web servers...
* In upcoming releases, Firefox will use its internal priority to implement the [Extensible Prioritization Scheme](https://www.rfc-editor.org/rfc/rfc9218.html) used by HTTP/2 and HTTP/3.
  See [bug 1865040](https://bugzilla.mozilla.org/show_bug.cgi?id=1865040) and [bug 1864392](https://bugzilla.mozilla.org/show_bug.cgi?id=1864392).
  Essentially, this means using its internal priority to adjust the [urgency](https://www.rfc-editor.org/rfc/rfc9218.html#section-4.1) parameter.

Note that various parts of Firefox rely on [NS_NewChannel](https://searchfox.org/mozilla-central/rev/b11735b86bb4d416c918e2b2413456561beff50c/netwerk/base/nsNetUtil.h#140) to load resources, including the fetching algorithm above, which Firefox uses to implement the fetch() method.
However, other cases mentioned in the first section have their own code paths with their own calls to `NS_NewChannel`, so these places must also be adjusted to take the fetch priority and destination into account.

## Finishing the implementation work

Summarizing a bit, [implementing fetch priority](https://bugzilla.mozilla.org/show_bug.cgi?id=1797715#c2) is a matter of:

1. Adding `fetchpriority` to DOM objects for `HTMLImageElement`, `HTMLLinkElement`, `HTMLScriptElement`, and `RequestInit`.
2. Parsing the fetch priority attribute into an `auto`/`low`/`high` enum.
3. Passing the information to the callers of `NS_NewChannel`.
4. Using that information to set the internal priority.
5. Using that internal priority for HTTP requests.

[Mirko Brodesser](https://www.igalia.com/team/mbrodesser) started this work in June 2023, and had already implemented almost all of the features discussed above.
fetch(), &lt;img>, and `<link rel=preload as=image>` were handled by [Ziran Sun](https://www.igalia.com/team/zsun) and I, while [Valentin Gosu](https://valentin.gosu.se/) from Mozilla made HTTP requests use the internal priority.

The main blocker was due to that "implementation-defined" use of fetch priority.
Mirko's approach was to align Firefox with the behavior described in the [web.dev article](https://web.dev/articles/fetch-priority?hl=en#effects), which reflects Chromium’s implementation.
But doing so would mean changing Firefox's default behavior when `fetchpriority` is not specified (or explicitly set to `auto`), and it was not clear whether Chromium's prioritization choices were the best fit for Firefox's own implementation of resource loading.

After meeting with Mozilla, we agreed on a safer approach:

1. Introduce [runtime preferences](https://searchfox.org/mozilla-central/search?q=network.fetchpriority.adjustments&path=StaticPrefList.yaml) to control how Firefox adjusts internal priorities when `low`, `high`, or `auto` is specified.
   By default, `auto` does not affect the internal priority so current behavior is preserved.
2. Ask Mozilla's performance team to run an experiment, so we can decide the best values for these preferences.
3. Ship fetch priority with the chosen values, probably cleaning things up a bit.
   Any other ideas, including the ones described in the `web.dev` article, could be handled in future enhancements.

We recently entered phase 2 of this plan, so fingers crossed it works as expected!

## Internal WPT tests

This project is part of the interoperability effort, but again, the "implementation-defined" part meant that we had very few WPT tests for that feature, really only those checking `fetchpriority` attributes for the DOM part.

Fortunately Mirko, who is a proponent of [Test-driven development](https://en.wikipedia.org/wiki/Test-driven_development), had written quite a lot of internal WPT tests that use internal APIs to retrieve the internal priority.
To test `Link` headers, he used the handy [wptserve pipes](https://web-platform-tests.org/writing-tests/server-pipes.html#headers).
The only thing he missed was checking [support in Early hints](https://bugzilla.mozilla.org/show_bug.cgi?id=1882084), but some WPT tests for early hints using [WPT Python Handlers](https://web-platform-tests.org/writing-tests/python-handlers/) were available, so integrating them into Mirko's tests was not too difficult.

It was also straightforward for Ziran and I to extend Mirko's tests to cover `fetch`, `img`, and `<link rel=preload as=image>`, with one exception: when the fetch() method uses a non-default destination.
In most of these code paths, we call `NS_NewChannel` to perform a fetch.
But fetch() is tricky, because if the fetch event is [intercepted](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent#examples), the event handler might call the fetch() method again using the same destination (e.g. `image`).

Handling this correctly involves multiple processes and IPC communication, which ended up not working well with the internal APIs used by Mirko's tests.
It took me a while to understand what was happening in [bug 1881040](https://bugzilla.mozilla.org/show_bug.cgi?id=1881040), and in the end I came up with a new approach.

## Upstreamable WPT tests

First, let's pause for a moment: all the tests we have so far use an internal API to verify the internal priority, but they don't actually check how that internal priority is used by Firefox when it sends HTTP requests.
Valentin mentioned we should probably have some tests covering that, and not only would it solve the problem with fetch() calls in fetch event handlers, it would also remove the use of an internal API, making the tests potentially reusable by other browsers.

To make this kind of test possible, I [added](https://bugzilla.mozilla.org/show_bug.cgi?id=1892734) a [WPT Python Handler](https://web-platform-tests.org/writing-tests/python-handlers/) that parses the [urgency](https://www.rfc-editor.org/rfc/rfc9218.html#section-4.1) from a HTTP request and responds with an urgency-dependent resource, such as a stylesheet with different property values, an image of a different size, or an audio or video file of a different duration.

When a test uses resources with different fetch priorities, this influences the urgency values of their HTTP requests, which in turn influences the response in a way that the test can check for in JavaScript.
This is a bit complicated, but it works!

## Conclusion

Fetch priority has been enabled in Firefox Nightly for a while, and experiments started recently to determine the optimal priority adjustments.
If everything goes well, we will be able to push this feature to the finish line after the (northern) summer.

Helping implement this feature also gave me the opportunity to work a bit on the Firefox networking code, which I had not touched since the [collaboration with IPFS](https://blog.ipfs.tech/2021-01-15-ipfs-and-igalia-collaborate-on-dweb-in-browsers/), and I learned a lot about resource loading and WPT features for HTTP requests.

To me, the "implementation-defined" part was still a bit awkward for the web platform.
We had to write our own internal WPT tests and do extra effort to prepare the feature for shipping.
But in the end, I believe things went relatively smoothly.

## Acknowledgments

To conclude this series of blog posts, I'd also like to thank Alexander Surkov, Cathie Chen, Jihye Hong, Martin Robinson, Mirko Brodesser, Oriol Brufau, Ziran Sun, and others at Igalia who helped on implementing these features in Firefox.
Thank you to Emilio Cobos, Olli Pettay, Valentin Gosu, Zach Hoffman, and others from the Mozilla community who helped with the implementation, reviews, tests and discussions.
Finally, our [spelling and grammar](https://www.azabani.com/2021/05/17/spelling-grammar.html) expert [Delan Azabani](https://www.igalia.com/team/dazabani) deserves special thanks for reviewing this series of blog post and providing useful feedback.

[^1]: Other elements have been or are being considered (e.g. [&lt;iframe>](https://bugzilla.mozilla.org/show_bug.cgi?id=1795233#c7), [SVG &lt;image>](https://bugzilla.mozilla.org/show_bug.cgi?id=1865837) or [SVG &lt;script>](https://bugzilla.mozilla.org/show_bug.cgi?id=1847712)), but these are the only ones listed in the HTML spec at the time of writing.
[^2]: As mentioned below, the browser needs to know about the actual destination in order to properly calculate the priority.
[^3]: As far as I know, Firefox does not take initiator into account, [nor does it support render-blocking yet](https://bugzilla.mozilla.org/show_bug.cgi?id=1751383).
