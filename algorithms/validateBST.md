---
layout: post
title:  Validate BST
subtitle: LeetCode
---

## Problem
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys less than the node's key.
* The right subtree of a node contains only nodes with keys greater than the node's key.
* Both the left and right subtrees must also be binary search trees.

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
def isValid(root: Node) -> bool:
    return isValidHelper(root, float("-inf"), float("inf"))

def isValidHelper(node: Node, minimum: int, maximum: int) -> bool:
    # Check node exists
    if not node:
        return True
    # Check node value is within range
    value = node.value
    if value <= minimum or value >= maximum:
        return False
    # Recursively check subtrees (left)
    valid_left = isValidHelper(node.left, minimum, value)
    # Recursively check subtrees (right)
    valid_right = isValidHelper(node.right, value, maximum)
    # Return True is both subtrees are valid
    return valid_left and valid_right
```
