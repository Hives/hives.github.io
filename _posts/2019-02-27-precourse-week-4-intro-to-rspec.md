---
layout: post
title: Precourse Week 4, intro to RSspec
date: 2019-02-27 01:25 +0000
category: makers
tags: [precourse, rspec, ruby]
---

Last week I met up with [Cosmin][cosmins-github], one of the other Makers
students in my cohort, and we did the first exercise from Week 4 of the
precourse - pair programming FizzBuzz. We used Rspec to write tests as we went
along according to the "Red, Green, Refactor, Repeat" method. I also met up with
my mentor [Luca][lucas-github] today to do something similar (see previous
post).  Here's some stuff I've learnt about Rspec.

- [Rspec core docs](https://relishapp.com/rspec/rspec-core/docs): rspec-core
provides the structure for RSpec code examples
- [Rspec expectations
docs](https://relishapp.com/rspec/rspec-expectations/docs/): rspec-expectations
is used to define expected outcomes
- [Rspec mocks docs](https://relishapp.com/rspec/rspec-mocks/docs): rspec-mocks
helps to control the context in a code example by letting you set known return
values, fake implementations of methods, and even set expectations that specific
messages are received by an object.

You can set up Rspec in a folder by running `rspec --init`. This creates some
conventional files - `spec/spec_helper.rb`, a well-commented config, and
`.rspec` which tells Rspec to `require` `spec_helper.rb` when you run it in the
folder.

Tests also go in the `spec/` folder, in a file called something like
`middle_char_spec.rb`. The `_spec` on the end of the filename tells Rspec to
look inside it for tests.

I'll use the example from the previous post - writing a method which takes a
string and returns the middle character if there is one, or else the middle two
characters.  Here's what some tests in `middle_char_spec.rb` might look like:

```ruby
require 'middle'

describe 'middle_char method' do
  it 'returns "b" when given "abc"' do
    expect(middle_char("abc")).to eq "b"
  end
  it 'return "C" when given "ABCDE"' do
    expect(middle_char("ABCDE")).to eq "C"
  end
end
```

The first line uses ruby's `require` command to import the file we want to test,
in this case `middle.rb`. Note that `require` does not need the file extension
or the path. Rspec loads the `lib/` folder into Ruby's `$LOAD_PATH` global
variable, an array of absolute paths where ruby looks for files referenced by
`require`. You can also specify files to include using this syntax:

```ruby
require './lib/middle'
require_relative '../lib/middle' # relative to the current file
```

From rspec-core docs:
> The `describe` method creates an example group. Within the block passed to
> `describe` you can declare nested groups using the `describe` or `context` methods,
> or you can declare examples using the `it` or `specify` methods.

From rspec-expectations docs:
> The basic structure of an rspec expectation is:
> ```ruby
> expect(actual).to matcher(expected)
> expect(actual).not_to matcher(expected)
> ```
> Note: You can also use `expect(..).to_not` instead of `expect(..).not_to`.
> One is an alias to the other, so you can use whichever reads better to you.

The text you add to the `describe` and `it` methods is used to give feedback
when you run the tests, so make sure you use something helpful.

Let's try putting this code in `lib/middle.rb`:

```ruby
def middle_char(string)
  'b'
end
```

And then run rspec in the root folder of our project. The output is:

```bash
➜ rspec
.F

Failures:

  1) middle_char method returns "C" when given "ABCDE"
     Failure/Error: expect(middle_char("ABCDE")).to eq "C"

       expected: "C"
            got: "b"

       (compared using ==)
     # ./spec/mid_char_spec.rb:8:in `block (2 levels) in <top (required)>'

Finished in 0.01165 seconds (files took 0.08722 seconds to load)
2 examples, 1 failure

Failed examples:

rspec ./spec/mid_char_spec.rb:7 # middle_char method returns "C" when given "ABCDE"
```

One test passes, the other fails. The output gives a lot of useful detail. We
can also see the value of giving our tests clear descriptions, as they are used
in RSpec's output to identify the failing tests.

We have more options than just testing for equality, e.g:

```ruby
# Equality
expect(actual).to eq(expected) # passes if actual == expected

# Comparisons
expect(actual).to be >  expected
expect(actual).to be >= expected
expect(actual).to be <= expected
expect(actual).to be <  expected
expect(actual).to be_between(minimum, maximum).inclusive
expect(actual).to be_between(minimum, maximum).exclusive
expect(actual).to match(/expression/)
expect(actual).to be_within(delta).of(expected)
expect(actual).to start_with expected
expect(actual).to end_with expected

# Types/classes/responses
expect(actual).to be_instance_of(expected)
expect(actual).to be_kind_of(expected)
expect(actual).to respond_to(expected)

# Truthiness and existentialism
expect(actual).to be_truthy    # passes if actual is truthy (not nil or false)
expect(actual).to be true      # passes if actual == true
expect(actual).to be_falsey    # passes if actual is falsy (nil or false)
expect(actual).to be false     # passes if actual == false
expect(actual).to be_nil       # passes if actual is nil
expect(actual).to exist        # passes if actual.exist? and/or actual.exists? are truthy
expect(actual).to exist(*args) # passes if actual.exist?(*args) and/or actual.exists

# and loads more...
```

Check the rspec-expectations docs for more examples and info:
<https://relishapp.com/rspec/rspec-expectations/v/3-8/docs/built-in-matchers>

[lucas-github]:https://github.com/punchcafe
[cosmins-github]:https://github.com/micosmin
