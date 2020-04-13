---
layout: post
title: Same Tree
subtitle: LeetCode
---

## Problem
Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

A BT Node
```python
class Node:
    def __init__(self, value):
        # Value stored in node
        self.value = value
        # Right child
        self.right = None
        # Left child
        self.left = None
```

## Solution

```python
def isSameTree(p: Node, q: Node):
    # Base case
    if not p and not q:
        return True
    if not p and q:
        return False
    if p and not q:
        return False
    # Check left subtree
    if not isSameTree(p.left, q.left):
        return False
    # Check right subtree
    if not isSameTree(p.right, q.right):
        return False
    # Check node has same value
    return p.value == q.value  
```
