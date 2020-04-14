---
layout: post
title: Binary Tree Inorder Traversal
subtitle: LeetCode
---

## Problem
Given a binary tree, return the inorder traversal of its nodes values.

Inorder traversal first visits the left node, then the current node at the end the right node.

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
def inorderTraversal(root: Node) -> List[int]:
    # Create a stack
    stack = []
    # Start at root node
    current = root
    # Push every node on the left branch into the stack
    while current:
        stack.append(current)
        current = current.left
    # While stack is not empty
    nodes = []
    while stack:
        # Get the node at furthest left
        node = stack.pop()
        # Visit node
        nodes.append(node.value)
        # Start at right child of current node
        current = node.right
        # Push every node on the left branch into the stack
        while current:
            stack.append(current)
            current = current.left
    return nodes  
```
