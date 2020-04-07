---
layout: post
title: Merge K Sorted Linked Lists
subtitle: LeetCode
---

## Problem
Merge k sorted linked lists and return it as one sorted list.

A Linked List Node
```python
class Node:
    def __init__(self, value):
        # Value stored in node
        self.value = value
        # Next value in list
        self.next = None
```

## Solution

1. Create a $merge$ function that merges two sorted lists into one
2. Use Divide and Conquer approach on the list of lists:
    * Merge first and last
    * Merge second and second last ...
    * Until there is only one list left

```python
def mergeKLists(lists: List[Node]):
    # Check lists is not empty
    if not lists:
        return None
    # While there is more than one lists
    while len(lists) > 1:
        # Get number of remaining lists
        n = len(lists)
        # Merge first and last and store in first,
        # Merge second and second last and store in second ...
        for i in range(n // 2):
            lists[i] = merge(lists[i], lists[-i-1])
        # Remove already merged lists
        lists = lists[:(n + 1) // 2]
    # Return first of all lists
    return lists[0]

def merge(list1: Node, list2: Node):
    # Base case: Check list not not empty
    if not list1 or not list2:
        return list1 if list1 else list2
    # If head of list1 is smaller than head of list2 ...
    if list1.value < list2.value:
        # Set head to list1 and recursively merge rest
        merge = list1
        merge.next = merge(list1.next, list2)
    else:
        # Set head to list2 and recursively merge rest
        merge = list2
        merge.next = merge(list1, list2.next)
    return merge
```
