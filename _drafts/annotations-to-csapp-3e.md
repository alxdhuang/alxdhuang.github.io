---
layout: post
title: "Annotations to CSAPP 3e"
categories: Annotations Programming
tags: computer-systems
---

[*Computer Systems: A Programmer's Perspective*, 3rd Edition](http://csapp.cs.cmu.edu/) (2015) by Randal E. Bryant and David R. O'Hallaron.

{% include toc.html %}

## Chapter 1. A Tour of Computer Systems

### 1.1 Information Is Bits + Context

The context means the algorithm of how we interpret bits.

### 1.2 Programs Are Translated by Other Programs into Different Forms

- Preprocessing phase
- Compilation phase
- Assembly phase
- Linking phase

### 1.3 It Pays to Understand How Compilation Systems Work

- *Optimizing program performance.*
    - Is a `switch` statement always more efficient than a sequence of `if-self` statements?
    - How much overhead is incurred by a function call?
    - Is a `while` loop more efficient than a `for` loop?
    - Are pointer references more efficient than array indexes?
    - Why does our loop run so much faster if we sum into a local variable instead of an argument that is passed by reference?
    - How can a function run faster when we simply rearrange the parentheses in an arithmetic expression?

    Later, I will answer these questions.

- *Understartding link-time errors.*
- *Avoiding security holes.*