---
layout: post
title: Monotonic Array
subtitle: LeetCode
---

## Problem
An array is monotonic if it is either monotone increasing or monotone decreasing.

An array $A$ is monotone increasing if for all $i \leq j, A[i] \leq A[j]$.  An array $A$ is monotone decreasing if for all $i \geq j, A[i] \geq A[j]$.

Return true if and only if the given array $A$ is monotonic.

## Solution

```python
def isMonotonic(array: List[int]):
    increasing = True 
    decreasing = True
    for i in range(1, len(array)):
        # Check array is monotonic increasing
        if array[i] < array[i - 1]:
            increasing = False
        # Check array is monotonic decreasing
        if array[i] > array[i - 1]:
            decreasing = False
    # Return true is monotonic increasing or decreasing
    return increasing or decreasing
```
