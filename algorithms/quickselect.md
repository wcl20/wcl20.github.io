---
layout: post
title: Quickselect
---

## Problem
Quickselect is a selection algorithm to find the $k^{th}$ smallest element in an unordered list. It is related to the quick sort sorting algorithm.

## Solution
The algorithm is similar to QuickSort. The difference is, instead of recurring for both sides (after finding pivot), it recurs only for the part that contains the $k^{th}$ smallest element.

At each iteration:

* If the index of the partition element is $k$, $k^{th}$ smallest element found.
* If the index of the partition element $<k$, recursively search the right subarray.
* If the index of the partition element $>k$, recursively search the left subarray.

```python
def quickselect(array: List[int], k:int):
    # Find $k$ smallest using quickselect
    quickselectHelper(array, 0, len(array) - 1, k)

def quickselectHelper(array: List[int], start: int, end: int, k: int):
    pivot = partition(array, start, end)
    # If index of partition is $k$
    if pivot == k - 1:
        return array[pivot]
    # If index of partition is $<k$
    if pivot < k - 1:
        # Search for right subarray
        return quickselectHelper(array, pivot + 1, end, k)
    else:
        # Search for left subarray
        return quickselectHelper(array, start, pivot - 1, k)

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

Variation 1: Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

The $k^{th}$ largest element in an array is $n - k + 1$ smallest element where $n$ is the number of elements in the array.

```python
def quickselect(array: List[int], k:int):
    # $kth$ largest is $n-k+1$ smallest element
    k = len(array) - k + 1
    # Find $k$ smallest using quickselect
    quickselectHelper(array, 0, len(array) - 1, k)

def quickselectHelper(array: List[int], start: int, end: int, k: int):
    pivot = partition(array, start, end)
    # If index of partition is $k$
    if pivot == k - 1:
        return array[pivot]
    # If index of partition is $<k$
    if pivot < k - 1:
        # Search for right subarray
        return quickselectHelper(array, pivot + 1, end, k)
    else:
        # Search for left subarray
        return quickselectHelper(array, start, pivot - 1, k)

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
