---
layout: post
title: "When Python isn't Python-ing"
date: 2025-11-01
categories: ["Local Development", "Python"]
image: /assets/img/weird-python.jpg
---

Python is known for its straightforwardness and readability, but sometimes.. it just doesn't make sense! We'll explore some of these unexpected quirks that make Python just puzzling.

1. [Wait, It Isn't?](#wait-it-isnt)
2. [Is This List Even Mine?](#is-this-list-even-mine)
3. [Yes but No](#yes-but-no)
4. [0.1 + 0.2 Ain't 0.3](#01--02-aint-03)
5. [The Loop-Lambda Surprise](#the-loop-lambda-surprise)
6. [Copying a List with *](#copying-a-list-with-)
7. [Sneaky Booleans!](#sneaky-booleans)
{:toc}

## Wait, It Isn't?

`is`, a common operator in Python used to check if _a_ equals to _b_. It should have no problems with anything, right? RIGHT??

~~~python
a = 256
b = 256
print(a is b)
~~~
.. this returns:
~~~bash
True
~~~
But if we add just one to both,
~~~python
a = 257
b = 257
print(a is b)
~~~
.. it should return `True` right? WRONG!
~~~bash
False
~~~
The technical reason for this is that Python internally caches small integers (-5 to 256) for optimization reasons. So.. best if you use `==` instead.

## Is This List Even Mine?

So, you think you're being clever by using a list as a default argument in your Python function? Well, hold on to your hats, because this can lead to some seriously weird behavior!

~~~python
def add_stuff(x, my_list=[]):
    my_list.append(x)
    return my_list

print(add_stuff(1))
print(add_stuff(2))
~~~
Normal, right? Theoritically, this would output:
~~~bash
[1]
[2]
~~~
.. but Python says HELL NO!
~~~bash
[1]
[1, 2]
~~~

What's happening here is that Python keeps using the same list over and over. Like a shared notebook; everyone's writing in the same one instead of getting their own.

Let's make Python give us a new list each time:

~~~python
def add_stuff(x, my_list=None):
    if my_list is None:
        my_list = []
    my_list.append(x)
    return my_list

print(add_stuff(1))
print(add_stuff(2))
~~~
This way, each call to `add_stuff` will have its own independent list, preventing the unintended sharing of mutable objects.
~~~bash
[1]
[2]
~~~

## Yes but No
Back in Python 2, you could do something truly bizarre:

~~~python
True = False
print(True)
~~~
~~~bash
False
~~~

Yep, you could make True become False. Why? Because in Python 2, True and False were just variables, not keywords. Thankfully, Python 3 fixed this nonsense.

~~~bash
Traceback (most recent call last):
  File "<main.py>", line 1
    True = False
    ^^^^
SyntaxError: cannot assign to True
~~~

## 0.1 + 0.2 Ain't 0.3

I mean, it isn't! (in Python)

~~~python
print(0.1 + 0.2 == 0.3) # should return True..
~~~
~~~bash
False
~~~
~~~python
print(0.1 + 0.2) # then what is it?
~~~
~~~bash
0.30000000000000004
~~~

Decimal fractions like 0.1 can't be stored exactly in binary, so you get tiny rounding leftovers. The only way to fix this is to round the results, or use the `decimal` library.

~~~python
print(round(0.1 + 0.2, 2))
~~~
~~~bash
0.3
~~~
~~~python
from decimal import Decimal
print(Decimal('0.1') + Decimal('0.2') == Decimal('0.3'))
~~~
~~~bash
True
~~~

## The Loop-Lambda Surprise

Make functions in a loop and expect each to remember its own number? Python gives them the last one.

~~~python
funcs = [lambda: i for i in range(3)]
for f in funcs:
    print(f())
~~~
~~~bash
2
2
2
~~~

Why? Well, those lambdas all look at the same name i, which ends up as 2. Quick fix: lock the value in a default argument, like this:

~~~python
funcs = [lambda i=i: i for i in range(3)]
for f in funcs:
    print(f())
~~~
~~~bash
0
1
2
~~~

## Copying a List with *

Using * to "copy" a list with mutable items makes them all point to the same thing.

~~~python
rows = [[0]] * 3
rows[0][0] = 1
print(rows)
~~~
~~~bash
[[1], [1], [1]]
~~~

Confusing isn't it? Each row is the same inner list. Use a comprehension to make independent rows:

~~~python
rows = [[0] for _ in range(3)]
rows[0][0] = 1
print(rows)
~~~
~~~bash
[[1], [0], [0]]
~~~

There you go!

## Sneaky Booleans!

True and False act like 1 and 0 for a reason, but sometimes they can go nuts.

~~~python
print(True + True)
print(True * 5)
~~~
~~~bash
2
5
~~~

There's no real point in this, just a cool quirk ;)

Well well well, enjoy these little quirks about Python! Now you know, the Python we all know and love sometimes doesn't make any logic sense.
