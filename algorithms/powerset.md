---
layout: post
title: Subsets
subtitle: LeetCode
---

## Problem
Given a set of distinct integers, $nums$, return all possible subsets (the power set).

## Solution

Method 1: Recursive Implementation

Iterate every number in $num$. For each number recursively find powerset once with the number included and once with the number excluded.
```python
def subsets(nums: List[int]) -> List[List[int]]:
    # List to store all subsets
    subsets = []
    # Recursive function starting from first element
    subsetsHelper(subsets, nums, [], 0)
    return subsets

def subsetsHelper(subsets: List[List[int]], nums: List[int], subset: List[int], index: int):
    # Base case: Reached end of list
    if index == len(nums):
        # Add subset to list of subsets
        subsets.append(subset)
        return
    # For each number, we have two options:
        # 1. Exclude number from subset
        # 2. Include number in subset
    # Exclude number, move to next index
    subsetsHelper(subsets, nums, subset.copy(), index + 1)
    # Include number and move to next index
    subset.append(nums[index])
    subsetsHelper(subsets, nums, subset.copy(), index + 1)
```

Method 2: Recursive Implementation

Iterate each number of $nums$. In each iteration, find all powerset with this number included in the subset. The second iteration will find all subsets without the first element, third iteration will find all subsets without first and second element and so on.
```python
def subsets(nums: List[int]) -> List[List[int]]:
    # List to store all subsets
    subsets = []
    # Recursive function starting from first element
    subsetsHelper(subsets, nums, [], 0)
    return subsets

def subsetsHelper(subsets: List[List[int]], nums: List[int], subset: List[int], index: int):
    # Add subset to list of subsets
    subsets.append(subset.copy())
    # For each number from index to end
    for i in range(index, len(nums)):
        # Include number in subset
        subset.append(nums[i])
        # Find powerset of remaining array
        subsetsHelper(subsets, nums, subset, i + 1)
        # Remove number from subset
        subset.pop()
```

Method 3: Using Bit Manipulation

An array with $n$ elements will have $2^n$ subsets. Iterate 0 to $2^n$ and find its binary representation (length $n$). '0' means excluding the element, '1' means including the element.

```python
def subsets(nums: List[int]) -> List[List[int]]:
    # List to store all subsets
    subsets = []
    # Iterate from 0 to $2^n$
    for i in range(2 ** len(nums)):
        # Create subset
        subset = []
        # Loop through binary representation of $i$
        for j in range(len(nums)):
            # Get bit at $j$ position
            bit = i & (1 << j)
            # At element if bit is 1
            if bit:
                subset.append(nums[j])
        # Add subset to list of subsets
        subsets.append(subset)
    return subsets
```
