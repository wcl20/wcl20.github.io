---
layout: post
title: Search a 2D Matrix
subtitle: LeetCode
---

## Problem
Write an efficient algorithm that searches for a value in an $m \times n$ matrix. This matrix has the following properties:

1. Integers in each row are sorted from left to right.
2. The first integer of each row is greater than the last integer of the previous row.

## Solution

```python
def searchMatrix(matrix: List[List[int]], target: int) -> bool:
    # Check matrix is not empty
    if not matrix:
        return False
    # Get number of rows $m$
    m = len(matrix)
    # Get number of columns $n$
    n = len(matrix[0])
    # Start from top right corner of matrix
    x, y = 0, n - 1
    while x < m and y >= 0:
        # Get current element
        value = matrix[x][y]
        # If value found ...
        if value == target:
            return True
        # If value is less than target ...
        elif value < target:
            # ... Search next row
            x += 1
        # If value is larger than target ...
        else:
            # ... Search previous element in row
            y -= 1
    return False    
```
