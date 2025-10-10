---
layout: post
title: "How to Write Actually Good Comments"
comments: true
---

Hey you, yes you! You might think your code comments are already good enough, but is it really?

Let me tell you something, most people don't actually know how to write good comments. Do you want to be one of them? No! So, what are you waiting for?

## Comments Aren't Subtitles!
Comments are meant to make readers understand your code. The code already tells *what* it does, so comments should explain *why* it's written that way.

For example, don't do this:

~~~js
balance = balance - fee; // subtract fee
~~~

Instead, do this!

~~~js
// Deducts processing fee; backend uses the same calculation for consistency.
balance = balance - fee;
~~~

Well, you don't have to make it that long, just long enough for the readers to understand.

## If You Break a Pattern, Explain Why
When you intentionally avoid the "clever" way, leave a note.

~~~js
// Could be a one-liner, but this is easier to debug.
for user in users:
	process(user)
~~~

## Comment Assumptions and Future Breakpoints
If you leave a part of your code unprotected from future breaks, explain why.

~~~js
// API says this never returns null; if it ever does, start debugging here.
const data = fetchData();
~~~

## Comment Your Code Hacks
Maybe you have a hack in your code to keep it working on some devices. Make sure to explain that so people won't delete it!

~~~css
/* Flex gap breaks in Safari when nested. This wrapper is just here to normalize spacing. */
.wrapper { display: flex }
~~~

## TL;DR
There you go! To sum things up,

Code explains *what* happens. Comments explain *why* it had to happen like that. Thanks for reading! 

