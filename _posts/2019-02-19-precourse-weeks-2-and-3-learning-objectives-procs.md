---
layout: post
title: Precourse Weeks 2 and 3, Ruby learning objectives - procs
date: 2019-02-19 21:15 +0000
category: makers
tags: ruby, procs
---

After blocks, the next topic I wanted to go over from the precourse weeks 2 and
3 learning objectives was procs. Again, my main reference here was David Black's
The Well-Grounded Rubyist.

## Procs

A proc is a way of turning a code block into an object, so you can store it,
pass it around as a method argument (remember blocks can only be passed
directly, not as an argument), and call it.

You create a proc by passing a block to

1. `Proc.new` or
2. the `proc` method.

You call it using the `call` method.

```ruby
pr1 = Proc.new { puts "Inside a Proc's block" }
pr2 = proc { puts "Inside another Proc's block" } 
pr1.call # outputs "Inside a Proc's block"
pr2.call # outputs "Inside another Proc's block"
```

Both these ways of creating a proc are equivalent (prior to Ruby 1.9 they were
slightly different). The code block becomes the body of the proc.

Because a proc is an object (blocks are not!), you can now use it to pass the
code block to methods as an argument:

```ruby
pr = Proc.new { puts "Inside a Proc's block" }

def my_method (a)
  a.call
end

my_method(pr) # outputs "Inside a Proc's block"
```

We saw in the previous section that you can pass a code block to a method, and
then run it from inside the method using the `yield` keyword. You can also write
a method that will take a block and convert it into a proc to use internally,
using this `&` syntax:

```ruby
def block_to_proc(&block)
  block.call
end
block_to_proc { puts "Inside the block" } # outputs "Inside the block"
```

The `&` tells the block to take the block and do something like `Proc.new` on it
to turn it into a proc. Note that the syntax for how you pass the block to the
method is the same as if you were going to call it using `yield`.

So we can pass a block to a method and have the method convert it to a proc. But
guess what - we can also pass a proc to a method and have the method convert it
to a block:

```ruby
def proc_to_block
  yield
end
pr = Proc.new { puts "Inside the proc" }
proc_to_block(&pr)
```

Just as the `&` in front of a parameter in a method definition tells the method
to expect a block and to convert it into a block, the `&` in front of the
argument when calling a method tells the method to expect a proc, and to use it
instead of a code block.

There was a lot more in the book along these lines. I think it's mostly
presented to illustrate the dynamic and expressive power of the language, and
I can't see how practically useful it is...

I guess you could use the last two examples together in a practical way to pass
either a block or a proc to a method depending on the situation, like this:

```ruby
def can_take_block_or_proc(&block)
  block.call
end
can_take_block_or_proc { puts "I'm a block" } # outputs "I'm a block"
pr = Proc.new { puts "I'm a proc" }
can_take_block_or_proc(&pr) # outputs "I'm a proc"
```

So in this example the `&` in the method definition converts a block input into
a proc. But the `&` in front of the argument in the method call on the final
line converts the proc into a block. So it gets converted from a proc to a block
when calling the method, and then back to a proc inside the method. 😖 This
flexibility might come in useful for something??

### Procs as closures

Blocks have access to variables which were in scope at the point they were
created. Since a proc is a block which has been made into an object, the same
rule applies.

But unlike blocks, procs can be stored and reused multiple times. Whenever the
proc is called it has access to all variables which were in scope at the point
it was created. So not only can procs be used to pass blocks around, they pass
the local context around too.

```ruby
def call_a_proc(pr)
  string = "string from the method scope"
  puts string # (2
  pr.call # (3)
end
string = "string from the outer scope"
pr = Proc.new { puts string }
pr.call # (1)
call_a_proc(pr)
# outputs:
#   "string from the outer scope" (1)
#   "string from the method scope" (2)
#   "string from the outer scope" (3)
```

In this example the string from the outer scope is preserved when then the proc
is passed into the method, even though the `string` variable is redefined inside
the method.

A piece of code which carries its context around with it like this is called a
closure. Closures are an important concept in programming.

According to *The Well Grounded Rubyist*, "the classic closure example is a
counter":

```ruby
def make_counter
  n = 0
  return Proc.new { n += 1 }
end
counter1 = make_counter
puts counter1.call
puts counter1.call
counter2 = make_counter
puts counter2.call
puts counter1.call
# outputs:
#   1
#   2
#   1
#   3
```

In the example `make_counter` returns a proc, which when called increments the
variable `n` by 1 and returns it. In the context in which the proc is created,
`n` is equal to 0. So the first time the proc is called it returns 1, then 2,
and so on. When a second counter is initialised by calling the method again, the
second method call represents a new local scope, so the `n` which gets passed to
the second proc is a different `n` to the one in the first proc. So after
calling the second counter, we can call the first counter again and it will
continue where it left off.

### Procs with arguments

The same as with any code block, a proc can be defined to take an argument. They
are less fussy than methods about whether they receive the right number of
arguments. If called with too few arguments the spare parameters get set to
`nil`. If called with too many then the extra ones are discarded:

```ruby
pr = Proc.new { |x| p x }
pr.call("Hello")
# outputs:
#   "Hello"
pr.call
# outputs:
#   nil
pr.call("Hello", "Goodbye")
# outputs:
#   "Hello"
```
