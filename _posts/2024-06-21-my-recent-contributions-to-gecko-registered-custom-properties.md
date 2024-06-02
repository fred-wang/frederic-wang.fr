---
layout: post
title: "My recent contributions to Gecko (1/3)"
tags: mozilla igalia css
---

## Introduction

Igalia has been contributing to the web platform implementations of different web engines for a long time.
One of our goals is ensuring that these implementations are interoperable, by relying on various web standards and [web platform tests](https://wpt.fyi/results/).
In July 2023, I happily joined a project that focuses on this goal, and I worked more specifically on the Gecko web engine.
One year later, three new features I contributed to are being shipped in Firefox.
In this series of blog posts, I'll give an overview of those features (namely registered custom properties, content visibility, and fetch priority) and my journey to make them "ride the train" as Mozilla people say.

Let's start with registered custom properties, an enhancement of traditional CSS variables.

## Registered custom properties

You may already be familiar with [CSS variables](https://drafts.csswg.org/css-variables/), these "dash dash" names that facilitate the maintenance of a large web site by allowing author-defined CSS properties.
In the example below, the `:root` selector defines a variable `--main-theme-color` with value "blue", which is used for the style applied to other elements via the `var()` CSS function.
As you can see, this makes the usage of the main theme color in different places more readable and makes customizing that color much easier.

```css
:root { --main-theme-color: blue; }
p { color: var(--main-theme-color); }
section {
  padding: 1em;
  border: 1px solid var(--main-theme-color);
}
.progress-bar {
  height: 10px;
  width: 100%;
  background: linear-gradient(white, var(--main-theme-color));
}
```

```html
<section>
  <p>Loading...</p>
  <div class="progress-bar"></div>
</section>
```

In [browsers supporting CSS variables](https://developer.mozilla.org/en-US/docs/Web/CSS/var#browser_compatibility), you should see a frame containing the text "Loading" and a progress bar, all of these components being blue:

<style>
.example1 {
  --main-theme-color: blue;
  margin: 2em;
}
.example1 p {
  color: var(--main-theme-color);
}
.example1 section {
  padding: 1em;
  border: 1px solid var(--main-theme-color);
}
.example1 .progress-bar {
  height: 10px;
  width: 100%;
  background: linear-gradient(white, var(--main-theme-color));
}
</style>
<div class="example1">
<section>
  <p>Loading...</p>
  <div class="progress-bar"></div>
</section>
</div>

Having such CSS variables available is already nice, but they are lacking some features available to native CSS properties...
For example, there is (almost) no syntax checking on specified values, they are always inherited, and their [initial value](https://drafts.csswg.org/css-cascade/#initial-values) is always the [guaranteed invalid value](https://drafts.csswg.org/css-variables/#guaranteed-invalid-value).
In order to improve on that situation, the [CSS Properties and Values specification](https://drafts.css-houdini.org/css-properties-values-api/) provides some APIs to *register* custom properties with further characteristics:

* An accepted [syntax](https://drafts.css-houdini.org/css-properties-values-api/#syntax-string) for the property; for example, `igalia | <url> | <integer>+` means either the custom identifier "igalia", or a URL, or a space-separated list of integers.
* Whether the property is inherited or non-inherited.
* An initial value.

Custom properties can be registered via CSS or via a JS API, and these ways are equivalent.
For example, to register `--main-theme-color` as a non-inherited [color](https://drafts.csswg.org/css-color-5/#typedef-color) with initial value `blue`:

```css
@property --main-theme-color {
  syntax: "<color>";
  inherits: false;
  initial-value: blue;
}
```

```js
window.CSS.registerProperty({
  name: "--main-theme-color",
  syntax: "<color>",
  inherits: false,
  initialValue: blue,
});
```

## Interpolation of registered custom properties

By having custom properties registered with a specific `syntax`, we open up the possibility of [interpolating](https://drafts.csswg.org/css-values-4/#interpolation) between two values of the properties when performing an animation.
Consider the following example, where the width of the `animated` div depends on the custom property `--my-length`.
Defining this property as a length allows browsers to [interpolate it continuously](https://drafts.csswg.org/css-values-4/#combine-dimensions) between 10px and 200px when it is animated:

```css
 @property --my-length {
   syntax: "<length>";
   inherits: false;
   initialValue: '0px';
 }
 @keyframes test {
   from {
     --my-length: 10px;
   }
   to {
     --my-length: 200px;
   }
 }
 div#animated {
   animation: test 2s linear both;
   width: var(--my-length, 10px);
   height: 200px;
   background: lightblue;
 }
```

With non-registered custom properties, we can instead only [animate discretely](https://drafts.csswg.org/web-animations-1/#discrete); `--my-length` would suddenly jump from 10px to 200px halfway through the duration of the animation, which is generally not what is desired for lengths.

## Custom properties in the cascade

If you check the [Interop 2023 Dashboard for custom properties](https://wpt.fyi/interop-2023?feature=interop-2023-property), you may notice that interoperability was really bad at the beginning of the year, and this was mainly due to Firefox's low score.
Consequently, when I joined the project, I was asked to help with improving that situation.

![Graph showing the 2023 evolution of scores and interop for custom properties](https://frederic-wang.fr//images/interop-2023-custom-properties.png)

While the two registration methods previously mentioned had already been implemented, the main issue was that the CSS cascade was always treating custom properties as inherited and initialized with the guaranteed invalid value.
This is indeed correct for unregistered custom properties, but it's generally *incorrect* for registered custom properties!

In [bug 1840478](https://bugzilla.mozilla.org/show_bug.cgi?id=1840478), [bug 1855887](https://bugzilla.mozilla.org/show_bug.cgi?id=1855887), and others, I made registered custom properties work properly in the cascade, including non-inherited properties and registered initial values.
But in the past, with the previous assumptions around inheritance and initial values, it was possible to store the computed values of custom properties on an element as a "cheap" map, considering only the properties actually specified on the element or an ancestor and (in most cases) only taking shallow copies of the parent's map.
As a result, when generalizing the cascade for registered custom properties, I had to be careful to avoid introducing performance regressions for existing content.

## Custom properties in animations

Another area where the situation was pretty bad was animations.
Not only was Firefox unable to interpolate registered custom properties between two values — one of the main motivations for the new spec — but it was actually unable to animate custom properties at all!

The main problem was that the existing animation code referred to CSS properties using an enum `nsCSSPropertyID`, with all custom properties represented by the single value `nsCSSPropertyID::eCSSPropertyExtra_variable`.
To make this work for custom properties, I had to essentially replace that value with a structure containing the `nsCSSPropertyID` and the name of the custom properties.

I uploaded patches to [bug 1846516](https://bugzilla.mozilla.org/show_bug.cgi?id=1846516) to perform that change throughout the whole codebase, and with a few more tweaks, I was able to make registered custom properties animate discretely, but my patches still needed some polish before they could be reviewed.
I had to move onto other tasks, but fortunately, some Mozilla folks were kind enough to take over this task, and more generally, complete the work on registered custom properties!

## Conclusion

This was an interesting task to work on, and because a lot of the work happened in Stylo, the CSS engine shared by Servo and Gecko, I also had the opportunity to train more on the Rust programming language.
Thanks to help from folks at Mozilla, we were able to get excellent progress on registered custom properties in Firefox in 2023, and this feature is [expected to ship in Firefox 128](https://groups.google.com/a/mozilla.org/g/dev-platform/c/UhQSvl_v6xk/m/AvkjQbC0BwAJ)!

As I said, I’ve since moved onto other tasks, which I'll describe in subsequent blog posts in this series.
Stay tuned for `content-visibility`, enabling interesting layout optimizations for web pages.
