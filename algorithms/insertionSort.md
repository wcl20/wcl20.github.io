---
layout: post
title: Insertion Sort
---

## Problem
Insertion sort is a simple sorting algorithm that sees the array as sorted and unsorted sequences. At each iteration, it picks a number from the unsorted sequence and insert it to the sorted sequence.

Given an array of size $n$, sort the array using Insertion Sort.

## Solution

```python
def insertionSort(array: List[int]):
    # At the beginning, only the first element is sorted
    for i in range(1, len(array)):
        # new value
        value = array[i]
        # Points to the last element in sorted sequence
        j = i - 1
        # While current value is larger than new value ...
        while j >= 0 and array[j] > value:
            # ... move current value one step to the right
            array[j + 1] = array[j]
            j -= 1
        # Insert new value into correct position
        array[j + 1] = value       
```
