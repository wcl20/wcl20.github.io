---
layout: post
title: Reverse a Singly Linked List
subtitle: Coderust
---

## Problem
Reverse the singly linked list and return the pointer/reference to the head of the reversed linked list.

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

Method 1: Iterative Approach
Iterate through the linked list, reversing elements one by one.
```python
def reverse(head: Node):
    # Check list is empty or contains only one element
    if not head or not head.next:
        return
    # Pointer to head of reversed list
    reversed = head
    # Pointer to head of remaining list
    current = head.next
    reversed.next = None
    while current:
        # Store next node in remaining list
        next = current.next
        # Reverse list
        current.next = reversed
        reversed = current
        # Move to next node
        current = next
    return reversed
```

Method 2: Recursive Approach
Reverse remaining list then append head to end of list.
```python
def reverse(head: Node):
    # Check list is empty or contains only one element
    if not head or not head.next:
        return
    # Reverse remaining list
    reversed = reverse(head.next)
    # head.next points to end of reversed list
    head.next.next = head
    head.next = None
    return reversed
```
