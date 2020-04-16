---
layout: post
title: Flatten Binary Tree to Linked List
subtitle: LeetCode
---

## Problem
Given a binary tree, flatten it to a linked list in-place. Usage of auxiliary data structure is not allowed.


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

Example: Given a binary tree { 1: { 2: { 3, 4 }}, { 5: { Null, 6 }}}

The output is { 1: Null, { 2: { Null, { 3: { Null, { 4: { Null, { 5: { Null , 6 }}}}}}}}}

## Solution

The way to visualise this is everything in the left subtree is flatten into a line $left$.

$left$ becomes the right child of the root, and the original right child is append to the last element of $left$.

```python
def flatten(root: Node):
    # Base case
    if not root:
        return
    # If the root has a left subtree ...
    if root.left:
        # Flatten left subtree
        flatten(root.left)
        # Save current right child
        right = root.right
        # Flattened left subtree becomes right child
        root.right = root.left
        root.left = None
        # Find the end of flattened left subtree
        current = root 
        while current.right:
            current = current.right
        # Append original right child to end of flattened left subtree
        current.right = right
    # Flatten right subtree
    flatten(root.right)      
```
