---
layout: post
title: Max Array Sum
subtitle: Hackerrank
---

## Problem
Given an array of integers, find the subset of non-adjacent elements with the maximum sum. Calculate the sum of that subset.

## Solution

Method 1: Dynamic Programming

$$
maxSubsetSum(arr, i) =
\begin{cases}
arr[0],
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
i = 0\\
max(arr[0], arr[1]),
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
i = 1\\
max
\begin{cases}
maxSubsetSum(arr, i - 2) + arr[i]\\
maxSubsetSum(arr, i - 1)\\
arr[i]
\end{cases}
\;\text{Otherwise}
\end{cases}
$$
```python
def maxSubsetSum(array: List[int]):
    # Get length of array
    n = len(array)
    # Create array to store subproblems (Dynamic Programming)
    dp = [0] * n
    # Iterate each number in array
    for i, num in enumerate(array):
        # Case i = 0
        if i == 0:
            dp[i] = array[0]
        # Case i = 1
        elif i == 1:
            dp[i] = max(array[0], array[1])
        else:
            # Include current number in subset
            include = dp[i - 2] + num
            # exclude current number from subset
            exclude = dp[i - 1]
            # Select max of three options
            dp[i] = max(include, exclude, num)
    return dp[-1]
```

Method 2: Dynamic Programming without Extra Space 

In each iteration, keep track of the maximum excluding current element and the maximum including this element.
```python
def maxSubsetSum(array: List[int]):
    # Stores maximum of including current element
    include = array[0]
    # Stores maximum of excluding current element
    exclude = 0
    # Iterate each number in array
    for num in array[1:]:
        # Update include and exclude
        include, exclude = exclude + num, max(exclude, include)
    return max(include, exclude)
```
