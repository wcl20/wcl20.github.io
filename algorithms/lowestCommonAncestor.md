---
layout: post
title: Lowest Common Ancestor of a Binary Tree
subtitle: LeetCode
---

## Problem
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

The lowest common ancestor is defined between two nodes $p$ and $q$ as the lowest node in $T$ that has both $p$ and $q$ as descendants (where we allow a node to be a descendant of itself).

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

Start from root and traverse the tree:

1. If reached end of tree, return null
2. If current root is $p$ or $q$, return current root
3. If $p$ and $q$ are in different subtrees, return current root
4. If $p$ and $q$ are in same subtree, recursively find solution in the subtree.

```python
def lowestCommonAncestor(root: Node, p: Node, q: Node):
    # Case 1: root is null
    if not root:
        return None
    # Case 2: root is $p$ or $q$
    if root == p or root == q:
        return root
    # Check left and right subtree
    left = lowestCommonAncestor(root.left, p, q)
    right = lowestCommonAncestor(root.right, p, q)
    # Case 3: $p$ and $q$ are in different subtrees
    if left and right:
        return root
    # Case 3: $p$ and $q$ are in same subtree
    if left:
        # $p$ and $q$ are in left subtree
        return left
    else:
        # $p$ and $q$ are in right subtree
        return right    
```
