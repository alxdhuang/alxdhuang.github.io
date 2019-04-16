---
layout: post
title: "Annotations to The Official Python Tutorial"
categories: Annotations Programming
tags: python
---

[The Official Python Tutorial](https://docs.python.org/3/tutorial/index.html).

{% include toc.html %}

## 2. Using the Python Interpreter

### 2.1. Invoking the Interpreter

How to exit the interpreter? `quit()` or `exit()`?

### 2.2. The Interpreter and Its Environment

#### 2.2.1. Source Code Encoding

> To declare an encoding other than the default one, a special comment line should be added as the first line of the file. The syntax is as follows:
> 
> ```python
> # -*- coding: encoding -*-
> ```

All `codecs` are listed in [here](https://docs.python.org/3/library/codecs.html#standard-encodings).

> One exception to the first line rule is when the source code starts with a UNIX “shebang” line. In this case, the encoding declaration should be added as the second line of the file. For example:
>
> ```python
> #!/usr/bin/env python3
> # -*- coding: cp1252 -*-
> ```

## 3. An Informal Introduction to Python

### 3.1. Using Python as a Calculator

#### 3.1.1. Numbers

Python has a builtin floor division `//`.

```python
>>> 17 // 3
5
```

What about ceil division? Python hasn't a builtin operator to do that. You have to import the `math` library.

```python
>>> import math
>>> math.ceil(17 / 3)
6
```

> In interactive mode, the last printed expression is assigned to the variable `_`. This means that when you are using Python as a desk calculator, it is somewhat easier to continue calculations, ...

Cool!
