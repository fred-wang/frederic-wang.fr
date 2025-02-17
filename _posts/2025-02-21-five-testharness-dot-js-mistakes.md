---
layout: post
title: "Five testharness.js mistakes"
tags: igalia wpt testharness
---

## Introduction

I recently led a small training session at Igalia where I proposed to find mistakes in five small [testharness.js](https://web-platform-tests.org/writing-tests/testharness.html) tests I wrote.
These mistakes are based on actual issues I found in official [web platform tests](https://web-platform-tests.org), or on mistakes I made myself in the past while writing tests, so I believe they would be useful to know.
The feedback from my teammates was quite positive, with very good participation and many ideas.
They suggested I write a blog post about it, so here it is.

Please read the tests carefully and try to find the mistakes before looking at the proposed fixes...

## 1. Multiple tests in one loop

We often need to perform identical assertions for a set of similar objects.
A good practice is to split such checks into multiple `test()` calls, so that it's easier to figure out which of the objects are causing failures.
Below, I'm testing the reflected `autoplay` attribute on the `<audio>` and `<video>` elements.
What small mistake did I make?

```html
<!DOCTYPE html>
<script src="/resources/testharness.js"></script>
<script src="/resources/testharnessreport.js"></script>
<script>
  ["audio", "video"].forEach(tagName => {
    test(function() {
      let element = document.createElement(tagName);
      assert_equals(element.autoplay, false, "inital value");
      element.setAttribute("autoplay", "autoplay");
      assert_equals(element.autoplay, true, "after setting attribute");
      element.removeAttribute("autoplay");
      assert_equals(element.autoplay, false, "after removing attribute");
    }, "Basic test for HTMLMediaElement.autoplay.");
  });
</script>
```

### Proposed fix

Each loop iteration creates one test, but they all have have the name `"Basic test for HTMLMediaElement.autoplay."`.
Because this name identifies the test in various places (e.g. failure expectations), it must be unique to be useful.
These tests will even cause a "Harness status: Error" with the message "duplicate test name".

One way to solve that is to move the loop iteration into the `test()`, which will fix the error but won't help you with fine-grained failure reports.
We can instead use a different description for each iteration:

```diff
       assert_equals(element.autoplay, true, "after setting attribute");
       element.removeAttribute("autoplay");
       assert_equals(element.autoplay, false, "after removing attribute");
-    }, "Basic test for HTMLMediaElement.autoplay.");
+    }, `Basic test for HTMLMediaElement.autoplay (${tagName} element).`);
   });
 </script>
```

### 2. Cleanup between tests

Sometimes, it is convenient to reuse objects (e.g. DOM elements) for several `test()` calls, and some cleanup may be necessary.
For instance, in the following test, I'm checking that setting the `class` attribute via `setAttribute()` or `setAttributeNS()` is properly reflected on the `className` property.
However, I must clear the `className` at the end of the first `test()`, so that we can really catch the failure in the second `test()` if, for example, `setAttributeNS()` does not modify the `className` because of an implementation bug.
What's wrong with this approach?

```html
<!DOCTYPE html>
<script src="/resources/testharness.js"></script>
<script src="/resources/testharnessreport.js"></script>
<div id="element"></div>
<script>
  test(function() {
    element.setAttribute("class", "myClass");
    assert_equals(element.className, "myClass");
    element.className = "";
  }, "Setting the class attribute via setAttribute().");

  test(function() {
    element.setAttributeNS(null, "class", "myClass");
    assert_equals(element.className, "myClass");
    element.className = "";
  }, "Setting the class attribute via setAttributeNS().");
</script>
```

### Proposed fix

In general, it is difficult to guarantee that a final cleanup is executed.
In this particular case, for example, if the `assert_equals()` fails because of bad browser implementation, then an exception is thrown and the rest of the function is not executed.

Fortunately, testharness.js provides a better way to [perform cleanup after a test execution](https://web-platform-tests.org/writing-tests/testharness-api.html#cleanup):

```diff
-  test(function() {
+  function resetClassName() { element.className = ""; }
+
+  test(function(t) {
+    t.add_cleanup(resetClassName);
     element.setAttribute("class", "myClass");
     assert_equals(element.className, "myClass");
-    element.className = "";
   }, "Setting the class attribute via setAttribute().");

-  test(function() {
+  test(function(t) {
+    t.add_cleanup(resetClassName);
     element.setAttributeNS(null, "class", "myClass");
     assert_equals(element.className, "myClass");
-    element.className = "";
   }, "Setting the class attribute via setAttributeNS().");
```


### 3. Checking whether an exception is thrown

Another very frequent test pattern involves checking whether a Web API throws an exception.
Here, I'm trying to use `DOMParser.parseFromString()` to parse a small MathML document.
The HTML spec says that it should throw a `TypeError` if one specifies the MathML MIME type.
The second `test()` asserts that the rest of the `try` branch is not executed and that the correct exception type is found in the `catch` branch.
Is this approach correct?
Can the test be rewritten in a better way?

```html
<!DOCTYPE html>
<script src="/resources/testharness.js"></script>
<script src="/resources/testharnessreport.js"></script>
<script>
  const parser = new DOMParser();
  const mathmlSource = `<?xml version="1.0"?>
<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mfrac>
    <mn>1</mn>
    <mi>x</mi>
  </mfrac>
</math>`;

  test(function() {
    let doc = parser.parseFromString(mathmlSource, "application/xml");
    assert_equals(doc.documentElement.tagName, "math");
  }, "DOMParser's parseFromString() accepts application/xml");

  test(function() {
    try {
      parser.parseFromString(mathmlSource, "application/mathml+xml");
      assert_unreached();
    } catch(e) {
      assert_true(e instanceof TypeError);
    }
  }, "DOMParser's parseFromString() rejects application/mathml+xml");
</script>
```

### Proposed fix

If the `assert_unreached()` is executed because of an implementation bug with `parseFromString()`, then the assertion will actually throw an exception.
That exception won't be a `TypeError`, so the test will still fail because of the `assert_true()`, but the failure report will look a bit confusing.

In this situation, it's better to use the [`assert_throws_*` APIs](https://web-platform-tests.org/writing-tests/testharness-api.html#assert-functions):


```diff
   test(function() {
-    try {
-      parser.parseFromString(mathmlSource, "application/mathml+xml");
-      assert_unreached();
-    } catch(e) {
-      assert_true(e instanceof TypeError);
-    }
+    assert_throws_js(TypeError,
+        _ => parser.parseFromString(mathmlSource, "application/mathml+xml"));
   }, "DOMParser's parseFromString() rejects application/mathml+xml");
```


### 4. Waiting for an event listener to be called

The following test verifies a very basic feature: clicking a button triggers the registered event listener.
We use the (asynchronous) testdriver API `test_driver.click()` to emulate that user click, and a `promise_test()` call to wait for the click event listener to be called.
The test may time out if there is something wrong in the browser implementation, but do you see a risk for flaky failures?

*Note: the testdriver API only works when running tests automatically.
If you run the test manually, you need to click the button yourself.*

```html
<!DOCTYPE html>
<script src="/resources/testharness.js"></script>
<script src="/resources/testharnessreport.js"></script>
<script src="/resources/testdriver.js"></script>
<script src="/resources/testdriver-vendor.js"></script>
<button id="button">Click me to run manually</button>
<script>
  promise_test(function() {
    test_driver.click(button);
    return new Promise(resolve => {
      button.addEventListener("click", resolve);
    });
  }, "Clicking the button triggers registered click event handler.");
</script>
```

### Proposed fix

The problem I wanted to show here is that we are sending the click event before actually registering the listener.
The test would likely still work, because `test_driver.click()` is asynchronous and communication to the test automation scripts is slow, whereas registering the event is synchronous.

But rather than making this kind of assumption, which poses a risk of flaky failures as well as making the test hard to read, I prefer to just move the statement that triggers the event into the `Promise`, after the listener registration:

```diff
 <button id="button">Click me to run manually</button>
 <script>
   promise_test(function() {
-    test_driver.click(button);
     return new Promise(resolve => {
       button.addEventListener("click", resolve);
+      test_driver.click(button);
     });
   }, "Clicking the button triggers registered click event handler.");
 </script>
```

My colleagues also pointed out that if the promise returned by `test_driver.click()` fails, then a "Harness status: Error" could actually be reported with "Unhandled rejection".
We can add a `catch` to handle this case:

```diff
 <button id="button">Click me to run manually</button>
 <script>
   promise_test(function() {
-    return new Promise(resolve => {
+    return new Promise((resolve, reject) => {
       button.addEventListener("click", resolve);
-      test_driver.click(button);
+      test_driver.click(button).catch(reject);
     });
   }, "Clicking the button triggers registered click event handler.");
 </script>
```

### 5. Dealing with asynchronous resources

It's very common to deal with asynchronous resources in web platform tests.
The following test case verifies the behavior of a frame with lazy loading: it is initially outside the viewport (so not loaded) and then scrolled into the viewport (which should trigger its load).
The actual loading of the frame is tested via the window name of `/common/window-name-setter.html` (should be "spices").
Again, this test may time out if there is something wrong in the browser implementation, but can you see a way to make the test a bit more robust?

*Side question: the `<div id="log"></div>` and `add_cleanup()` are not really necessary for this test to work, so what's the point of using them?
Can you think of one?*

```html
<!DOCTYPE html>
<script src="/resources/testharness.js"></script>
<script src="/resources/testharnessreport.js"></script>
<style>
  #lazyframe { margin-top: 10000px; }
</style>
<div id="log"></div>
<iframe id="lazyframe" loading="lazy"
        src="/common/window-name-setter.html"></iframe>
<script>
  promise_test(function() {
    return new Promise(resolve => {
      window.addEventListener("load", () => {
        assert_not_equals(lazyframe.contentWindow.name, "spices");
        resolve();
      });
    });
  }, "lazy frame not loaded after page load");
  promise_test(t => {
    t.add_cleanup(_ => window.scrollTo(0, 0));
    return new Promise(resolve => {
      lazyframe.addEventListener('load', () => {
        assert_equals(lazyframe.contentWindow.name, "spices");
        resolve();
      });
      lazyframe.scrollIntoView();
    });
  }, "lazy frame loaded after appearing in the viewport");
</script>
```

### Proposed fix

This is similar to what we discussed in the previous tests.
If the `assert_equals()` in the listener fails, then an exception is thrown, but it won’t be caught by the testharness.js framework.
A "Harness status: Error" is reported, but the test will only complete after the timeout.
This can slow down test execution, especially if this pattern is repeated for several tests.

To make sure we report the failure immediately in that case, we can instead reject the promise if the equality does not hold, or even better, place the `assert_equals()` check after the promise resolution:


```diff
 <script>
   promise_test(function() {
     return new Promise(resolve => {
-      window.addEventListener("load", () => {
-        assert_not_equals(lazyframe.contentWindow.name, "spices");
-        resolve();
-      });
-    });
+      window.addEventListener("load", resolve);
+    }).then(_ => {
+      assert_not_equals(lazyframe.contentWindow.name, "spices");
+    });;
   }, "lazy frame not loaded after page load");
   promise_test(t => {
     t.add_cleanup(_ => window.scrollTo(0, 0));
     return new Promise(resolve => {
-      lazyframe.addEventListener('load', () => {
-        assert_equals(lazyframe.contentWindow.name, "spices");
-        resolve();
-      });
+      lazyframe.addEventListener('load', resolve);
       lazyframe.scrollIntoView();
+    }).then(_ => {
+      assert_equals(lazyframe.contentWindow.name, "spices");
     });
   }, "lazy frame loaded after appearing in the viewport");
 </script>
```

Regarding the side question, if you run the test by opening the page in the browser, then the report will be appended at the bottom of the page by default.
But `lazyframe` has very large height, and the page may be scrolled to some other location.
`<div id="log"></div>` makes sure the report is placed at the bottom of the page, while the `add_cleanup()` ensures that we scroll to that location after test execution.
