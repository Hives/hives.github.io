---
layout: post
title: Precourse Week 1 - Version Control
date: 2019-02-07 16:51 +0000
category: makers
tags: 
---

The next chunk of lessons are about version control.

## Git

An introduction to the concept of version control, and some basic git concepts
like what a repository is, the staging area, and commits.

Commands include
- `git init`
- `git add`
- `git rm`
- `git status`
- `git commit -m "Commit message"`
- `git log`
- and `git checkout` to look at earlier commits.

## GitHub

Lesson 42 stressed that "as a developer, you are your GitHub profile", and that
it's the first thing potential employers will check. It recommends that Makers
students use git and GitHub for all the code we write from here on. It also says
to treat it like a CV, i.e. add a picture and your real name. So I've added my
real name. I like my current profile pic too much to change it at the moment
though...

Example of a basic git + GitHub workflow:
1. `git init` a local repo
2. create a repo on GitHub
3. `git remote add origin URL_OF_GITHUB_REPO` to set it as a remote to the local
repo
4. `git push -u origin master` pushes changes, and saves "origin master" as
default push and pull parameters
5. next time can just do `git push`
6. make some changes to the remote repo, and pull them down with `git pull`

The importance of meaningful commit messages was stressed, and the [commit
messages of the jQuery project][jquery-commits] were given as a good example.

## $BONUS

Many optional extras were given for learning more about git:

<https://makersacademy.teachable.com/courses/256825/lectures/3989174>

## Learning objectives

The final learning objectives included some concepts not yet dealt with,
including:
- how branching works, including merging
- forking
- topic branches
- pull requests

Some more research to do there then.

[jquery-commits]: https://github.com/Hives/playing-with-git.git
