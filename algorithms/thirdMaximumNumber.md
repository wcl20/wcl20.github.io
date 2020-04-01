---
layout: post
title: Third Maximum Number
subtitle: LeetCode
---

## Problem
Given a non-empty array of integers, return the third maximum number in this array. If it does not exist, return the maximum number.

The function should return the third unique number.

Example 1:
Input: [2, 1, 1] should return 2 because there is no third maximum number.

Example 2:
Input: [3, 2, 2, 1] should return 1

## Solution

```python
def thirdMax(array: List[int]) -> int:
    # Keep track of first three largest numbers
    first = second = third = float("-inf")
    # Iterate each number in array
    for num in array:
        # If number is larger than largest
        if num > first:
            # Update first three numbers
            first, second, third = num, first, second
        # If number is larger than second largest
        if second < num < first:
            # Update second and third number
            second, third = num, second
        # If number is larger than third number
        if third < num < second:
            # Update third number
            third = num
    # If third largest does not exist
    if first == float("-inf") or second == float("-inf") or third == float("-inf"):
        # Return maximum
        return max(array)
    # Otherwise, return third largest
    return third  
```
