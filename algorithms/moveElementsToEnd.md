---
layout: post
title: Move Zeroes
subtitle: LeetCode
---

## Problem
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

## Solution

```python
def moveZeroes(array: List[int]):
    # Current position of write pointer
    end = 0
    # Iterate the array
    for num in array:
        # If the number is not 0
        if not num == 0:
            # write the element to front
            array[end] = num
            end += 1
    # Fill all remaining space after write pointer with 0
    while end < len(array):
        array[end] = 0
        end += 1
```
