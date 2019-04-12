---
layout: post
title: "Notes of Python for Data Analysis, 2nd Edition"
categories: Notes
tags: python data-analysis
---

This post is a set of notes of [*Python for Data Analysis*](http://wesmckinney.com/pages/book.html), 2nd Edition (2017) written by [Wes McKinney](http://wesmckinney.com/).

{% include toc.html %}

## What Is This Book About?

This book introduces manipulating, processing, cleaning, and crunching data in Python.

## NumPy Basics: Arrays and Vectorized Computation

[NumPy](http://www.numpy.org/) has fast vectorized array operations. We can compare, in [IPython](https://ipython.org/), the performance difference between a NumPy array and an equivalent Python list.

```python
In [1]: import numpy as np

In [2]: my_arr = np.arange(1000000)

In [3]: my_list = list(range(1000000))

In [4]: %time for _ in range(10): my_arr2 = my_arr * 2
Wall time: 21 ms

In [5]: %time for _ in range(10): my_list2 = [x * 2 for x in my_list]
Wall time: 1.1 s
```

[**Why are NumPy arrays so fast?**](https://stackoverflow.com/questions/8385602/why-are-numpy-arrays-so-fast)

### The NumPy `ndarray`