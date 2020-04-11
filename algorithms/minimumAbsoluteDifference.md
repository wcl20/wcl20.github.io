---
layout: post
title: Minimum Absolute Difference
subtitle: LeetCode
---

## Problem
Given an array of distinct integers, find all pairs of elements with the minimum absolute difference of any two elements.

Return a list of pairs in ascending order(with respect to pairs), each pair [a, b] follows:
* $a$, $b$ are from the Array
* $a < b$
* $abs(a-b)$ is the minimum absolute difference of any two elements in the array.

## Solution

To find the minimum difference between any two elements in the array:

1. Sort the array in ascending order.
2. Initialize minimum difference as infinite
3. Compare all adjacent pairs in the sorted array to keep track of minimum absolute difference.

```python
def minimumAbsoluteDifference(array: List[int]) -> List[List[int]]:
    # Sort the array
    array.sort()
    # Initialise minimum difference as infinite
    minimum = float("inf")
    # Keep track of pairs
    pairs = []
    # Iterate the sorted array
    for i in range(1, len(array)):
        # Compute difference of adjacent pairs
        difference = abs(array[i] - array[i - 1])
        # If difference is smaller than minimum
        if difference < minimum:
            # Update minimum
            minimum = difference
            # Clear all current stored pairs
            pairs.clear()
            # Append current pair
            pairs.append([array[i - 1], array[i]])
        # If difference equals minimum
        elif difference == minimum:
            # Append current pair
            pairs.append([array[i - 1], array[i]])
    return pairs
```

## Variations

Variation 1: Find minimum absolute difference
```python
def minimumAbsoluteDifference(array: List[int]) -> int:
    # Sort the array
    array.sort()
    # Initialise minimum difference as infinite
    minimum = float("inf")
    # Iterate the sorted array
    for i in range(1, len(array)):
        # Compute difference of adjacent pairs
        difference = abs(array[i] - arry[i - 1])
        # Update minimum difference
        minimum = min(minimum, difference)
    return minimum
```
