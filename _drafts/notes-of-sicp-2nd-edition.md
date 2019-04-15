---
layout: post
title: "Notes of SICP, 2nd Edition"
categories: Programming
tags: sicp lisp scheme programming computer-science
math: true
---

Notes of [*Structure and Interpretation of Computer Programs*, 2nd Edition](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html) by Harold Abelson and Gerald Jay Sussman with Julie Sussman.

{% include toc.html %}

## Quotes, Summaries, and Comments

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

#### 1.2 Procedures and the Processes They Generate

##### 1.2.1 Linear Recursion and Iteration

This section introduces two different ways to implement the factorial function $n!$.

- Linear recursive process: The process builds up a chain of *deferred operations*. The interpreter is responsible for keeping the state variables.

  ```scheme
  (define (factorial n)
    (if (= n 1)
        1
        (* n (factorial (- n 1)))))
  ```

  ```scheme
  (factorial 6)
  (* 6 (factorial 5))
  (* 6 (* 5 (factorial 4)))
  (* 6 (* 5 (* 4 (factorial 3))))
  (* 6 (* 5 (* 4 (* 3 (factorial 2)))))
  (* 6 (* 5 (* 4 (* 3 (* 2 (factorial 1))))))
  (* 6 (* 5 (* 4 (* 3 (* 2 1)))))
  (* 6 (* 5 (* 4 (* 3 2))))
  (* 6 (* 5 (* 4 6)))
  (* 6 (* 5 24))
  (* 6 120)
  720
  ```

- Linear iterative process: The process itself keeps the state variables.

  ```scheme
  (define (factorial n)
    (fact-iter 1 1 n))

  (define (fact-iter product counter max-count)
    (if (> counter max-count)
        product
        (fact-iter (* counter product)
                  (+ counter 1)
                  max-count)))
  ```

  ```scheme
  (factorial 6)
  (fact-iter 1 1 6)
  (fact-iter 1 2 6)
  (fact-iter 2 3 6)
  (fact-iter 6 4 6)
  (fact-iter 24 5 6)
  (fact-iter 120 6 6)
  (fact-iter 720 7 6)
  720
  ```

##### 1.2.2 Tree Recursion

## Solutions to Exercises

### Exercise 1.9

> Each of the following two procedures defines a method for adding two positive integers in terms of the procedures `inc`, which increments its argument by `1`, and `dec`, which decrements its argument by `1`.
>
> ```scheme
> (define (+ a b)
>   (if (= a 0)
>       b
>       (inc (+ (dec a) b))))
> 
> (define (+ a b)
>   (if (= a 0)
>       b
>       (+ (dec a) (inc b))))
> ```
> 
> Using the substitution model, illustrate the process generated by each procedure in evaluating `(+ 4 5)`. Are these processes iterative or recursive?

- recursive
  
  ```scheme
  (+ 4 5)
  (inc (+ 3 5))
  (inc (inc (+ 2 5)))
  (inc (inc (inc (+ 1 5))))
  (inc (inc (inc (inc (+ 0 5)))))
  (inc (inc (inc (inc 5))))
  (inc (inc (inc 6)))
  (inc (inc 7))
  (inc 8)
  9
  ```

### Exercise 1.10

> The following procedure computes a mathematical function called [Ackermann's function](https://en.wikipedia.org/wiki/Ackermann_function).
>
> ```scheme
> (define (A x y)
>   (cond ((= y 0) 0)
>         ((= x 0) (* 2 y))
>         ((= y 1) 2)
>         (else (A (- x 1)
>                  (A x (- y 1))))))
> ```
> 
> What are the values of the following expressions?
>
> ```scheme
> (A 1 10)
> (A 2 4)
> (A 3 3)
> ```
>
> Consider the following procedures, where `A` is the procedure defined above:
> 
> ```scheme
> (define (f n) (A 0 n))
> (define (g n) (A 1 n))
> (define (h n) (A 2 n))
> (define (k n) (* 5 n n))
> ```
>
> Give concise mathematical definitions for the functions computed by the procedures `f`, `g`, and `h` for positive integer values of `n`. For example, `(k n)` computes $5n^2$.

```scheme
(A 1 10)
(A 0 (A 1 9))
(A 0 (A 0 (A 1 8)))
(A 0 (A 0 (A 0 (A 1 7))))
(A 0 (A 0 (A 0 (A 0 (A 1 6)))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 1 5))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 4)))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 3))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 2)))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 1 1))))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 2)))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 4))))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 (A 0 8)))))))
(A 0 (A 0 (A 0 (A 0 (A 0 (A 0 16))))))
(A 0 (A 0 (A 0 (A 0 (A 0 32)))))
(A 0 (A 0 (A 0 (A 0 64))))
(A 0 (A 0 (A 0 128)))
(A 0 (A 0 256))
(A 0 512)
1024
```

`(A 1 n)` equals $2^n$.

```scheme
(A 2 4)
(A 1 (A 2 3))
(A 1 (A 1 (A 2 2)))
(A 1 (A 1 (A 1 (A 2 1))))
(A 1 (A 1 (A 1 2)))
(A 1 (A 1 4))
(A 1 16)
65536
```

`(A 2 n)` equals $\def\rddots#1{\cdot^{\cdot^{\cdot^{#1}}}} 2^{2^{\rddots2}}$, which has $n$ 2s.

```scheme
(A 3 3)
(A 2 (A 3 2))
(A 2 (A 2 (A 3 1)))
(A 2 (A 2 2))
(A 2 4)
65536
```

`(A 3 n)` equals `(A 2 (A 2 ... (A 2 2))) ... )`, which has `n` 2s.

Ackermann's function is one of the simplest and earliest-discovered examples of a total computable function that is not primitive recursive.

### Exercise 1.11

> A function $f$ is defined by the rule that $f(n) = n$ if $n<3$ and $f(n) = f(n - 1) + 2f(n - 2) + 3f(n - 3)$ if $n> 3$. Write a procedure that computes $f$ by means of a recursive process. Write a procedure that computes $f$ by means of an iterative process.

- Recursive

  ```scheme
  (define (f n) 
    (if (< n 3) 
        n
        (+ (f (- n 1)) 
            (* 2 (f (- n 2)))
            (* 3 (f (- n 3))))))
  ```

- Iterative

  ```scheme
  (define (f-iter sum1 sum2 sum3 counter max-count)
    (if (> counter max-count)
        sum3
        (f-iter sum2 
                sum3
                (+ sum3 (* 2 sum2) (* 3 sum1))
                (+ counter 1)
                max-count)))

  (define (f n)
      (if (< n 3)
          n
          (f-iter 0 1 2 3 n)))
  ```

### Exercise 1.12

> The following pattern of numbers is called Pascal's triangle.
> 
> {% include image.html name="pascal.png" %}
>
> The numbers at the edge of the triangle are all 1, and each number inside the triangle is the sum of the two numbers above it. Write a procedure that computes elements of Pascal's triangle by means of a recursive process.

```scheme
(define (pascal m n)
    (cond ((<= n 1) 1)
        ((>= n m) 1)
        (else (+ (pascal (- m 1) (- n 1))
                 (pascal (- m 1) n)))))
```