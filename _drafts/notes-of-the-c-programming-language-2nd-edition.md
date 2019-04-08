---
layout: post
title: "Notes of The C Programming Language, 2nd Edition"
categories: Notes
tags: c
---

Here are some notes of [*The C Programming Language*, 2nd Edition](https://www.amazon.com/dp/0131103628) (K&R C) written by [Brian W. Kernighan](https://en.wikipedia.org/wiki/Brian_Kernighan) and [Dennis Ritchie](https://en.wikipedia.org/wiki/Dennis_Ritchie).

> C is not a big language, and it is not well served by a big book.

> C is not a "very high level" language, nor a "big" one, and is not specialized to any particular area of application.

> Most of the treatment is based on reading, writing and revising examples, rather than on mere statements of rules. For the most part, the  examples are complete, real programs, rather than isolated fragments.

| [Code](https://github.com/alxdhuang/knrc) |

{% include toc.html %}

## Introduction

> Many of the important ideas of C stem from the language [BCPL](https://en.wikipedia.org/wiki/BCPL), developed by [Martin Richards](https://en.wikipedia.org/wiki/Martin_Richards_(computer_scientist)). The influence of BCPL on C proceeded indirectly through the language B, which was written by [Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson) in 1970 for the first UNIX system on the DEC PDP-7.

> C is a relatively "low level" language.

What aspects reflect this?

- C deals with the same sort of objects that most computers do, namely *characters*, *numbers*, and *addresses*.
- C provides no operations to deal directly with *composite objects* such as *character strings*, *sets*, *lists*, or *arrays*.
- C provides no operations that manipulate an entire array or string, although structures may be copied as a unit.
- C does not define any storage allocation facility other than static definition and the stack discipline provided by the local variables of functions; there is no heap or garbage collection.
- C provides no input/output facilities; there are no READ or WRITE statements, and no built-in file access methods.
- C offers only straightforward, single-thread control flow: tests, loops, grouping, and subprograms, but not multiprogramming, parallel operations, synchronization, or coroutines.

Keeping C in a ralative small size makes it can be described in a small space, and learned quickly.

> C retains the basic **philosophy** that programmers know what they are doing; it only requires that they state their intentions explicitly.

## Chapter 1. A Tutorial Introduction

### 1.1 Getting Started

> The only way to learn a new programming language is by writing programs in it. 

In this section, the authors wrote down a "Hello World" program, which had become a famous tiny example of showing the basic features of a programming language.

Example: [`hello.c`](https://github.com/alxdhuang/knrc/blob/master/ch01/hello.c)

### 1.2 Variables and Arithmetic Expressions

Example: [`f2c.c`](https://github.com/alxdhuang/knrc/blob/master/ch01/f2c.c), a program that print a Fahrenheit-Celsius table.

### 1.3 The For Statement

Still writing a program to print a Fahrenheit-Celsius table, but instead of using `while`, using `for` makes the code more compact and elegant.

```c
int fahr;
for (fahr = 0; fahr <= 300; fahr = fahr + 20) 
    printf("%3.0f %6.1f\n", fahr, (5.0/9.0) * (fahr - 32.0));
```

### 1.4 Symbolic Constants

### 1.5 Character Input and Output

> The model of input and output supported by the standard library is very simple. Text input or output, regardless of where it originates or where it goes to, is dealt with as streams of characters. A **text stream** is a sequence of characters divided into lines; each line consists of zero or more characters followed by a newline character. 

#### 1.5.1 File Copying

Example: [`copy.c`](https://github.com/alxdhuang/knrc/blob/master/ch01/copy.c), a program that copies its input to its output one character at a time.