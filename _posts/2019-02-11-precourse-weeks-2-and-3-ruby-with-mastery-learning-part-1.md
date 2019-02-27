---
layout: post
title: Precourse Weeks 2 and 3, Ruby with mastery learning
date: 2019-02-12 15:06 +0000
category: makers
tags: [ruby, precourse]
---

The material for weeks 2 and 3 of the precourse was 10 ruby lessons, covering
stuff like variables, control flow, objects, strings, arrays, hashes, methods
and classes. Here's some stuff that caught my brain from the lessons:

## Chapter 2: Constants

Constants are like variables, except their values cannot be changed after they
are initialised (why would you want this??). The first character of their name
must be a capital - by convention they are named in all caps, LIKE\_THIS.  

So e.g. running this:
```ruby
PI = 3.14
PI = 3.14159265359
```
produces a warning:  
```
warning: already initialized constant PI
```

N.b. variables can't be accessed outside the file they're written in, but
constants can be

## Chapter 3: Messages and interfaces

When you see `1 + 2`, `+` is a message, and `2` is the argument to that message.
So what it's actually doing is `1.+(2)`. Ruby knows to translate the former into
the latter. This is called '[syntactic sugar][wp-syntactic-sugar]'.

Anytime you run a method without specifying an object, it gets sent to `main`,
the program object. E.g. if you run `methods` in irb it will show you the
methods available to `main`.

Duck typing:
> In Ruby, we rely less on the type (or class) of an object and more on its
> capabilities. Hence, Duck Typing means an object type is defined by what it
> can do, not by what it is. Duck Typing refers to the tendency of Ruby to be
> less concerned with the class of an object and more concerned with what
> methods can be called on it and what operations can be performed on it. In
> Ruby, we would use respond\_to? or might simply pass an object to a method and
> know that an exception will be raised if it is used inappropriately.
<http://rubylearning.com/satishtalim/duck_typing.html>

## Chapter 9: Methods

Some helpful rules of thumb to help picking the right abstraction when writing
methods:
1. Can you name your method in a simple way, without using the word 'and'? Does
   it do one thing, and nothing more?
2. Can you name your method after what it returns, instead of what it does? For
   instance, `average(test_scores)` is a better name than
   `averages_scores(test_scores)`. For another example, `score(hand)` is a
   better method name than `scores_cards(hand)`.

[wp-syntactic-sugar]:https://en.wikipedia.org/wiki/Syntactic_sugar
