---
layout: post
title: Path Sum
subtitle: LeetCode
---

## Problem
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

A BST Node
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
def pathSum(root: Node, sum: int):
    # Base case: leaf node
    if not root:
        return sum == 0
    # Calculate remaining sum
    remaining = sum - root.value
    # Traverse left and right subtree
    return pathSum(root.left, remaining) or pathSum(root.right, remaining)
```
