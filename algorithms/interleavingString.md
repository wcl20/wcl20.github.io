---
layout: post
title: Interleaving String
subtitle: LeetCode
---

## Problem
Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

## Solution

This problem can be solved using Dynamic Programming.

We create a 2D matrix  $dp$ of size $m+1 \times n+1$ where $m$ is length of $s1$ and $n$ is length of $s2$.

$dp[i][j]$ is True if the string $s3[0...i+j]$ is an interleaving of $s1[0...i]$ and $s2[0...j]$.

The Base Cases are:

1. $i=0$ and $j=0$ is always True because interleaving empty strings gives an empty string.
2. $i=0$ then $dp[0][j]$ is True up to the point where $s3$ is different from $s2$.
3. $j=0$ then $dp[i][0]$ is True up to the point where $s3$ is different from $s1$.

After filling up the base case (first row and first column), we can fill up the remaining matrix from top left to bottom right.

1. Letter $s3[i+j-1]$ is the same as $s1[i-1]$ and $s2[j-1]$:
  * Move one letter ahead for $s1$ and recursively check.
  * Move one letter ahead for $s2$ and recursively check.
2. Letter $s3[i+j-1]$ is the same as $s1[i-1]$:
  * Move one letter ahead for $s1$ and recursively check.
3. Letter $s3[i+j-1]$ is the same as $s2[j-1]$:
  * Move one letter ahead for $s2$ and recursively check.

```python
def isInterleave(s1: str, s2: str, s3: str) -> bool:
    # Get length of string1
    m = len(s1)
    # Get length of string2
    n = len(s2)
    # If length of s3 is not m + n return false
    if not len(s3) == m + n:
        return False
    # Create 2D matrix to store subproblems (Dynamic Programming)
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    # Fill matrix from upper left to lower right corner
    for i in range(m + 1):
        for j in range(n + 1):
            # Base case 1:
            if i == 0 and j == 0:
                dp[i][j] = True
            # Base case 2:
            elif i == 0:
                dp[i][j] = dp[i][j-1] and s3[j - 1] == s2[j-1]
            # Base case 3:
            elif j == 0:
                dp[i][j] = dp[i-1][j] and s3[i - 1] == s1[i-1]
            # Case 1: Current character is same as head of s1 and s2
            elif s3[i + j - 1] == s1[i-1] and s3[i + j - 1] == s2[j-1]:
                # Move a letter ahead for s1
                # Move a letter ahead for s2
                dp[i][j] = dp[i-1][j] or dp[i][j-1]
            # Case 2: Current character is same as head of s1
            elif s3[i + j - 1] == s1[i-1]:
                # Move a letter ahead for s1
                dp[i][j] = dp[i-1][j]
            # Case 3: Current character is same as head of s2
            elif s3[i + j - 1] == s2[j-1]:
                # Move a letter ahead for s2
                dp[i][j] = dp[i][j-1]
    return dp[-1][-1]
```
