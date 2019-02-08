---
layout: post
title: Precourse Week 1 - The Command Line Murder
date: 2019-02-08 18:53 +0000
category: makers
tags: 
sitemap: false
---

The final part of Week 1 was an exercise to test knowledge of the command line
and git. We started by forking and cloning a GitHub repo, which contained
various huge text files which had to be filtered using various command line
tools (`cat`, `grep`, `ls`, `wc`, `find`, `head`, `tail` etc. combined with
pipes) to reveal a series of clues to a murder.

At one point we had to cover our tracks by merging an alternative branch into
the master branch, and we let the Chief know we were making progress in the
investigation with a pull request. Ingenious!

One interesting thing I hadn't seen before was using grep with flags to output
context around the line containing the match. From the Detective's Handbook:

> `grep -A N SEARCH_STRING` outputs not only the line that contains a match but also
> N lines after that one.
> 
> `grep -B N SEARCH_STRING` is like -A but prints out N lines before the line
> with the match.
> 
> `grep -C N SEARCH_STRING` outputs N lines before and after the match string.

More info in `man grep`.
