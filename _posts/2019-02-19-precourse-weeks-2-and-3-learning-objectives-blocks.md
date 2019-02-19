---
layout: post
title: Precourse Weeks 2 and 3, Ruby learning objectives - blocks
date: 2019-02-19 20:29 +0000
category: makers
tags: ruby, blocks
---

There were some topics in the precourse weeks 2 and 3 [learning
objectives][teachable.com] which reminded me of some stuff that was covered in
the CodeAcademy Ruby course I did to prepare for the Makers interview, but which
I realised I had forgotten. So I refreshed my memory by looking up blocks, procs
and lambdas and a couple of other topics in David Black's The Well-Grounded
Rubyist, which seems like a great resource for getting into the nitty-gritty with
Ruby. This ended up being quite long, so I'll break it up into a number of
posts.

First up:

## Blocks

A block is an anonymous function that can be passed to a method. They are
delimited by braces, `{ ... }`, or by `do ... end`. They can receive parameters
surrounded by pipes: `{ |e| some_code_here }`.

You pass a block to a method by doing something like this:

```ruby
5.times { |i| puts "I'm on iteration #{i}" }
```

We say the method **yields** to the block. You can pass a block to any
method call in Ruby, but not all of them will do anything with it 🙂. N.b. a
code block passed to a method is not an argument. It's its own thing.

It's possible to write your own methods which will yield control to a code block
by using the `yield` keyword, e.g:

```ruby
def my_method
  puts "Start of method"
  yield("John", 2)
  puts "End of method"
end

my_method { |name, age| puts "#{name} is #{age} years old" }

# outputs:
#   Start of method
#   John is 2 years old
#   End of method
```

This example calls a method and passes it a code block. When the method reaches
`yield` it yields control to the block, and passes it two parameters. When the
block has finished executing control is returned to the method.

### Block variable scope

The way blocks deal with variable scope is slightly more complicated than methods: 

#### Variables from the outer scope

Blocks share local scope with the code that precedes them. In other words, if
you define `x` before the block, and then refer or assign to `x` inside the
block, the `x` you're dealing with is the same one that existed prior to the
block, e.g.

```ruby
x = 100
1.times do
  puts x # output is 100
  x = 200
  puts x # output is 200
end
puts x # output is still 200
```

#### Block parameters (local)

However, if a block parameter is given the same name as a variable that already
exists, they will remain distinct:

```ruby
x = 100 # outer x
[1,2,3].each do |x| # block parameter is called x
  puts "Parameter x is #{x}" # 1, 2, 3
  x = x + 10
  puts "Reassigned x in block, now it's #{x}" # 11, 12, 13
end
puts "Outer x is still #{x}" # 100
```

In this case the `x` inside the block is different from the `x` outside the
block.

#### Block variables (local)

Sometimes you may want to use a variable inside a block without worrying that
you might clobber a variable in the outer scope which has the same name. You can
do this by using *reserved names*, indicated by using a semicolon to separate
names in the parameter list. The variables before the semicolon are parameters,
the variables after the semicolon are temporary variables local to the block:

```ruby
x = 100 # outer x
3.times do |i; x| # i is a parameter, x is a block-local variable
  x = i # assign to the block-local x
  puts "x in the block is now #{x}"
end
puts "x after the block ended is #{x}" # still 100 - the outer x is unchanged
```

You don't need parameters either, so this is apparently valid: `{ |; x|
x_is_now_local_to_the_block }`

[teachable.com]:https://makersacademy.teachable.com/courses/256825/lectures/3989238
