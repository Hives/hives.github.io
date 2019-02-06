---
layout: post
title: Precourse Week 1 - Command Line
date: 2019-02-06 17:00:00 +0000
categories: [makers]
tags: [precourse, command line, bash]
---
After spending a couple of days fiddling with this blog, I thought I ought to do
some work, so here we go with Week 1 of the precourse. The first lesson is an
introduction to the command line.

Lessons 1-16 are on the following **basic** shell commands, including how they
use parameters and switches where appropriate:
- `date`
- `pwd` = "print working directory"
- `ls`
- `cd`
- `touch`
- `mkdir`
- `rmdir`
- `rm`
- `cp`
- `mv`
- `cat`, also in conjunction with `>` to redirect output to a file
- `less` for viewing long files
- `head` and `tail` for viewing the start and end of long files. `tail` in
particular is useful for monitoring log files
- using man pages to get help on commands

Lessons 17-31 were on **advanced** commands. This included:
- Streams: #0 = stdin, #1 = stdout, #2 = stderr
- Pipes and redirection, e.g. `cat file.txt | less`, `ls -lA | less`, `cat
file1.txt > file2.txt`
- Wildcards, e.g `ls new*.txt`, `ls *`, `ls *n*`.
  - Also introduced `find`, to find files in the current directory and sub
  directories (e.g. `find . -name "*.txt" -print` - don't forget the quotes
  around `"*.txt"`)
  - ...and `grep`. 
- "Very brief mention of regular expressions" 😬: e.g. the example given was
`find ~ -name "*" -print | grep "\d\+"` in which grep is taking a regular
expression as an input, `\d+\`, which will find all files that have a number in
the filename. This didn't work on my machine - it found all files with a "d" in
the filename. Some Googling reveals that regular expressions come in different
flavours and can behave differently in different contexts, and an alternative
regex which worked for me was `[0-9]\+` or
`[[:digit:]]\+`.
  - The lesson suggested checking out <https://regexr.com/> as a tool to learn
  more about regular expressions.
- Counting words and lines with `wc`
- Permissions
  - `whoami`
  - "user", "group" and "other" classes of permissions
  - read, write and execute permissions
  - viewing permissions with `ls -l`
  - changing permissions with `chmod`, including making a file executable
- Shebangs aka hashbangs: `#!` Used at the beginning of an executable file to
tell the system what program to use to run it. In the
example given, we used a shebang to load the environment and use the default
version of ruby. It didn't go into too much detail about how that works, but
here's the example:
```ruby
#!/usr/bin/env ruby
puts "Hello, world!"
```
- Superuser mode, i.e. `sudo`, including a quick mention of `sudo rm -rf /*`
**(NEVER DO THIS!)** to emphasise the need to be careful 😆
- Environment: use `env` to see all environment variables, and e.g. `echo $PATH`
to view any single environment variable.
- Echo: seems trivial, but simple commands like `echo "some string"` and `echo
"some string" > file.txt` can come in useful...
- PATH: This is the name of the environment variable which stores the path, the
colon-separated list
of directories where the system will look for programs you ask it to run. The
system will search in the folders in order from first to last.
- Setting environment variables: e.g. `export SEASON=winter`, `export
PATH=$PATH:$HOME/my-folder`. By convention the names of environment variables
are ALLCAPS. Example use case given was storing secret data like passwords that
you need to access in a program, but you don't want to store in the code where
anyone else can access it.
- Profile files: e.g. .bash\_profile, or .zshrc for Z shell. Amongst other
things, used to set up 'permanent' environment variables.
- Processes: `ps` by default shows processes with the same user ID and
associated with the current terminal, `ps x` shows all processes on the
computer.
- Vim: the modal text editor that we all know and love.

Finally there were some optional materials:
- [Unix Tutorial for Beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/)
- [Learn Unix the hard way](https://learncodethehardway.org/unix/)
