---
layout: post
title: Precourse Weeks 2 and 3, Ruby learning objectives - other stuff
date: 2019-02-19 23:26 +0000
category: makers
tags: ruby
---

After looking at blocks, procs and lambdas there were a couple of other odd bits
that came up in the precourse weeks 2 and 3 that I wanted to make some notes on.

## "Splat" operator (\*)

The `*` operator (sometimes called 'splat') "does a kind of unwrapping of its
operand into its components", according to The Well-Grounded Rubyist.

You can use it to write methods which don't mind how many arguments they get:

```ruby
def splat_my_args(a, b, *args)
  p args
end
splat_my_args(1, 2, "woah", 666, :wtf) # outputs ["woah", 666, :wtf]
```

So in this case it sponges up the spare arguments into an array.

You can also do gnarly things like this:

```ruby
first, *middle, last = [0,1,2,3,4,5,6]
p first # outputs 0
p middle # outputs [1, 2, 3, 4, 5]
p last # outputs 6
```

So the `middle` variable here takes the middle elements and turns them into a
new array.

Looks like there's lots of cool stuff you can do with a splat, so watch out for
it.

## Double splat (\*\*)

Introduced in Ruby 2.0, the double splat is like the single splat but for
hashes. E.g.:

```ruby
def doublesplat(**args)
  p args
end
doublesplat(one: 1, two: 2, three: 3)
# outputs:
#   {:one=>1, :two=>2, :three=>3}
```

## Parallel assignment

In many (most?) programming languages, if you want to swap the values of two
variables, you have to use a temporary variable:

```c
int a = 1;
int b = 2;
int temp;

temp = a;
a = b;
b = temp;
```

But Ruby can do it much more cleanly, like this:

```ruby
a, b = b, a
```

This is called parallel assignment. The way this works is that that in an
assignment each value on the right hand side is evaluated from left to right,
and only after that is completed does the assignment take place. You can see
this clearly with this example:

```ruby
x = 0
a, b, c = x, (x += 1), (x += 1)
# now a == 0, b == 1 and c == 2
```

Check [this page][parallel-assignment-examples] for some interesting examples of
stuff you can do with parallel assignment combined with the splat operator.

## Shovel operator

I remember this was covered in the Codeacademy Ruby course I did to prepare for
my Makers interview, but then I completely forgot about it. So to refresh my
memory - the 'shovel' operator, `<<`, adds things onto the end of other things.

For arrays it's equivalent to `.push`, and can be chained:

```ruby
[1, 2] << "c" << "d" << [3, 4]
# => [1, 2, "c", "d", [3, 4]]
```

For strings it's equivalent to `.concat`, and can also be chained:

```ruby
"hello " << "world" << "!"
# => "hello world!"
```

This differs from using `+=` in that `a += b` is equivalent to `a = a + b`,
which creates a new object and assigns it to `a`, whereas `a << b` modifies `a`
itself without creating a new object. As a result, `<<` is significantly
faster, at least according to [this guy on StackExchange][shovel-benchmark], and
so is often the preferable way to join stuff together. Speed is not the only
consideration though, and in some situations `"String #{INTERPOLATION}"` will be
more readable, for example.

[parallel-assignment-examples]:https://www.linuxtopia.org/online_books/programming_books/ruby_tutorial/Ruby_Expressions_Parallel_Assignment.html
[shovel-benchmark]:https://stackoverflow.com/a/28618941
