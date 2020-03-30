---
layout: post
title: Search a Rotated Array
subtitle: Coderust
---

## Problem
Search for a given number in a sorted array, with unique elements, that has been rotated by some arbitrary number. Return -1 if the number does not exist.

## Solution

The solution is essentially a binary search but with some modifications.
In each iteration in the Binary Search, either:
  * The first half of the array is fully sorted.
  * The second half of the array is fully sorted.
  * The full array is fully sorted.
In the first case, search the first half of the array if the target is within the range of first subarray. Otherwise, search second half of the array.
In the second case, search the second half of the array if the target is within the range of second subarray. Otherwise, search first half of the array.
In the third case, this is just a normal binary search.

Method 1: Iterative Implementation
```python
def shiftedBinarySearch(array: List[int], target: int) -> int:
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
        # Case 1: First half of array is sorted
        if array[left] < array[mid]:
            # If target is within range of first half ...
            if array[left] <= target < array[mid]:
                # Search first half
                right = mid - 1
            else:
                # Otherwise, search second half
                left = mid + 1
        # Case 2: Second half of array is sorted
        else:
            # If target is within range of second half ...
            if array[mid] < target <= array[right]:
                # Search second half
                left = mid + 1
            else:
                # Otherwise, search first half
                right = mid - 1
    # Out of range, element is not in array
    return -1
```

Method 2: Recursive Implementation
```python
def shiftedBinarySearch(array: List[int], target: int) -> int:
    # Check array is not empty
    if array is None or len(array) < 1:
        return -1
    # Binary search
    return shiftedBinarySearchHelper(array, target, 0, len(array) - 1)

def shiftedBinarySearchHelper(array: List[int], target: int, left: int, right: int) -> int:
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
    # Case 1: First half of array is sorted
    if array[left] < array[mid]:
        # If target is within range of first half ...
        if array[left] <= target < array[mid]:
            # Search first half
            return shiftedBinarySearchHelper(array, target, left, mid - 1)
        else:
            # Otherwise, search second half
            return shiftedBinarySearchHelper(array, target, mid + 1, right)
    # Case 2: Second half of array is sorted
    else:
        # If target is within range of second half ...
        if array[mid] < target <= array[right]:
            # Search second half
            return shiftedBinarySearchHelper(array, target, mid + 1, right)
        else:
            # Otherwise, search first half
            return shiftedBinarySearchHelper(array, target, left, mid - 1)
```
