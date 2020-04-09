---
layout: post
title: Maximum In Sliding Window
subtitle: Coderust
---

## Problem
Given a large array of integers and a window of size $w$, find the current maximum value in the window as the window slides through the entire array.

Example: [-4, 2, -5, 3, 6] $w = 3$ should output [2, 3, 6]

## Solution

Use a stack to keep track of the current maximum element. The largest element is always at the top of the stack. Instead of keeping track of the elements, we can keep track of the index of the element such that we know when an element is out of the sliding window.

```python
def maxSlidingWindow(array: List[int], w: int):
    # Store indices of maximum element
    stack = []
    # Store result
    result = []
    # Loop through the first $w$ elements
    for i in range(w):
        # Remove elements from stack smaller than current element
        while stack and array[stack[-1]] <= array[i]:
            stack.pop()
        # Add current element to stack
        stack.append(i)
    # Append largest element to result
    result.append(array[stack[-1]])
    # Slide window through remaining list
    for i in range(w, len(array)):
        # Remove elements from stack smaller than current element
        while stack and array[stack[-1]] <= array[i]:
            stack.pop()
        # Remove element if it is out of window
        if stack and stack[-1] <= i - w:
            stack.pop()
        # Add current element to stack
        stack.append(i)
        # Append largest element to result
        result.append(array[stack[-1]])
    return result
```
