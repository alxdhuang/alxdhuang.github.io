---
layout: post
title: "Notes of SICP, 2nd Edition"
categories: Programming
tags: sicp lisp scheme programming computer-science
---

Notes of [*Structure and Interpretation of Computer Programs*, 2nd Edition](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html) by Harold Abelson and Gerald Jay Sussman with Julie Sussman.

{% include toc.html %}

## Quotes, Summary, and Comment

### Preface to the First Edition

> Our design of this introductory computer-science subject reflects two major concerns. First, we want to establish the idea that a computer language is not just a way of getting a computer to perform operations but rather that it is **a novel formal medium for expressing ideas about methodology**. Thus, programs must be written for people to read, and only incidentally for machines to execute. Second, we believe that the essential material to be addressed by a subject at this level is not the syntax of particular programming-language constructs, nor clever algorithms for computing particular functions efficiently, nor even the mathematical analysis of algorithms and the foundations of computing, but rather the techniques used to **control the intellectual complexity of large software systems**.

### Chapter 1. Building Abstractions with Procedures

Why Lisp?

> Lisp's flexibility in **handling procedures as data** makes it one of the most convenient languages in existence for exploring these techniques. The ability to represent procedures as data also makes Lisp an excellent language for writing programs that must manipulate other programs as data, such as the interpreters and compilers that support computer languages.

#### 1.1 The Elements of Programming

> Every powerful language has three mechanisms for accomplishing this:
>
> - **primitive expressions**, which represent the simplest entities the language is concerned with,
> - **means of combination**, by which compound elements are built from simpler ones, and
> - **means of abstraction**, by which compound elements can be named and manipulated as units.

##### 1.1.1 Expressions

One of the examples of primitive expression is the number. Numbers can be combined by a *primitive procedure* (such as `+` or `*`) to form a compound expression; that's the means of combination.

```scheme
(+ 137 349)
;Value: 486
```

##### 1.1.2 Naming and the Environment

The simplest means of abstraction is giving a name to a combination.

```scheme
(define <name> <body>)
```

Defining names is a way to *reduce the complexity of a program* because a very complex combination can be understood, remembered and reused.

##### 1.1.4 Compound Procedures

Another means of abstraction is defining compound procedures. The general form is

```scheme
(define (<name> <formal parameters>) <body>)
```

##### 1.1.5 The Substitution Model for Procedure Application

> To apply a compound procedure to arguments, evaluate the body of the procedure with each formal parameter replaced by the corresponding argument.

The application of a compound procedure has two evaluation orders:

- *normal-order evaluation*. Fully expand and then reduce.
- *applicative-order evaluation*. Evaluate the arguments and then apply.

Applicative-order evaluation is more effective.

##### 1.1.7 Example: Square Roots by Newton's Method

```scheme
(define (sqrt-iter guess x)
  (if (good-enough? guess x)
      guess
      (sqrt-iter (improve guess x) x)))
(define (improve guess x)
  (average guess (/ x guess)))
(define (average x y)
  (/ (+ x y) 2))
(define (good-enough? guess x)
  (< (abs (- (square guess) x)) 0.001))
(define (sqrt x)
  (sqrt-iter 1.0 x))
```

##### 1.1.8 Procedures as Black-Box Abstractions

We can use the *block structure* to rewrite the `sqrt` procedure, i.e. put all the definitions of auxiliary procedures into the definition of `sqrt`. Then we have finished the encapsulation.

```scheme
(define (sqrt x)
  (define (good-enough? guess x)
    (< (abs (- (square guess) x)) 0.001))
  (define (improve guess x)
    (average guess (/ x guess)))
  (define (sqrt-iter guess x)
    (if (good-enough? guess x)
        guess
        (sqrt-iter (improve guess x) x)))
  (sqrt-iter 1.0 x))
```

Another benefit is we do not have to pass `x` explicitly into the internal procedures. We allow `x` to be a free variable in the internal definitions. This discipline is called *lexical scoping*.

```scheme
(define (sqrt x)
  (define (good-enough? guess)
    (< (abs (- (square guess) x)) 0.001))
  (define (improve guess)
    (average guess (/ x guess)))
  (define (sqrt-iter guess)
    (if (good-enough? guess)
        guess
        (sqrt-iter (improve guess))))
  (sqrt-iter 1.0))
```
