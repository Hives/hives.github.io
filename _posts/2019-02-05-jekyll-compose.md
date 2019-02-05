---
layout: post
title: jekyll-compose
---
Found a ruby gem called jekyll-compose which lets you create drafts, posts and pages from the command line. The command is e.g. `bundle exec jekyll draft "My new draft"` which seems like a bit of a mouthful but maybe I can make an alias for it or something... This saves the work of creating a new markdown file with the date in the title and the published time and so on. You can also set default front matter (categories, tags etc).

You can also have it open the post automatically in your favourite editor by setting this in your site \_config.yml file, which is pretty sweet:
```ruby
jekyll_compose:
  auto_open: true
```
You need to have either the $EDITOR or $JEKYLL\_EDITOR environment variable set for this to work (e.g. put `export EDITOR='atom'` in your bash profile).

So using this gem it's very quick and easy to add a new post to this blog, which is one of my main aims, so 👍 for that.

[https://github.com/jekyll/jekyll-compose](https://github.com/jekyll/jekyll-compose)

p.s. I'm not totally sure what I'm doing with these gems, how the Gemfiles work, what the 'bundle' command does and so on, but I'm going to blag it for the moment until Makers make me an expert 😎
