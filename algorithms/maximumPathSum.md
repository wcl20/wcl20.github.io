---
layout: post
title: Binary Tree Maximum Path Sum
subtitle: LeetCode
---

## Problem
Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

Example: { -10: { left: 9, right: { 20: { left: 15, right: 7 }}}}

The maximum path sum if 42 formed by right subtree { 20: { left: 15, right: 7 }}

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

Traversing from the root of the tree, we update the maximum path sum considering each node as the root. When considering each node as root, there are four different cases:

1. The node itself is the maximum path sum.
{ 5: { left: -1, right: -3 }}
2. The node and left branch is the maximum path sum.
{ 5: { left: { 1: { left: 2, right: 5 }}, right: -1 }}
3. The node and right branch is the maximum path sum.
{ 5: { left: -1, right: 7}}
4. The node and left branch and right branch is the maximum path sum.
{ 5: { left: 1, right: 2 }}

The $maxPathSumHelper$ function has two functions:
1. It considers the current node as root and updates the maximum path sum.
2. It returns the maximum branch sum with starting from the current node.

```python
def maxPathSum(root: Node) -> int:
    # Keep track of the maximum path sum
    maximum = [float("-inf")]
    # Traverse tree starting from root
    maxPathSumHelper(root, maximum)
    # Return maximum
    return maximum[0]

def maxPathSumHelper(node: Node, maximum: List[int]) -> int:
    # Base case: Reached end of tree
    if not node:
        return 0
    # Traverse left subtree (Returns max branch sum starting from left child)
    left = maxPathSumHelper(node.left, maximum)
    # Traverse right subtree (Returns max branch sum starting from right child)
    right = maxPathSumHelper(node.right, maximum)
    # Consider current node as root and update maximum
    # Case 1: Node itself is maximum
    maximum[0] = max(maximum[0], node.value)
    # Case 2: Node and left branch is maximum
    maximum[0] = max(maximum[0], node.value + left)
    # Case 3: Node and right branch is maximum
    maximum[0] = max(maximum[0], node.value + right)
    # Case 4: Node and left and right branch is maximum
    maximum[0] = max(maximum[0], node.value + left + right)
    # Returns maximum branch staring from current node
    return max(left, right, 0) + node.value
```
