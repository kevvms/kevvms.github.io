---
layout: post
title: "How to Write Actually Good Comments"
comments: true
---

It's common to assume your code comments are sufficient. However, for many developers, comments are an afterthought, often leading to noise rather than clarity. The goal isn't just to write comments, but to write **comments that add measurable value**.

By understanding the core purpose of a comment, you can elevate the readability and maintainability of your codebase.

---

## Comments Explain the *Why*, Not the *What*

The code itself is the specification for *what* is happening. A comment's primary role is to explain the **rationale, context, or constraint**—in short, the *why* the code is written in a particular way.

### Avoid Redundancy:

~~~js
balance = balance - fee; // subtract fee
~~~
This type of comment is easily ignored and adds cognitive load without providing new information.

### Provide Context:

~~~js
// Deducts the processing fee. This calculation is written to precisely 
// mirror the logic used in the backend service for financial consistency.
balance = balance - fee;
~~~
This comment clarifies the **business logic constraint**, making the code more robust against future refactoring.

---

## Justify Intentional Deviations

When you deliberately choose a simple, clear implementation over a more "clever" or terse alternative, document that decision. This prevents future maintainers from wasting time trying to "optimize" or rewrite code that was intentionally kept simple for a good reason.

~~~js
// A one-liner map/reduce could be used here, but this explicit loop 
// simplifies debugging and makes control flow clearer for complex user objects.
for user in users:
	process(user)
~~~

---

## ⚠️ Document Assumptions and Potential Breakpoints

If a section of code relies on a specific external condition or assumption, mark that dependency clearly. This creates a critical debugging note for the future, should that external condition change.

~~~js
// API documentation asserts that `fetchData()` will never return a null value.
// If a NullPointer or TypeError occurs here, the issue is likely upstream in the API.
const data = fetchData();
~~~

---

## ⚙️ Explain Your Workarounds

Code that implements a workaround for a specific bug (e.g., a browser-specific issue, an external library bug) must be documented. Without context, these essential fixes look like errors and are often mistakenly removed.

~~~css
/* This wrapper is present to normalize spacing. Flex 'gap' property fails 
to render correctly in Safari when nested within this specific component structure.
Do not remove this wrapper unless the Safari bug is confirmed fixed. */
.wrapper { display: flex }
~~~

---

## Summary

To write truly good comments, remember this:

> **Code** defines *what* is executed. **Comments** articulate *why* it was designed that way.
