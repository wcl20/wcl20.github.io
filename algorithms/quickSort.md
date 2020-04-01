---
layout: post
title: Quick Sort
---

## Problem
QuickSort is a Divide and Conquer algorithm. It picks an element as pivot and partitions the given array around the picked pivot.

Given an array of size $n$, sort the array using Quick Sort.

## Solution

```python
def quickSort(array: List[int]):
    quickSortHelper(array, 0, len(array) - 1)

def quickSortHelper(array: List[int], start: int, end: int):
    # Base Case
    if start >= end:
        return
    # Partition array
    pivot = partition(array, start, end)
    # Sort first partition
    quickSortHelper(array, start, pivot - 1)
    # Sort second partition
    quickSortHelper(array, pivot + 1, end)

def partition(array: List[int], start: int, end: int):
    # Select last element as pivot
    pivot = array[end]
    # Keep track of position of the last element in smaller partition
    low = start
    # Iterate array
    for i in range(start, end):
        # If current element is smaller than pivot
        if array[i] < pivot:
            # Put element to smaller partition
            array[low], array[i] = array[i], array[low]
            low += 1
    # Put pivot to correct position
    array[low], array[end] = array[end], array[low]
    # Return position of pivot
    return low
```

## Variations

Variation of Quick Sort uses different methods to select pivots:
* Pick random element as pivot
* Pick median of three elements as pivot

Variation 1: Median of Three Pivot
```python
def partition(array: List[int], start: int, end: int):
    # Select three numbers from array
    mid = start + (end - start) // 2
    pivots = [array[start], array[mid], array[end]]
    # Find median of three numbers
    pivots.sort()
    pivot = pivots[1]
    # Swap pivot with last element
    if pivot == array[start]:
        array[start], array[end] = array[end], array[start]
    elif pivot == array[mid]:
        array[mid], array[end] = array[end], array[mid]
    # Keep track of position of the last element in smaller partition
    low = start
    # Iterate array
    for i in range(start, end):
        # If current element is smaller than pivot
        if array[i] < pivot:
            # Put element to smaller partition
            array[low], array[i] = array[i], array[low]
            low += 1
    # Put pivot to correct position
    array[low], array[end] = array[end], array[low]
    # Return position of pivot
    return low
```
