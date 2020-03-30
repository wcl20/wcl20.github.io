---
layout: post
title: Binary Search
---

## Problem
Given a sorted array of $n$ elements. Use Binary Search to return the position of a given element in the array.

## Solution

Begin with an interval covering the whole array. If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half. Otherwise narrow it to the upper half. Repeatedly check until the value is found or the interval is empty.

Method 1: Iterative Implementation
```python
def binarySearch(array: List[int], target: int) -> int:
    # Check array is not empty
    if array is None or len(array) < 1:
        return -1
    # Create left and right pointers for search range (begin with full array)
    left, right = 0, len(array) - 1
    # Search in range
    while left <= right:
        # Calculate midpoint
        mid = left + (right - left) // 2
        # Get value at midpoint
        value = array[mid]
        # If value found ...
        if value == target:
            # return index
            return mid
        # If middle value is larger than target
        if value > target:
            # Search first half of array
            right = mid - 1
        # Otherwise, middle value is smaller than target
        else:
            # Search second half of array
            left = mid + 1
    # Out of range, element is not in array
    return -1
```

Method 2: Recursive Implementation
```python
def binarySearch(array: List[int], target: int) -> int:
    # Check array is not empty
    if array is None or len(array) < 1:
        return -1
    # Binary search
    return binarySearchHelper(array, target, 0, len(array) - 1)

def binarySearchHelper(array: List[int], target: int, left: int, right: int) -> int:
    # Base case: Not in range
    if left > right:
        # Element is not in array
        return -1
    # Calculate midpoint
    mid = left + (right - left) // 2
    # Get value at midpoint
    value = array[mid]
    # If value found ...
    if value == target:
        # ... return index
        return mid
    # If middle value is larger than target
    if value > target:
        # Search first half of array
        return binarySearchHelper(array, target, left, mid - 1)
    # Otherwise, middle value is smaller than target
    else:
        # Search second half of array
        return binarySearchHelper(array, target, mid + 1, right)
```
