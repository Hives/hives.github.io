---
layout: post
title: Precourse Week 4, pairing on FizzBuzz
category: makers
tags: ruby, fizzbuzz, tdd, rspec, git, github, pair programming
---

Today I met up with [Cosmin][cosmins-github], another Makers candidate in my
cohort, to do some work together. We decided to make an early start on the work
for Week 4, the first exercise of which was pair-programming FizzBuzz using a
Test Driven Development (TDD) process.

The teachable.com page for the exercise is
[here](https://makersacademy.teachable.com/courses/256825/lectures/3989229>).

Used exercise 1 here to set up a collaborative repo:
<https://uoftcoders.github.io/studyGroup/lessons/git/collaboration/lesson/>
Here's the repo:
<https://github.com/micosmin/FizzBuzz>

require doesn't need the extension? read up on this

> It's important to question scenarios like the one above and not simply accept
> that they work 'by magic'. Do some research online - try to understand what's
> happening behind the scenes. In this case, RSpec actually adds lib to its
> LOAD_PATH by default. This means that it will look for required files in lib
> automatically, which is why we can simply  require 'fizzbuzz'. Ruby will infer
> the .rb extension if it is omitted, so this is optional too.

Good command we learnt:
git checkout --patch pauls-branch3 spec/fizzBuzz_spec.rb

Used this to push my branch to GitHub (what does it mean?):
git push --set-upstream origin pauls-branch3

[cosmins-github]:https://github.com/micosmin
