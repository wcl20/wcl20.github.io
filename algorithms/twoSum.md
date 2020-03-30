---
layout: post
title: Two Sum
subtitle: LeetCode
---

## Problem
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Solution
```python
def twoSum(nums: List[int], target: int) -> List[int]:
    # Create table to store (value, index)
    dict = {}
    # Iterate array ...
    for i, n in enumerate(nums):
        # ... If target - n is in hash ...
        if target - n in dict:
            # ... Return indices
            return [dict[target-n], i]
        # Add number into hash
        dict[n] = i
```
