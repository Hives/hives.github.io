---
layout: post
title: Precourse Weeks 2 and 3, Ruby learning objectives - lambdas
date: 2019-02-19 21:44 +0000
category: makers
tags: ruby, lambdas
---

The final big topic I wanted to look at from the precourse weeks 2 and 3
[learning objectives][teachable.com] was lambdas. Shout out again to David
Black's The Well-Grounded Rubyist.

## Lambdas

A lambda is a proc with some "special internal engineering". We create one by
passing a block to the `lambda` method, and it returns a lambda with the block
as the function body:

```ruby
lam = lambda { puts "I'm a lambda!" }
p lam # outputs #<Proc:0x0000559edb44cfa8@(irb):1 (lambda)> 
lam.call # outputs "I'm a lambda!"
```

The inspect string `#<Proc:...` shows that the object returned by `lambda`
is from the class `Proc`, but the `(lambda)` at the end indicates that it's a
special lambda flavoured proc.

Lambdas differ from normal procs in three ways. First, they can only be created
explicitly. Remember how we could create a proc by passing a block to a method
using the `&` syntax, e.g. with `def my_method(&block)`? Well that's implicit
creation of a proc, which means it's just a normal proc, not a lambda.

Second, they treat the `return` keyword differently. In a lambda `return` will
exit from the body of the lambda back into the code from which the lambda was
called. But calling `return` inside a proc triggers a return from the method in
which was the proc was called. So in this example the second `puts` won't
output, because the `return` in the proc will cause the containing method to
exit:

```ruby
def proc_lambda_return_test
  l = lambda { return }
  l.call
  puts "Still running"
  p = proc { return }
  p.call
  puts "You won't see this"
end
proc_lambda_return_test

# output:
#  Still running
```

Thirdly, they are fussy about getting the right number of arguments. Too many or
too few will throw an error.

### The 'stabby lambda' constructor

An alternative syntax for creating lambdas, nicknamed the "stabby lambda", is
like this:

```ruby
lam = -> { puts "I'm a lambda!" }
lam.call # outputs "I'm a lambda!"
# if you want to use arguments, do it like this:
lam2 = ->(x,y) { x * y }
lam2.call(7, 8) # outputs 56
```

This exists for historical reasons (prior to Ruby 1.8 the parser had trouble
with method-style argument syntax inside pipes for lambdas) which no longer
pertain, so the stabby syntax is no longer necessary. Apparently you still see it
used fairly widely though.
