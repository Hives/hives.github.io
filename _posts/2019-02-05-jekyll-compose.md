---
layout: post
title: Creating new posts from the command line
date: 2019-02-05 21:30 +0000
categories: [makers]
---
I found a gem called jekyll-compose which lets you create drafts, posts and
pages from the command line:

<https://github.com/jekyll/jekyll-compose>

The command is e.g. `bundle exec jekyll post "My new post"` which seems like a
bit of a mouthful but maybe I can make an alias for it or something... This
saves the work of creating a new markdown file with the date in the title and
the published time and so on. It allows you to set default front matter
(categories, tags etc) as well.

You can also have it open the post automatically in your favourite editor by
setting this in your site \_config.yml file, which is pretty sweet: ```ruby
jekyll_compose: auto_open: true ``` You need to have either the $EDITOR or
$JEKYLL\_EDITOR environment variable set for this to work (e.g. put `export
EDITOR='atom'` in your bash profile).

So using this gem it's very quick and easy to add a new post to this blog, which
is one of my main aims, so 👍 for that.

p.s. I've been installing various gems to get this blog up and running, and I'm
not 100% sure what I'm doing - how the Gemfiles work, what the 'bundle' command
does and so on... but I'm going to blag it for the moment, and after a few weeks
of Makers hopefully I'll be an expert 😎
