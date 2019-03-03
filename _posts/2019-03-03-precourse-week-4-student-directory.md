---
layout: post
title: Precourse Week 4, student directory
date: 2019-03-03 23:13 +0000
category: makers
tags: [ruby, reading, writing, csvs]
---

The main piece of work for week 4 of the precourse was writing a program to
allow a user to enter a list of students with some metadata (e.g. a cohort)
attached to each one, save it to a file, and load it again, with various bells
and whistles to make the process more user-friendly. My work is in this repo
<https://github.com/hives/student-directory/>

Here's some new stuff that was covered:

## Magic numbers

A magic number is a unique numerical value with unexplained meaning. In general
these are bad for readability and maintainability. Check this pseudocode card
sorting example from [Wikipedia][magic-numbers-wiki]:

```
 for i from 1 to 52
   j := i + randomInt(53 - i) - 1
   a.swapEntries(i, j)
```

Compared to:

```
constant int deckSize := 52
for i from 1 to deckSize
  j := i + randomInt(deckSize + 1 - i) - 1
  a.swapEntries(i, j)
```

The second version is more readable because the variable name tells us what the
number `52` means, and if we want to change the value we only need to do it in
one place.

## '@' variables, how do they work?

Have used these before, but couldn't remember exactly how they worked... A
variable with a name like `this` is a **local variable**. Local variables are
not available to methods defined in the same scope as the variable:

```ruby
x = 10
def my_method
  p x
end
my_method # throws an error - undefined local variable or method 'x'
```

A variable with a name like `@this` is an **instance variable**. Instance
variables are available to methods defined in the same scope:

```ruby
@x = 10
def my_method
  p @x
end
my_method # prints '10'
```

To be precise, instance variables exist inside a particular object, and are
accessible everywhere inside it.

There are also **class variables** which have names like `@@this`. Class
variables exist inside a class, and all objects which inherit from that class
have access to it. Two objects which belong to the same class can have different
values of their instance variables, but their class variables are the same.

## File.open - for reading and writing

This was the first time I had seen reading and writing files in Ruby. In the
exercise I did something like this for saving:

```ruby
file = File.open("hi.txt", "w")
file.puts "Some string"
file.close
```

The `"w"` parameter given to the `File.open` method indicates that the file
should be open in write-only mode - trying to read it will throw an error.

Notice that we print into the open file using puts. `puts`ing without a
receiver prints to `STDOUT`, but `file.puts` prints into the file.

Note also that we need to close the file after we're done with `file.close`.
(Why??)

Opening a file in write-only mode will erase the contents. If you want to append
to the existing contents you need append mode, specified with the `"a"`
parameter. [Ruby file open modes].

Similarly we can read files like this:

```ruby
file = File.open("hi.txt", "r")
file.readlines.each do |line|
  puts line
end
file.close
```

The `r` parameter to `File.open` indicates we're opening the file in read-only
mode. Again we have to close it at the end with `file.close`.

## Block method for reading/writing files

More idiomatic than using `file = File.open` however is to pass a block to
`File.open`, like this:

```ruby
File.open("hi.txt", "r") do |file|
  file.readlines.each do |line|
    puts line
  end
end
```

## Ruby's csv library

In the example we were working with rows and columns of data in the
'comma-separated value' format, and Ruby has a library for that. So for example,
I rewrote my save method as something like:

```ruby
require 'csv'
# ...
def save_students
  filename = 'students.csv'
  CSV.open(filename, "wb") do |csv|
    @students.each do |student|
      csv << [student[:name], student[:cohort]]
    end
  end
end
```

The library has got lots of natty methods for working with .csv files:
<http://ruby-doc.org/stdlib-2.0.0/libdoc/csv/rdoc/CSV.html>


## Command line arguments

We can pass command line arguments when calling a Ruby program, and they are
available in the `ARGV` array. E.g. save this code as `print_arguments.rb`:

```ruby
p ARGV
```

and call it from the command line like this:

```shell
ruby print_arguments.rb -v somefile.txt
#=> ["-v", "somefile.txt"]
```

We used this in the students directory example to pass a file to the program to
be read.

## 'gets' gotcha

We're used to using `gets` to get input from the user. But `gets` will read from
the list of files given as command line arguments via the `ARGV` array before it
will get input from the user. In which case it may not behave like you expect.
[See the documentation on gets][gets-docs].

You can explicitly tell Ruby to get input from the keyboard by doing:

```ruby
STDIN.gets
```

So if there's a possibility that your program have a file passed to it on the
command line, you'll need to use `gets` like this.

[Ruby file open modes]:https://ruby-doc.org/core-2.2.2/IO.html#method-c-new-label-IO+Open+Mode
[gets-docs]:http://ruby-doc.org/core-2.3.1/Kernel.html#method-i-gets
