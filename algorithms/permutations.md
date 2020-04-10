---
layout: post
title: Permutations
subtitle: LeetCode
---

## Problem
Given a collection of distinct integers, return all possible permutations.

## Solution
The solution is to consider each element in the array, place it at the head of the list and permute the remaining array.

Method 1: Remove element and place in head
```python
def permute(array: List[int]) -> List[List[int]]:
    # Base Case: 0 or 1 element in array
    if len(array) < 2:
        # Only one possible permutation
        return [array]
    # Create list to store permutations
    permutations = []
    # Iterate each number in array
    for i, num in enumerate(array):
        # Get remaining list of elements removing $num$
        remaining = array[:i] + array[i + 1:]
        # Using $num$ as head and permute remaining list
        for permutation in permute(remaining):
            permutations.append([num] + permutation)
    return permutations
```

Method 2: Swap each element with head
```python
def permute(array: List[int]) -> List[List[int]]:
    # Create list to store permutations
    permutations = []
    permuteHelper(array, 0, permutations)
    return permutations

def permuteHelper(array: List[int], start: int, permutations: List[List[int]]):
    # Base case
    if start == len(array) - 1:
        # Add permutation to list of permutations
        permutations.append(array[:])
    else:
        # For each element in array
        for i in range(start, len(array)):
            # Swap with head of list
            array[i], array[start] = array[start], array[i]
            # Permute remaining list
            permuteHelper(array, start + 1, permutations)
            # Swap back element with head of list
            array[i], array[start] = array[start], array[i]
```
