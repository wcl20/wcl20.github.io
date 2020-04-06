---
layout: post
title: Construct BST From Preorder Traversal
subtitle: LeetCode
---

## Problem
Return the root node of a binary search tree that matches the given preorder traversal.

Preorder traversal displays the value of the node first, then traverses to left child, then traverses to right child.

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

1. Create a Stack.
2. Create root node using first value and add to stack.
3. Iterate the rest of the array:
  * If $num$ is less than top of stack $top$, make $num$ the left child of $top$.
  * If $num$ is larger than top of stack $top$, keep popping stack until it finds the largest $top$ smaller than $num$, make $num$ the right child of $top$.
  * Append $num$ to stack.

Example: preorder array [8, 5, 1, 7, 10, 12]

Iteration 1:
stack: [8]           
Tree: { 8 }

Iteration 2:
stack: [8, 5]        
Tree: { 8: { 5, Null }}

Iteration 3:
stack: [8, 5, 1]     
Tree: { 8: { 5: { 1, Null }, Null }}

Iteration 4:
stack: [8, 7]        
Tree: { 8: { 5: { 1, 7 }, Null }}

Iteration 5:
stack: [10]         
 Tree: { 8: { 5: { 1, 7 }, 10: { Null, Null }}}

Iteration 6:
stack: [12]          
Tree: { 8: { 5: { 1, 7 }, 10: { Null, 12 }}}

```python
def constructBST(array: List[int]) -> Node:
    # Make first element as root
    root = Node(array[0])
    # Create a stack and append root
    stack = [root]
    # Iterate the rest of the array
    for num in array[1:]:
        # Create a node for each number
        node = Node(num)
        # Peek top node
        parent = stack[-1]
        # If current value is less than top of stack
        if num < parent.value:
            # Append current value as left child
            parent.left = node
        # If current value is larger than top of stack
        else:
            # Find the largest parent smaller than current value
            while stack and num > stack[-1].value:
                parent = stack.pop()
            # Append current value as right child
            parent.right = node
        # Add node to stack
        stack.append(node)
    return root
```
