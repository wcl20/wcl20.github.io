---
layout: post
title: Linked List Cycle
subtitle: LeetCode
---

## Problem
Given a linked list, determine if it has a cycle in it.

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

Linked List cycle can be detected using Floyd's Cycle-Finding algorithm. The algorithm traverses the linked list using two pointers $slow$ and $fast$. The $slow$ pointer moves by one step every time and the $fast$ pointer moves by two every time. If the pointers meet, there is a cycle in the linked list.

```python
def hasCycle(head: Node) -> bool:    
      # $slow$ pointer
      slow = head
      # $fast$ pointer
      fast = head
      # While not reaching end of list
      while slow and fast and fast.next:
          # Move $slow$ pointer by one
          slow = slow.next
          # Move $fast$ pointer by two
          fast = fast.next.next
          # If the two pointers meet ...
          if slow == fast:
              # ... A cycle is detected
              return True
      # No cycle detected
      return False
```

## Variations

Variation 1: The algorithm can be modified to find the first node in the loop.

Once the loop is found.
1. Position the $slow$ pointer to head of list. Keeping $fast$ at its current position.
2. Move $slow$ and $fast$ one step at a time until they meet.

```python
def firstCycleNode(head: Node) -> Node:    
      # $slow$ pointer
      slow = head
      # $fast$ pointer
      fast = head
      # While not reaching end of list
      while slow and fast and fast.next:
          # Move $slow$ pointer by one
          slow = slow.next
          # Move $fast$ pointer by two
          fast = fast.next.next
          # If the two pointers meet ...
          if slow == fast:
              break
      # If a cycle is detected
      if slow == fast:
          # Position $slow$ to head of list
          slow = head
          # Move $slow$ and $fast$ pointer until they meet
          while not slow == fast:
              slow = slow.next
              fast = fast.next
          # Return first element in loop
          return slow
      # No cycle detected
      return None
```
