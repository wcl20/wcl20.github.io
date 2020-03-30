---
layout: post
title: Fibonacci Numbers
subtitle: Hackerrank
---

## Problem
The Fibonacci sequence begins with $fibonacci(0) = 0$  and $fibonacci(1) = 1$ as its first and second terms. After these first two elements, each subsequent element is equal to the sum of the previous two elements.

Programmatically:

$$
\begin{align*}
&fibonacci(0) = 0\\
&fibonacci(1) = 1\\
&fibonacci(n) = fibonacci(n-1) + fibonacci(n-2)
\end{align*}
$$

Given $n$, return the $n^{th}$ number in the sequence.

## Solution
```python
def fibonacci(n: int) -> int:
    if n < 2:
        return n
    # Store only previous two numbers
    a, b = 0, 1
    # Iterate 2 to n ...
    for _ in range(2, n + 1):
        # ... calculate next number in the sequence
        a, b = b, a + b
    return b
```
