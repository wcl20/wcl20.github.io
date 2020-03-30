---
layout: post
title: Bubble Sort
---

## Problem
Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in wrong order.

Given an array of size $n$, sort the array using Bubble Sort.

## Solution

```python
def bubbleSort(array: List[int]):
    # Length of array
    n = len(array)
    # Repeat for $n - 1$ iterations ...
    for i in range(n - 1):
        # The last $i$ elements are already sorted
        for j in range(n - i - 1):
            # If adjacent elements are in wrong order ...
            if array[j] > array[j+1]:
                # ... Swap elements
                array[j], array[j+1] = array[j+1], array[j]
```
