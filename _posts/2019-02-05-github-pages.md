---
layout: post
title: Hosting on GitHub pages
date: 2019-02-05 21:15 +0000
categories: [makers]
---

Turns out that GitHub pages runs on Jekyll, so it's easy to host your Jekyll
site on GitHub.

It works something like this:
1. Create a GitHub repo with a special name: XXXX.github.io where XXXX is
   whatever name you want to use.
2. Set up a Jekyll site on your local machine and initialise a git repo in its
   root folder.
3. Connect the local repo to the GitHub repo (e.g. `git remote add origin
   https://github.com/YOUR-USERNAME/XXXX.github.io`).
4. The site should now appear at XXXX.github.io. You can edit it on your local
   machine, checking it using Jekyll's local server (`bundle exec jekyll serve`)
   and then publish changes with a `git push`. (Updates can take a couple of
   minutes to appear.)

Here's the GitHub repo for this site:
<https://github.com/Hives/hives.github.io>

One tricky thing was that GitHub pages requires Jekyll use a gem called
'github-pages', which doesn't seem to be compatible with the latest version of
Jekyll, so you need to specify an older version of Jekyll when setting up your
site.

I found this page pretty helpful in getting this set up:
<https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/>

