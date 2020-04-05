---
layout: post
title: Bubble Sort
---

## Problem
Heap sort is a comparison based sorting technique based on Binary Heap data structure. It is similar to selection sort where we first find the maximum element and place the maximum element at the end. We repeat the same process for remaining element.

Given an array of size $n$, sort the array using Heap Sort.

## Solution

1. Build a max heap from input.
2. Swap root of heap with last element and heapify root.
3. Repeat step 2 for $n - 1$ iterations.

```python
def heapSort(array: List[int]):
    # Get number of items
    n = len(array)
    # Build max heap
    start = (n - 2) // 2
    for index in range(start, -1, -1):
        heapify(array, index, n)
    # Iterate array $n - 1$ times
    for end in range(n - 1, 0, -1):
        # Swap root with last element
        array[0], array[end] = array[end], array[0]
        # Heapify root node (everything after end is already sorted)
        heapify(array, 0, end)

def heapify(array: List[int], index: int, end: int):
    # Get left child
    left = 2 * index + 1
    # Get right child
    right = 2 * index + 2
    # Find largest of current node, left child and right child
    largest = index
    if left < end and array[left] > array[largest]:
        largest = left
    if right < end and array[right] > array[largest]:
        largest = right
    # If current node is not the largest
    if not largest == index:
        # Swap current node with larger child
        array[index], array[largest] = array[largest], array[index]
        # Continue heapify larger child
        heapify(array, largest, end)
```
