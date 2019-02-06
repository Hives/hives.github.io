---
layout: post
title: Blogging workflow
categories: [makers]
tags: [jekyll, vim, markdown, metablogging]
---
Editing markdown in vim:
- Line wrapping, sorta: `au BufRead,BufNewFile *.md setlocal textwidth=80`
  - Only works while you're typing. Otherwise select text and use `gq` to
  reformat.
- Spellcheck! `autocmd BufRead,BufNewFile *.md setlocal spell`
  - Use `zg` to add words to dictionary
  - `[s` goes to previous misspelled word, `]s` to next

