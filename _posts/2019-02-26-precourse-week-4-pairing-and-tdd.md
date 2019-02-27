---
layout: post
title: Precourse Week 4, pair programming, TDD
date: 2019-02-26 23:36 +0000
category: makers
tags: [precourse, pair programming, TDD]
---

Today I met up with my mentor [Luca][lucas-github]. We did some pair programming
on a simple exercise - write a method which takes a string and returns the
middle character, or the two middle characters if it's even in length. We used a
test driven development (TDD) approach, using Rspec.

## Driver/navigator pair programming

At Luca's suggestion we used the driver/navigator method. One of us would be the
navigator, giving instructions to the driver, the driver typing code and
terminal commands into the computer according to the instructions. Luca set a
timer and we switched role every 15 minutes.

This has the benefit of meaning you're both engaged on the problem - the one not
on the keyboard can't zone out. It also meant that the navigator could focus on
defining the algorithm, while the driver was specifying the exact syntax. This
probably has advantages where one or both of you are less experienced as the
division of labour allows each programmer to deal with a smaller area, although
apparently in the 'strong' form of driver/navigator pairing the driver shouldn't
type anything at all that hasn't been explicitly specified by the navigator, and
if they want to contribute an idea they have to pass the keyboard over.

## Red, green, refactor, repeat

Working with Luca we used the "red, green, refactor, repeat" approach to TDD:

1. RED - Write a test that fails
2. GREEN - Write a small amount of code to pass the test
3. REFACTOR - Now the test(s) pass(es), refactor your code as appropriate
4. REPEAT - Start again with new test(s)

The idea is to keep repeating this loop, adding new tests until you've
completely defined the behaviour of your program, and you've got a program which
passes the tests.

Luca emphasised to me the importance of **working in very small steps**. This means
that when you make a mistake you'll catch it right away, and you won't have to
root through many lines of spaghetti code to find it.

So for instance, in writing our program to find the middle character of a
string, I'll give a couple of iterations to illustrate. I won't go into too much
detail about the Rspec code - I'll save that for another post.

We started with a single
test like:

```ruby
it "should return 'b' when given 'abc'" do
  expect(middle_char("abc")).to eq "b"
end
```

Running the test gave an error, since we had written no code yet. That's the Red
stage. So we wrote this code to satisfy it:

```ruby
def middle_car(string)
  "b"
end
```

Clearly this will satisfy the test, although it won't satisfy much more than
that. So we're in the Green stage. But it's important to note that even code as
apparently useless as this has the virtue of checking that your environment and
test set-up is working correctly.

There's nothing much to refactor, so let's add another test:

```ruby
it "should return 'c' when given 'abcde'" do
  expect(middle_char("abcde")).to eq "c"
end
```

Run the tests again, and now this one is failing - Red stage. Update our code:

```ruby
def middle_car(string)
  index = (string.length + 1 ) / 2 - 1
  string[index]
end
```

And this now passes - Green stage. But it won't work for a string with even
length, so we need to go through more loops to expand our tests and finish
writing the program. The exercise is left for the reader 🙂

[This blogpost about TDD][james-shore-on-tdd], as well as containing a good
summary of the principles of TDD, points up another benefit - whether you're
writing tests or code, you're always thinking about design. Writing tests is an
interface design process as you're thinking about what you put in and what you
get out, and refactoring is a code design process.

[lucas-github]:https://github.com/punchcafe
[james-shore-on-tdd]:https://www.jamesshore.com/Blog/Microsoft-Gets-TDD-Completely-Wrong.html
