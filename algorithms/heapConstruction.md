---
layout: post
title: Heap Construction
---

## Problem
Given an array of N elements. The task is to build a Binary Heap from the given array. The heap can be either Max Heap or Min Heap.

A Binary Heap is a Binary Tree with following properties:
1. It is a complete tree. All levels are completely filled except possibly the last level and the last level has all keys as left as possible.
2. In a Max heap, the key at the root must be maximum among all values in the heap. The same property must be recursively true for all nodes in Binary Tree.
3. In a Min heap, the key at the root must be minimum among all values in the heap. The same property must be recursively true for all nodes in Binary Tree.

## Solution

Array representation of a Heap:
1. Root is at index 0 of the array
2. Left child of the $i^{th}$ node is at index $2 \times i + 1$.
3. Right child of the $i^{th}$ node is at index $2 \times i + 2$.
4. Parent of the $i^{th}$ node is at index $(i - 1) // 2$

Heapify each non-leaf node in reverse order.

Max Heap Construction
```python
def heapConstruction(array: List[int]):
    # Get number of items
    n = len(array)
    # Get index of last non-leaf node (Parent of last node)
    start = (n - 2) // 2
    # Heapify each node in reverse order
    for index in range(start, -1, -1):
        heapify(array, index)

def heapify(array: List[int], index: int):
    # Get left child
    left = 2 * index + 1
    # Get right child
    right = 2 * index + 2
    # Find largest of current node, left child and right child
    largest = index
    if left < len(array) and array[left] > array[largest]:
        largest = left
    if right < len(array) and array[right] > array[largest]:
        largest = right
    # If current node is not the largest
    if not largest == index:
        # Swap current node with larger child
        array[index], array[largest] = array[largest], array[index]
        # Continue heapify larger child
        heapify(array, largest)
```

Min Heap Construction
```python
def heapConstruction(array: List[int]):
    # Get number of items
    n = len(array)
    # Get index of last non-leaf node (Parent of last node)
    start = (n - 2) // 2
    # Heapify each node in reverse order
    for index in range(start, -1, -1):
        heapify(array, index)

def heapify(array: List[int], index: int):
    # Get left child
    left = 2 * index + 1
    # Get right child
    right = 2 * index + 2
    # Find smallest of current node, left child and right child
    smallest = index
    if left < len(array) and array[left] < array[smallest]:
        smallest = left
    if right < len(array) and array[right] < array[smallest]:
        smallest = right
    # If current node is not the smallest
    if not smallest == index:
        # Swap current node with smaller child
        array[index], array[smallest] = array[smallest], array[index]
        # Continue heapify larger child
        heapify(array, smallest)
```
