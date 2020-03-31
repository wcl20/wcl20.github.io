---
layout: post
title: Merge Sort
---

## Problem
Merge Sort is a Divide and Conquer algorithm. It divides input array in two halves, calls itself for the two halves and then merges the two sorted halves.

Given an array of size $n$, sort the array using Merge Sort.

## Solution

Method 1
```python
def mergeSort(array: List[int]):
    # Check array is empty
    if array is None or len(array) < 2:
        return
    # Find midpoint of array
    mid = len(array) // 2
    # Split array
    left = array[:mid]
    right = array[mid:]
    # Sort subarrays
    mergeSort(left)
    mergeSort(right)
    # Merge left and right array
    array.clear()
    while left and right:
        # If first element of left is smaller
        if left[0] < right[0]:
            # Add element from left array
            array.append(left[0])
            # Remove first element from left
            left.pop(0)
        # Otherwise, first element of right is smaller
        else:
            # Add element from right subarray
            array.append(right[0])
            # Remove first element from right
            right.pop(0)
    # Add remaining elements
    array.extend(left)
    array.extend(right)
```

Method 2: Create only one auxiliary array instead of creating subarrays recursively.
```python
def mergeSort(array: List[int]):
    # Check array is empty
    if array is None or len(array) < 2:
        return
    # Create auxiliary array
    auxiliary = array.copy()
    mergeSortHelper(array, auxiliary, 0, len(array) - 1)

def mergeSortHelper(array: List[int], auxiliary: List[int], start: int, end: int):
    # Base Case
    if start >= end:
        return
    # Find midpoint of array
    mid = start + (end - start) // 2
    # Sort auxiliary array
    mergeSortHelper(auxiliary, array, start, mid)
    mergeSortHelper(auxiliary, array, mid + 1, end)
    # Copy sorted part of auxiliary to array
    merge(array, auxiliary, start, mid, end)

def merge(array: List[int], auxiliary: List[int], start: int, mid: int, end: int):
    left = start
    right = mid + 1
    # Merge subarray from start to end
    for i in range(start, end + 1):
        # If left subarray is 'empty'
        if left > mid:
            # Add rest of right subarray
            array[i] = auxiliary[right]
            right += 1
        # If right subarray is 'empty'
        elif right > end:
            # Add rest of left subarray
            array[i] = auxiliary[left]
            left += 1
        # If first element of left is smaller
        elif auxiliary[left] < auxiliary[right]:
            # Add first element of left
            array[i] = auxiliary[left]
            left += 1
        # If first element of right is smaller
        else:
            # Add first element of right
            array[i] = auxiliary[right]
            right += 1
```
