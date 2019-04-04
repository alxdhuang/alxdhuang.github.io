---
layout: post
title: "Read The Ruby Programming Language by David Flanagan and Yukihiro Matsumoto"
categories: Reading
tags: ruby
---

[*The Ruby Programming Language*](http://shop.oreilly.com/product/9780596516178.do) is a book written by [David Flanagan](https://twitter.com/__davidflanagan) and [Yukihiro Matsumoto](https://twitter.com/yukihiro_matz) in 2008, and it is an updated and expanded version of *Ruby in a Nutshell* by [Matz](https://twitter.com/yukihiro_matz). This book is loosely modeled after the classic [K&R C](https://en.wikipedia.org/wiki/The_C_Programming_Language).

My running Ruby version: 2.6.x.

{% include toc.html %}

## What is Ruby?

> Ruby is a dynamic programming language with a **complex** but **expressive** grammar and a core class library with a rich and powerful API. Ruby draws inspiration from Lisp, Smalltalk, and Perl, but uses a grammar that is easy for C and Java<sup>TM</sup> programmers to learn. Ruby is a **pure object-oriented** language, but it is also suitable for procedural and functional programming styles. It includes powerful **metaprogramming** capabilities and can be used to create domain-specific languages or DSLs.

## A Tour of Ruby

### Ruby Is Pure Object-Oriented

Ruby is pure object-oriented means that every value in Ruby is an object. An object has methods.

```ruby
1.class     # => Integer
1.0.class   # => Float
true.class  # => TrueClass
false.class # => FalseClass
nil.class   # => NilClass
```

> In Ruby, parentheses are usually optional and they are commonly omitted, especially when the method being invoked takes no arguments.

Omitted parentheses make the code more readable. Maybe.

### Blocks and Iterators

> The use of **iterators** and **blocks** is another notable feature of Ruby; although the language does support an ordinary `while` loop, it is more common to perform loops with constructs that are actually method calls.

```ruby
3.times { print "Ruby! " } # Ruby! Ruby! Ruby! 
1.upto(9) { |x| print x }  # 123456789
```

Comparing these code with the traditional `while` or `for` loops, it looks like more compact and directly. Because if you want to print a string three times, why do you have to create a variable and do the counting?

```c
for (int i = 0; i < 2; i++) printf("Ruby! ");
```