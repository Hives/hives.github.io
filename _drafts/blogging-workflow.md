---
layout: post
title: Blogging workflow
categories: makers
tags: [jekyll, vim, markdown]
---

Editing markdown in vim:
- Line wrapping, sorta: `au BufRead,BufNewFile *.md setlocal textwidth=80`
  - Only works while you're typing. Otherwise select text and use `gq` to
  reformat.
  - Vim pencil plugin as alternative text wrapping method?
  - Or soft wrapping à la Greg Hurrell?
- Spellcheck! `autocmd BufRead,BufNewFile *.md setlocal spell`
  - Use `zg` to add words to dictionary
  - `[s` goes to previous misspelled word, `]s` to next
- Use Goyo to soft wrap text at 80 characters, with some modifications?
  - http://makble.com/vim-distraction-free-mode
- Use liquid's {% raw %}`{% raw %}`{% endraw %} tag to allow Liquid code blocks
to display without executing

Other good vim stuff I learned:
  - `it` = 'inner tag block' - selects inside of a HTML or XML block
  - `at` = 'a tag block' - same as above but selects tags too

Creating / publishing posts:
- create drafts/posts using jekyll-compose
  - use `bundle exec jekyll draft` and `bundle exec jekyll draft`
  - publish drafts with `bundle exec jekyll publish`
  - create aliases for those commands
- use a vim snippet ([UltiSnips][ultisnips]) to insert date into front matter
  - UltiSnips and YouCompleteMe default behaviour conflicts. Resolved by mapping
  UltinSnips' expand snippet to ctrl-j
- can use FZF vim plugin to find and edit posts quickly

Blog features wishlist
- Next/prev links to click through posts
- Tags and categories pages
- Search? there are some plugins that do client-side search

[ultisnips]:https://github.com/SirVer/ultisnips
