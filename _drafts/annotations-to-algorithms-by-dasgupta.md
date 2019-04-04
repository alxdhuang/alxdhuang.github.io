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

No need exact and rigorous calculation, we could see that $2^{0.5n} \leq F_n < 2^{n}$ for $n \geq 6$.

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

(**Be careful!** When $n=6$, the equality holds.)

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

> 0.3. The Fibonacci numbers $F_0,F_1,F_2,\cdots$ are defined by the rule
>
> $$
> F_0=0,F_1=1,F_n = F_{n-1} + F_{n-2}
> $$
> 
> In this problem we will confirm that this sequence grows exponentially fast and obtain some bounds on its growth.
> 
> (a) Use induction to prove that $F_n \geq 2^{0.5n}$ for $n\geq 6$.  
> (b) Find a constant $c < 1$ such that $F_n \leq 2^{cn}$ for all $n \geq 0$. Show that your answer is correct.  
> (c) What is the largest $c$ you can find for which $F_n = \Omega(2^{cn})$?  

(a) See [0.2 Enter Fibonacci](#02-enter-fibonacci).

(b) Suppose $F_{n-1} \leq 2^{c(n-1)}$ and $F_{n-2} \leq 2^{c(n-2)}$, for that the mathematical induction works, it must obeys 

$$
2^{c(n-1)} + 2^{c(n-2)} \leq 2^{cn}
$$

i.e. 

$$
2^{2c} - 2^{c} - 1 \geq 0
$$

Let $x = 2^{c}$, then we have $x^2 - x - 1 \geq 0$. The solution is $x \geq \frac{1+\sqrt{5}}{2} \approx 1.618$, i.e. $c \geq \log_2 \frac{1+\sqrt{5}}{2} \approx 0.694$.

(c) According to (b), we know that the largest $c$ is $\log_2 \frac{1+\sqrt{5}}{2}$.

> 0.4. Is there a faster way to compute the `n`th Fibonacci number than by `fib2`(page 4)? One idea involves **matrices**.
>
> We start by writing the equations $F_1=F_1$ and $F_2=F_0+F_1$ in matrix notation:
>
> $$
> \begin{pmatrix}
> F_1 \\
> F_2 \\
> \end{pmatrix} = 
> \begin{pmatrix}
> 0 & 1 \\ 
> 1 & 1
> \end{pmatrix} \cdot
> \begin{pmatrix}
> F_0 \\
> F_1 \\
> \end{pmatrix}
> $$
>
> Similarly, 
>
> $$
> \begin{pmatrix}
> F_2 \\
> F_3 \\
> \end{pmatrix} =
> \begin{pmatrix}
> 0 & 1 \\ 
> 1 & 1
> \end{pmatrix} \cdot
> \begin{pmatrix}
> F_1 \\
> F_2 \\
> \end{pmatrix} =
> \begin{pmatrix}
> 0 & 1 \\ 
> 1 & 1
> \end{pmatrix}^2 \cdot
> \begin{pmatrix}
> F_0 \\
> F_1
> \end{pmatrix}
> $$
>
> and in general
> 
> $$
> \begin{pmatrix}
> F_n \\
> F_{n+1} \\
> \end{pmatrix} =
> \begin{pmatrix}
> 0 & 1 \\ 
> 1 & 1
> \end{pmatrix}^n \cdot
> \begin{pmatrix}
> F_0 \\
> F_1
> \end{pmatrix}
> $$
>
> So, in order to compute $F_n$, it suffices to raise this $2\times2$ matrix, call it $X$, to the `n`th power.
>
> (a) Show that two $2\times2$ matrices can be multiplied using 4 additions and 8 multiplications.
>
> But how many matrix multiplications does it take to compute $X^n$?
>
> (b) Show that $O(\log n)$ matrix multiplications suffice for computing $X^n$. (Hint: Think about computing $X^8$.)
>
> Thus the number of arithmetic operations needed by our matrix-based algorithm, call it `fib3`, is just $O(\log n)$, as compared to $O(n)$ for `fib2`. Have we broken another exponential barrier?
> 
> **The catch is that our new algorithm involves multiplication, not just addition; and multiplications of large numbers are slower than additions.** We have already seen that, when the complexity of arithmetic operations is taken into account, the running time of `fib2` becomes $O(n^2)$.
>
> (c) Show that all intermediate results of `fib3` are $O(n)$ bits long.

(a) This statement is easily proved by directly multiply the two matrices.

(b) Suppose $T(X^n)$ is the times of matrix multiplication of computing $X^n$, and let $n=2^m + i$. Because $X^{2^m} = X^{2^{m-1}} \cdot X^{2^{m-1}}$, we have

$$
T(X^{2^m}) = T(X^{2^{m-1}}) + 1 = \cdots = T(X^{2}) + m-1 = m
$$

So that 

$$
T(X^n) = T(X^{2^m}) + T(X^i) = m + T(X^i)
$$

Because $i < 2^m$, we have $T(X^i) < m$. So that $T(X^n) < 2m$. Finally

$$
T(X^n) = O(\log n)
$$

(c) Suppose 

$$
X^{n-1}=\begin{pmatrix} x_{11} & x_{12} \\ x_{21} & x_{22} \end{pmatrix}
$$

then 

$$
X^n = \begin{pmatrix} 0 & 1 \\ 1 & 1 \end{pmatrix} \cdot \begin{pmatrix} x_{11} & x_{12} \\ x_{21} & x_{22} \end{pmatrix} = \begin{pmatrix} x_{21} & x_{22} \\ x_{11} + x_{21} & x_{12} + x_{22} \end{pmatrix}
$$

Because that the bits long of the value of addition of two integers at most plus 1, we have $O(n)$.