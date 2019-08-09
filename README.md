# Block Parameters

## Learning Goals

- Define a code block
- Recognize block parameters
- Utilize block parameters with `do...end`
- Incorporate block parameters into loops for `Array`s

## Introduction

We have seen a few examples of loops so far, one example being `times`:

```ruby
number = 5

number.times do
  puts "I print out #{number} times"
end
```

In another example, we saw how we can use a `while` loop to access
each element in an `Array`:

```ruby
counter = 0
array = [1,2,3,4,5]

while array[counter] do
  puts array[counter]
  counter += 1
end
```

Repetition is so common that Ruby provides a variety of loops as well as
multiple ways to use those loops. In this lesson, we're going to explore an
additional component of loops that we can use to simplify the `while` example:
block parameters.

First though, we need to understand what _code blocks_ are.

## Ruby Code Blocks

A code block is a way of grouping statements together. We've actually already
used them quite a few times! They are most often seen in the form of `do...end`,
as with a `while` loop:

```ruby
while true do
  puts 'hello'
end
```

The code block here defines what will happen during a single iteration of our
`while` loop. Code blocks can also be written with curly braces (`{}`):

```ruby
while true {
  puts 'hello'
}
```

We're effectively saying to Ruby, "while this condition is true, do
**_this_**." Code blocks are written immediately after a method.  We will most
often see them used in loops and, in the near future, [enumerables][].
Eventually, you will write methods that take _code blocks_. It'll be great!

Ruby has two ways of defining blocks. For "short blocks" Rubyists prefer `{}`,
for blocks with multiple lines of code, they prefer `do...end`.

## Block Parameters

So, it turns out, we've been using code blocks already. However, there is one
piece we haven't discussed: depending on the method, **blocks can receive
parameters that are accessible from within the block**.

When using a `times` loop, for instance, we have access to a block parameter
that is equal to an `Integer` with the particular "loop number" we're in. In
the example below, we've named the parameter `index`:

```ruby
5.times do |index|
  puts index
end
```

The above loop outputs:

```text
0
1
2
3
4
```

As we just said, since it's just one line of code, most Rubyists would write
the loop using the `{}` block format as:

```ruby
5.times { |index| puts index }
```

Block parameters are surrounded by `|` symbols, usually referred to as 'pipes.'

Block parameters are similar to the parameters for an method in that _we_
provide the name. If instead of `index`, we wanted to name it `hot_dog` (a bad
idea), the results would be the same

```ruby
5.times do |hot_dog|
  puts hot_dog
end
```

```text
0
1
2
3
4
```

While we can name the parameter whatever we like, the value sent to it will
usually be obviously related to the method that's being run.  With `times`, the
value of the parameter is the `Integer` of the loop count. This integer will
change every time the block is called (that is, every iteration of the loop),
starting at zero and incrementing by one each time.

> **APPLY KNOWLEDGE**: You might be seeing how we could use `.times` to shorten
> up our `while` loops. If you want to test your cleverness, try it out in IRB!

To reiterate, the values block parameters represent are determined by what that
code block is related to. The `while` loop, for instance, **doesn't have a
block parameter**, even though it has a code block. Other methods we'll see later
have two or even three parameters.

## Combining Arrays, Loops and Block Parameters

Let's tighten up our looping code.

```ruby
counter = 0
array = [1,2,3,4,5]

while array[counter] do
  puts array[counter]
  counter += 1
end
```

Can become...

```ruby
array = [1,2,3,4,5]
length = array.length

length.times do |index|
  puts array[index]
end
```

```text
1
2
3
4
5
```

Or, simplifying further (written here with the optional curly brace syntax):

```ruby
array = [1,2,3,4,5]

array.length.times { |index|
  puts array[index]
}
```

Or, to tighten it up even further:

```ruby
array = [1,2,3,4,5]
array.length.times { |index| puts array[index] }
```

We've eliminated the need for `counter` by using a block parameter!

> **DEEP THINKING**: You might realize that what's effectively happening here
> is "for each member of the `Array`, do something in a block to that member."
> Ruby has a built-in that matches this case that we'll learn later on!

## Conclusion

As you progress, block parameters will become as normal as writing a `puts`
statement. How block parameters are used depends on what method the code block
is being used with. Some built in Ruby methods, like `while`, use a code block,
but do not have a parameter.

## Resources

- [`while` loops][while]
- [`times` loops][times]

[times]: https://ruby-doc.org/core-2.5.0/Integer.html#method-i-times
[while]: https://ruby-doc.org/core-2.5.0/doc/syntax/control_expressions_rdoc.html#label-while+Loop
[enumerables]: https://ruby-doc.org/core-2.6.2/Enumerable.html
