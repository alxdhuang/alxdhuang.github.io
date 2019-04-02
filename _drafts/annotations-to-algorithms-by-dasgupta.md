---
layout: post
title: "Annotations to Algorithms by Dasgupta"
categories: Annotations
tags: algorithms
math: true
---

Annotations to [*Algorithms*](https://www.amazon.com/dp/0073523402) by Sanjoy Dasgupta, Christos H. Papadimitriou and Umesh Vazirani (2006).

{% include toc.html %}

## Chapter 0. Prologue

### 0.1 Books and algorithms
### 0.2 Enter Fibonacci

| n     | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7  | ... |
| $F_n$ | 0 | 1 | 1 | 2 | 3 | 5 | 8 | 13 | ... |

The Fibonacci numbers grow *almost* as fast as the powers of 2: $F_n \approx 2^{0.694n}$.

No need exact and rigorous calculation, we could see that $2^{0.5n} < F_n < 2^{n}$ for $n \geq 6$.

Proof: for $n \geq 6$, we have $F_n > F_{n-1}$ and $F_n = F_{n-1} + F_{n-2}$, then

$$
F_n < 2F_{n-1} < 2^{2}F_{n-2} < 2^{3}F_{n-3} < \cdots < 2^{n-6}F_{6} = 2^{n-3} < 2^n
$$

$$
F_n > 2F_{n-2} > 2^{2}F_{n-4} > 2^{3}F_{n-6} > \cdots
$$

If $n$ is even, 

$$
F_n > \cdots > 2^{0.5n-3}F_{6} = 2^{0.5n}
$$

If $n$ is odd,

$$
F_n > \cdots > 2^{0.5n-3.5}F_{7} = 2^{0.5n}\frac{13}{2^{3.5}} = 2^{0.5n}\frac{13}{11.3\cdots} > 2^{0.5n}
$$

### 0.3 Big-O notation

A concrete definition of Big-O:

> Let $f(n)$ and $g(n)$ be functions from positive integers to positive reals. We say $f=O(g)$ (which means that "f grows no faster than g") if there is a constant $c > 0$ such that $f(n) \leq c g(n)$.

More notations:

> $f=\Omega(g)$ means $g=O(f)$
> 
> $f=\Theta(g)$ means $f=O(g)$ and $f=\Omega(g)$

## Chapter 1. Algorithms with numbers

### 1.1 Basic arithmetic
### 1.2 Modular arithmetic
### 1.3 Primality testing
### 1.4 Cryptography
### 1.5 Universal hashing

## Randomized algorithms: a virtual chapter

## Chapter 2. Divide-and-conquer algorithms

### 2.1 Multiplication
### 2.2 Recurrence relations
### 2.3 Mergesort
### 2.4 Medians
### 2.5 Matrix multiplication
### 2.6 The fast Fourier transform

## Chapter 3. Decompositions of Graphs

### 3.1 Why graphs?
### 3.2 Depth-first search in undirected graphs
### 3.3 Depth-first search in directed graphs
### 3.4 Strongly connected components

## Chapter 4. Paths in graphs

### 4.1 Distances
### 4.2 Breadth-first search
### 4.3 Lengths on edges
### 4.4 Dijkstra's algorithm
### 4.5 Priority queue implementations
### 4.6 Shortest paths in the presence of negative edges
### 4.7 Shortest paths in dags

## Chapter 5. Greedy algorithms

### 5.1 Minimum spanning trees
### 5.2 Huffman encoding
### 5.3 Horn fomulas
### 5.4 Set cover

## Chapter 6. Dynamic programming

### 6.1 Shortest paths in dags, revisited
### 6.2 Longest increasing subsequences
### 6.3 Edit distance
### 6.4 Knapsack
### 6.5 Chain matrix multiplication
### 6.6 Shortest paths
### 6.7 Independent sets in trees

## Chapter 7. Linear programming and reductions

### 7.1 An introduction to linear programming
### 7.2 Flows in networks
### 7.3 Bipartite matching
### 7.4 Duality
### 7.5 Zero-sum games
### 7.6 The simplex algorithm
### 7.7 Postscript: circuit evaluation

## Chapter 8. NP-complete problems

### 8.1 Search problems
### 8.2 NP-complete problems
### 8.3 The reductions

## Chapter 9. Coping with NP-completeness

### 9.1 Intelligent exhaustive search
### 9.2 Approximation algorithms
### 9.3 Local search heuristics

## Chapter 10. Quantum algorithms

### 10.1 Qubits, superposition, and measurement
### 10.2 The plan
### 10.3 The quantum fourier transform
### 10.4 Periodicity
### 10.5 Quantum circuits
### 10.6 Factoring as periodicity
### 10.7 The quantum algorithm for factoring

## Exercises

> 0.2. Show that, if $c$ is a positive real number, then $g(n)=1+c+c^2+\cdots+c^n$ is:
>
> (a) $\Theta(1)$ if $c < 1$.  
> (b) $\Theta(n)$ if $c = 1$.  
> (c) $\Theta(c^n)$ if $c > 1$.
>
> The moral: in big-$\Theta$ terms, the sum of a geometric series is simply the first term if the series is strictly decreasing, the last term if the series is strictly increasing, or the number of terms if the series is unchanging.

If $c = 1$, $g(n)=n$. (b) is true. 

If $c < 1$, $g(n)=1 + c \frac{1-c^{n}}{1-c}$. Because $0 < c \frac{1-c^{n}}{1-c} < \frac{c}{1-c}$, we have $1 < g(n) < \frac{1}{1-c}$. (a) is true.

If $c > 1$, $g(n)=c^n + \frac{c^{n}-1}{c-1}$. Because $c^{n-1} < \frac{c^{n}-1}{c-1} < \frac{c^{n}}{c-1}$, we have $\frac{1+c}{c}c^n < g(n) < \frac{c}{c-1}c^n$. (c) is true.