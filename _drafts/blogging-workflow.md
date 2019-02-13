---
layout: post
title: Blogging workflow
categories: makers
tags: jekyll, vim, markdown
---
Editing markdown in vim:
- Line wrapping, sorta: `au BufRead,BufNewFile *.md setlocal textwidth=80`
  - Only works while you're typing. Otherwise select text and use `gq` to
  reformat.
- Spellcheck! `autocmd BufRead,BufNewFile *.md setlocal spell`
  - Use `zg` to add words to dictionary
  - `[s` goes to previous misspelled word, `]s` to next
- Use Goyo to soft wrap text at 80 characters, with some modifications?
  - http://makble.com/vim-distraction-free-mode

Creating / publishing posts:
- create drafts/posts using jekyll-compose
  - use `bundle exec jekyll draft` and `bundle exec jekyll draft`
  - publish drafts with `bundle exec jekyll publish`
  - create aliases for those commands
- use a vim snippet ([UltiSnips][ultisnips]) to insert date into front matter

[ultisnips]:https://github.com/SirVer/ultisnips
