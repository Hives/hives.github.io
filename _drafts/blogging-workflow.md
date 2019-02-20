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
  - Vim pencil plugin as alternative text wrapping method?
  - Or soft wrapping à la Greg Hurrell?
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
  - had to use [Supertab][supertab] to make this play nicely with YouCompleteMe,
  which has messed up tab behaviour in the latter. Can this be fixed?

Blog features wishlist
- Next/prev links to click through posts
- Tags and categories pages
- Search? there are some plugins that do client-side search

[ultisnips]:https://github.com/SirVer/ultisnips
[supertab]:https://github.com/ervandew/supertab
