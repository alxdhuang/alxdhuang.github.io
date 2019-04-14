---
layout: post
title: "Notes of The Elements of Computing Systems"
categories: Programming
tags: computer-science computer-systems
math: true
---

Notes of [*The Elements of Computing Systems*](https://www.nand2tetris.org/) by Noam Nisan and Shimon Schocken.

{% include toc.html %}

## Quotes, Summary, and Comment

### Chapter 1. Boolean Logic

#### 1.1 Background

##### 1.1.1 Boolean Algebra

A truth table of a boolean function $f(x,y,z)$:

| $x$ $y$ $z$ | $f(x,y,z)$ |
| $0$ $0$ $0$ | $0$        |
| $0$ $0$ $1$ | $0$        |
| $0$ $1$ $0$ | $1$        |
| $0$ $1$ $1$ | $0$        |
| $1$ $0$ $0$ | $1$        |
| $1$ $0$ $1$ | $0$        |
| $1$ $1$ $0$ | $1$        |
| $1$ $1$ $1$ | $0$        |

The *canonical representation* of the boolean function $f(x,y,z)$ can be constructed by these steps: Choose all rows in which the function has value 1. For each such row, we construct a term created by And-ing together literals that fix the values of all the row’s inputs. Finally, we Or-together all these terms. 

For example, for the third row, we construct $\bar{x}y\bar{z}$; for the fifth row, we construct $x\bar{y}\bar{z}$; for the seventh row, we construct $xy\bar{z}$. Now we Or-together them,

$$
f(x,y,z)=\bar{x}y\bar{z} + x\bar{y}\bar{z} + xy\bar{z}
$$

This construction leads to an important conclusion: *Every Boolean function, no matter how complex, can be expressed using three Boolean operators only: And, Or, and Not*.

The number of Boolean functions that can be defined over n binary variables is $2^{2^n}$. Here are all the Boolean functions of two variables:

{% include image.html name="two-input-boolean-functions.png" width="61.8%" %}

The Nand function (as well as the Nor function) has an interesting theoretical property: Each one of the operations And, Or, and Not can be constructed from it, and it alone. And since every Boolean function can be constructed from And, Or, and Not operations using the canonical representation method, it follows that every Boolean function can be constructed from Nand operations alone.

Suppose $\oplus$ represents Nand,

$$
\begin{align}
x + y &= (x \oplus x) \oplus (y \oplus y) \\

\bar{x} &= x \oplus x \\

x \cdot y &= \overline{\bar{x} + \bar{y}} \\
          &= \overline{(\bar{x} \oplus \bar{x}) \oplus (\bar{y} \oplus \bar{y})} \\
          &= ((\bar{x} \oplus \bar{x}) \oplus (\bar{y} \oplus \bar{y})) \oplus ((\bar{x} \oplus \bar{x}) \oplus (\bar{y} \oplus \bar{y}))
\end{align}
$$