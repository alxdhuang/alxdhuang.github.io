---
layout: post
title: "Notes of The Ruby Programming Language by David Flanagan and Yukihiro Matsumoto"
categories: Notes
tags: ruby
---

Here are notes of [*The Ruby Programming Language*](http://shop.oreilly.com/product/9780596516178.do) written by David Flanagan and Yukihiro Matsumoto.

{% include toc.html %}

## Chapter 1. Introduction

> Ruby is a dynamic programming language with a **complex** but **expressive** grammar and a core class library with a rich and powerful API. Ruby draws inspiration from Lisp, Smalltalk, and Perl, but uses a grammar that is easy for C and Java<sup>TM</sup> programmers to learn. Ruby is a pure object-oriented language, but it is also suitable for procedural and functional programming styles. It includes powerful metaprogramming capabilities and can be used to create domain-specific languages or DSLs.

### 1.1 A Tour of Ruby

Ruby is a *completely* object-oriented language. That means every value in Ruby is an object, i.e. it has methods. Parentheses in method invocations are commonly omitted, that make it more readable.

Some examples of *iterators*:

```ruby
3.times { print "Ruby! " }           # Prints "Ruby! Ruby! Ruby!"
1.upto(9) {|x| print x }             # Prints "123456789"

a = [1,2,3,4]                        # Start with an array
b = a.map {|x| x*x }                 # Square elements: b is [1,4,9,16]
c = a.select {|x| x % 2 == 0 }       # Select even elements: c is [2,4]
a.inject do |sum,x|                  # Compute the sum of the elements => 10
    sum + x
end
```

### 1.2 Try Ruby

