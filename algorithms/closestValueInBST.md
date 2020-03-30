---
layout: post
title: Closest Value in BST
subtitle: LeetCode
---

## Problem
Given a binary search tree and a target node $k$. The task is to find a node with minimum absolute difference with given target value $k$.

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

Method 1: Recursion
```python
def closestValue(root: Node, target: int) -> int:
    # Store closest value
    closest = [float('inf')]
    # Recursive helper function
    closestValueHelper(root, target, closest)
    return closest[0]

def closestValueHelper(node: Node, target: int, closest: List[int]):
    # Base case: node if a leaf node
    if node is None:
        return
    # Obtain value of current node
    value = node.value
    # Calculate difference from target
    difference = abs(value - target)
    # If absolute difference is smaller than current closest ...
    if difference < abs(closest[0] - target):
        # ... update closest value
        closest[0] = node.value
    # If value is smaller than target ...
    if value < target:
        # ... check right subtree
        closestValueHelper(node.right, target, closest)
    else:
        # Otherwise, check left subtree
        closestValueHelper(node.left, target, closest)  
```

Method 2: Iteration
```python
def closestValue(root: Node, target: int) -> int:
    # Store closest value
    closest = root.value
    # Start from root
    node = root
    # While not reached left node ...
    while not node is None:
        # ... Obtain value of current node
        value = node.value
        # Return value if value is exactly target
        if value == target:
            return value
        # Calculate difference from target
        difference = abs(value - target)
        # If absolute difference is smaller than current closest ...
        if difference < abs(closest - target):
            # ... update closest value
            closest = value
        # If value is smaller than target ...
        if value < target:
            # ... check right subtree
            node = node.right
        else:
            # Otherwise, check left subtree
            node = node.left
    return closest
```
