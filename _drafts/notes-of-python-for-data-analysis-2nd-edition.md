---
layout: post
title: "Notes of Python for Data Analysis, 2nd Edition"
categories: Programming
tags: python data-analysis
---

[*Python for Data Analysis*, 2nd Edition](https://www.amazon.com/Python-Data-Analysis-Wrangling-IPython/dp/1491957662) (2017) by Wes McKinney.

{% include toc.html %}

## NumPy

[`numpy.ndarray`](https://docs.scipy.org/doc/numpy/reference/arrays.ndarray.html) is a class to represent multidimensional array. It is faster than the Python builtin [`list`](https://docs.python.org/3.4/library/stdtypes.html#list).

```python
In [1]: import numpy as np
In [2]: my_arr = np.arange(1000000)
In [3]: my_list = list(range(1000000))
In [4]: %time for _ in range(10): my_arr2 = my_arr * 2
Wall time: 21 ms
In [5]: %time for _ in range(10): my_list2 = [x * 2 for x in my_list]
Wall time: 1.09 s
```

### Multidimensional Arrays

#### Creating


