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

### 1.4 Processors Read and Interpret Instructions Stored in Memory

#### 1.4.1 Hardware Organization of a System

{% include image.html name="hardware-organization.png" %}

##### Buses

> Buses are typically designed to transfer fixed-size chunks of bytes known as **words**.

Another definition of a word size is the size of the virtual memory address (pointer). What's the relationship between these two definitions?

##### I/O Devices

> Each I/O device is connected to the I/O bus by either a **controller** or an **adapter**. The distinction between the two is mainly one of packaging. Controllers are chip sets in the device itself or on the system's main printed circuit board (often called the **motherboard**). An adapter is a card that plugs into a slot on the motherboard.