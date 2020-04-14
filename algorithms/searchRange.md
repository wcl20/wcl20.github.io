---
layout: post
title: Find First and Last Position of Element in Sorted Array
subtitle: LeetCode
---

## Problem
Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

If the target is not found, return [-1, -1].

## Solution
The solution uses a variation of Binary Search.

When searching for the low index, we do not stop when we found the target but continue to search for the first part of the array to find a smaller index. 

When searching for the high index, we do not stop when we found the target but continue to search for the second part of the array to find a larger index.

```python
def searchRange(array: List[int], target: int):
    # Search for low index
    low = lowIndex(array, target)
    # Search for high index
    high = highIndex(array, target)
    # Return range
    return [low, high]

def lowIndex(array: List[int], target: int):
    # Create start and end pointers for search range (begin with full array)
    start, end = 0, len(array) - 1
    # While in search range
    while start <= end:
        # Calculate midpoint
        mid = (start + end) // 2
        # Get value at midpoint
        value = array[mid]
        # If target found ...
        if value == target:
            # Search first half to find smaller index
            end = mid - 1
        # If middle value is larger than target ...
        elif value > target:
            # Search first half
            end = mid - 1
        # middle value is smaller than target ...
        else:
            # Search second half
            start = mid + 1
    # When loop breaks, start points to the lowest index if target exists
    return start if start < len(array) and array[start] == target else -1

def highIndex(array: List[int], target: int):
    # Create start and end pointers for search range (begin with full array)
    start, end = 0, len(array) - 1
    # While in search range
    while start <= end:
        # Calculate midpoint
        mid = (start + end) // 2
        # Get value at midpoint
        value = array[mid]
        # If target found ...
        if value == target:
            # Search second half to find larger index
            start = mid + 1
        # If middle value is larger than target ...
        elif value > target:
            # Search first half
            end = mid - 1
        # middle value is smaller than target ...
        else:
            # Search second half
            start = mid + 1
    # When loop breaks, end points to the highest index if target exists
    return end if end >= 0 and array[end] == target else -1                
```
