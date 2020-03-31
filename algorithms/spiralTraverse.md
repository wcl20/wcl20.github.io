---
layout: post
title: Spiral Matrix
subtitle: LeetCode
---

## Problem
Given a matrix of $m \times n$ elements ($m$ rows, $n$ columns), return all elements of the matrix in spiral order.

## Solution

Use four indices to keep track of start row, end row, start column and end column.

Method 1: Iterative Approach
```python
def spiralTraverse(matrix: List[List[int]]) -> List[int]:
    # Check matrix is empty
    if not matrix:
        return matrix
    # Get number of rows $m$
    m = len(matrix)
    # Get number of columns $n$
    n = len(matrix[0])
    # Keep track of start row, end row
    row_start, row_end = 0, m
    # Keep track os start column, end column
    col_start, col_end = 0, n
    # Spiral traverse
    result = []
    while row_start < row_end and col_start < col_end:
        # Traverse in right direction
        for i in range(col_start, col_end):
            result.append(matrix[row_start][i])
        # Traverse in downward direction
        for i in range(row_start + 1, row_end):
            result.append(matrix[i][col_end - 1])
        # Prevent traversing the same row twice
        if row_start + 1 < row_end:
            # Traverse in left direction
            for i in range(col_end - 2, col_start - 1, -1):
                result.append(matrix[row_end - 1][i])
        # Prevent traversing the same column twice
        if col_start + 1 < col_end:
            # Traverse in upward direction
            for i in range(row_end - 2, row_start, -1):
                result.append(matrix[i][col_start])
        # Move to inner loop
        row_start += 1
        row_end -= 1
        col_start += 1
        col_end -= 1
    return result
```

Method 2: Recursive Approach
```python
def spiralTraverse(matrix: List[List[int]]) -> List[int]:
    # Check matrix is empty
    if not matrix:
        return matrix
    # Get number of rows $m$
    m = len(matrix)
    # Get number of columns $n$
    n = len(matrix[0])
    result = []
    return spiralTraverseHelper(matrix, 0, m, 0, n, result)

def spiralTraverseHelper(matrix: List[List[int]], row_start: int, row_end: int, col_start: int, col_end: int, result: List[int]) -> List[int]:
    # Base case
    if row_start >= row_end or col_start >= col_end:
        return result
    # Traverse in right direction
    for i in range(col_start, col_end):
        result.append(matrix[row_start][i])
    # Traverse in downward direction
    for i in range(row_start + 1, row_end):
        result.append(matrix[i][col_end - 1])
    # Prevent traversing the same row twice
    if row_start + 1 < row_end:
        # Traverse in left direction
        for i in range(col_end - 2, col_start - 1, -1):
            result.append(matrix[row_end - 1][i])
    # Prevent traversing the same column twice
    if col_start + 1 < col_end:
        # Traverse in upward direction
        for i in range(row_end - 2, row_start, -1):
            result.append(matrix[i][col_start])
    # Move to inner loop
    return spiralTraverseHelper(matrix, row_start + 1, row_end - 1, col_start + 1, col_end - 1, result)
```
