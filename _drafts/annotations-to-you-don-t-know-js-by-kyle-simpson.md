---
layout: post
title: "Annotations to You Don't Know JS by Kyle Simpson"
categories: Annotations
tags: javascript
---

Annotations to [*You Don't Know JS (book series)*](https://github.com/getify/You-Dont-Know-JS) by Kyle Simpson.

{% include toc.html %}

## Up & Going

### Chapter 1: Into Programming
### Chapter 2: Into JavaScript
### Chapter 3: Into YDKJS
### Appendix A: Thank You's!

## Scope & Closures

### Chapter 1: What is Scope?

> Where do those variables **live**?

### Chapter 2: Lexical Scope

Lexical scopes are created at the lexing time. When you create a block, you introduce a scope. Lexical scopes form a list of scope-*chains* or scope-*stacks*.

```
+---------+   +---------+   +---------+
| scope 1 |-->| scope 2 |-->| scope 3 |
+---------+   +---------+   +---------+
+---------+   +---------+ 
| scope 4 |-->| scope 5 |
+---------+   +---------+ 
+---------+   +---------+   +---------+   +---------+
| scope 6 |-->| scope 7 |-->| scope 8 |-->| scope 9 |
+---------+   +---------+   +---------+   +---------+
+----------+
| scope 10 |
+----------+
...
```

When the engine looks up an identifier, it will at first find in the current scope, if it doesn't find out, it will look up in the outer scope, and so on, finally reach to the global scope.

### Chapter 3: Function vs. Block Scope
### Chapter 4: Hoisting
### Chapter 5: Scope Closures
### Appendix A: Dynamic Scope
### Appendix B: Polyfilling Block Scope
### Appendix C: Lexical-this
### Appendix D: Thank You's!

## `this` & Object Prototypes

### Chapter 1: this Or That?
### Chapter 2: this All Makes Sense Now!
### Chapter 3: Objects
### Chapter 4: Mixing (Up) "Class" Objects
### Chapter 5: Prototypes
### Chapter 6: Behavior Delegation
### Appendix A: ES6 class
### Appendix B: Thank You's!

## Types & Grammar

### Chapter 1: Types
### Chapter 2: Values
### Chapter 3: Natives
### Chapter 4: Coercion
### Chapter 5: Grammar
### Appendix A: Mixed Environment JavaScript
### Appendix B: Thank You's!

## Async & Performance

### Chapter 1: Asynchrony: Now & Later
### Chapter 2: Callbacks
### Chapter 3: Promises
### Chapter 4: Generators
### Chapter 5: Program Performance
### Chapter 6: Benchmarking & Tuning
### Appendix A: Library: asynquence
### Appendix B: Advanced Async Patterns
### Appendix C: Thank You's!

## ES6 & Beyond

### Chapter 1: ES? Now & Future
### Chapter 2: Syntax
### Chapter 3: Organization
### Chapter 4: Async Flow Control
### Chapter 5: Collections
### Chapter 6: API Additions
### Chapter 7: Meta Programming
### Chapter 8: Beyond ES6
### Appendix A: Thank You's!