---
layout: post
title: Blogging workflow
date: 2019-03-03 22:15 +0000
categories: [makers, metablogging]
tags: [jekyll, vim, markdown]
---

Some notes on how I'm writing drafts/posts and managing the blog.

## Jekyll stuff

As mentioned before I'm using the [jekyll-compose] gem to create and publish
posts from the command line. The commands are:

```shell
bundle exec jekyll draft "My draft name"
bundle exec jekyll post "My post name"
bundle exec jekyll publish path/to/a/draft
```

But I've made aliased for those commands: `draft`, `post` and `publish`. The
draft and post commands are configured in the site's `_config.yml` to auto-open
in my default editor (vim).

I've added various basic features to the site (see posts passim), but I'd still
like to add a search function and maybe line numbers on code blocks. I guess
we'll have to see if I've got time for that once I'm into the course.

## Vim stuff

I'm using vim to write and edit posts, in the spirit of 'keeping close to the
command line'. I made some tweaks to my vim setup to help with writing blog
posts and markdown in general:

### Line wrapping

I've been using hard line wrapping because I tend to have my terminal windows
quite large (~150 characters wide) since I'm working on a large monitor, and I
don't like to have to resize the window to get readable lines of text in vim. I
set hard line wrapping at 80 characters for markdown files like this:
```vimscript
au BufRead,BufNewFile *.md setlocal textwidth=80
```

It's not perfect, as it can get mixed up if you're typing in the middle of a
paragraph. When this happens you can force reformatting (`vip` = select inside
paragraph, and `gq` = reformat), but this is slightly annoying...

There are vim plugins that aim to improve the text wrapping, e.g. Vim pencil
might be worth investigating.

Or there's [Goyo]'s distraction-free mode, which is good but removes too much of
the UI that I'd rather keep.

Or would it be better to go with soft wrapping à la [Greg
Hurrell][wincent-static-blog-vid]? This might be more appropriate once I'm
working on the laptop I'm going to be borrowing off Makers, since It'll have a
smaller screen than the huge one I'm working on at the moment, so I'll probably
have to be more economical with my screen real estate.

### Spell checking

Apparently vim has built in spellchecking! Very useful. Turn it on with:

```vimscript
autocmd BufRead,BufNewFile *.md setlocal spell
```

Use `zg` to add words to the dictionary.

`[s` goes to previous misspelled word, `]s` to next.

### Good plugins

I used the [UltiSnips] plugin in vim to create a snippet which inserts the date
in the right format in a post's front matter so I can easily update a draft's
date when I publish it.

[FZF] is a great fuzzy finder for the command line, which can be used inside
Vim. I've got it bound to `ctrl-p`, so I can open vim in the root folder of my
blog, run it, and very quickly search for and open drafts and posts by typing
words from the filename. I've found this also to be a useful way of navigating
between different files in larger projects.

[UltiSnips]:https://github.com/SirVer/ultisnips
[jekyll-compose]:https://github.com/jekyll/jekyll-compose
[wincent-static-blog-vid]:https://www.youtube.com/watch?v=fTyfevqIuJA
[Goyo]:https://github.com/junegunn/goyo.vim
[FZF]:https://github.com/junegunn/fzf
