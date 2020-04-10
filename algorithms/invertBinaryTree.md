---
layout: post
title: Invert Binary Tree
subtitle: LeetCode
---

## Problem
Invert a binary tree.

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
def invertTree(root: Node) -> Node:
    # Base Case: Reached end of tree
    if not root:
        return None
    # Invert left subtree
    invertTree(root.left)
    # Invert right subtree
    invertTree(root.right)
    # Swap left and right subtree
    root.left, root.right = root.right, root.left
    return root
```
