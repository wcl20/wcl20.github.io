---
layout: post
title: Binary Tree Level Order Traversal
subtitle: LeetCode
---

## Problem
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

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
def levelOrder(root: Node) -> List[List[int]]:
    # Create list to store results
    levels = []
    # Check root is not null
    if not root:
      return levels
    # Create a queue and append root node
    queue = [root]
    # While queue is not empty
    while queue:
        # Create list to store elements in this level
        level = []
        # Get number of elements in this level
        n = len(queue)
        # For each element in the level
        for _ in range(n):
            node = queue.pop(0)
            # Append value to list
            level.append(node.value)
            # Add left child to queue
            if node.left:
                queue.append(node.left)
            # Add right child to queue
            if node.right:
                queue.append(node.right)
        # Append level to result list
        levels.append(level)
    return levels
```
