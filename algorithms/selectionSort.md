---
layout: post
title: Selection Sort
---

## Problem
The selection sort algorithm sorts an array by repeatedly finding the minimum element from unsorted part and putting it at the beginning.

Given an array of size $n$, sort the array using Selection Sort.

## Solution

```python
def selectionSort(array: List[int]):
    # Iterate array $n$ times
    n = len(array)
    for i in range(n):
        # $i$ points to the last element in the sorted subarray
        # Find index of minimum element in remaining array
        minimum = i
        for j in range(i, n):
            # Update smallest number index
            if array[j] < array[minimum]:
                minimum = j
        # Put smallest element at the beginning
        array[i], array[minimum] = array[minimum], array[i]
```
