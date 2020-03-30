---
layout: post
title: The Maximum Subarray
subtitle: Hackerrank
---

## Problem
We define subsequence as any subset of an array. We define a subarray as a contiguous subsequence in an array. Given an array, find the maximum subarray sum.



## Solution

Kadane's Algorithm is used for finding the maximum subarray sum.

1. Store maximum subarray sum ending at index $i$. The maximum subarray sum at index $i$ is either the current value, or the sum of current value and the accumulated sum.


$$
dp[i] = max(dp[i-1] + arr[i], arr[i])
$$

Method 1: Use table to store subproblems
```python
def maximumSubarray(array: List[int]) -> int:
    # Create array to store subproblems (Dynamic Programming)
    dp = [0 for _ in range(len(array))]
    # Start with dp[0] as first element in array
    dp[0] = array[0]
    # Kadane's Algorithm
    for i in range(1, len(dp)):
        # Maximum subarray sum at index $i$ is either:
        #   1. Current value + accumulated sum
        #   2. Current value
        dp[i] = max(dp[i-1] + array[i], array[i])
    # Return maximum of all maximum subarray ending at different index
    return max(dp)
```

Method 2: Store current max and global max
```python
def maximumSubarray(array: List[int]) -> int:
    # Store current maximum
    currentMax = array[0]
    # Store global maximum
    globalMax = array[0]
    # Kadane's Algorithm
    for i in range(1, len(array)):
        # Current max is either:
        #   1. Current value + accumulated sum
        #   2. Current value
        currentMax = max(currentMax + array[i], array[i])
        # Update global max
        globalMax = max(globalMax, currentMax)
    return globalMax
```

## Variations

Variation 1: Return the indices of maximum subarray
```python
def maximumSubarray(array: List[int]) -> int:
    # Store current maximum
    currentMax = array[0]
    # Store global maximum
    globalMax = array[0]
    # Store start and end index
    start, end, currentStart = 0, 0, 0
    # Kadane's Algorithm
    for i in range(1, len(array)):
        # If current value is larger without accumulated sum ...
        if array[i] > currentMax + array[i]:
            # Update current max to current value
            currentMax = array[i]
            # Update start index to current value
            currentStart = i
        else:
            # Otherwise, current max is current value + accumulated sum
            currentMax += array[i]
        # If current max is larger than global max ...
        if currentMax > globalMax:
            # Update global max
            globalMax = currentMax
            # Update start and end index
            start, end = currentStart, i
    return start, end
```
