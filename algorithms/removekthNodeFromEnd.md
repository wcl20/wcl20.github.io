---
layout: post
title: Remove Kth Node From End
subtitle: LeetCode
---

## Problem
Given a linked list, remove the $k$-th node from the end of list and return its head. Given $k$ is always valid.

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

Finding the $k^{th}$ node from end can be done using two pointers.
1. Move a $fast$ pointer $k$ node forward
2. Move $slow$ and $fast$ pointer one step at a time. When $fast$ reaches the end of list, $slow$ points to $k^{th}$ node from end.

Since we are removing the $k^{th}$ node from end, we want to find its previous node ($k+1^{th}$ node from end).

```python
def removeKthFromEnd(head: Node, k: int):
    # Create two pointers
    slow = head
    fast = head
    # Move fast pointer $k$ step forward
    for _ in range(k):
        fast = fast.next
    # If fast reaches end of list
    if not fast:
        # $k^{th}$ element from end is head
        head = head.next
    else:
        # Find $k+1^{th}$ node from end
        while fast.next:
            slow = slow.next
            fast = fast.next
        # Remove the $k^{th}$ node
        slow.next = slow.next.next
    return head          
```
