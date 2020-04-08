---
layout: post
title: Longest Common Subsequence
subtitle: LeetCode
---

## Problem
Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters. (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings is a subsequence that is common to both strings.

## Solution

Consider two input sequences $a[0...n]$ and $b[0...m]$. The longest common subsequence is defined as follow, starting from $i = n$ and $j = m$.

$$
lcs_{a,b}(i,j) =
\begin{cases}
0,
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
\text{if } min(i,j) = 0\\
lcs_{a,b}(i - 1, j - 1) + 1,
\;\;\;\;\;\;\;\;\text{if } a[i] = b[j]\\
max
\begin{cases}
lcs_{a,b}(i, j - 1)\\
lcs_{a,b}(i - 1, j)\\
\end{cases}
\;\;\;\;\;\;\;\;\;\text{Otherwise}
\end{cases}
$$

Where
* $a$: First string
* $b$: Second string
* $i$: Character position of string $a$
* $j$: Character position of string $b$

```python
def longestCommonSubsequence(a: str, b: str) -> int:
    # Create 2D matrix to store subproblems (Dynamic Programming)
    dp = [[0 for _ in range(len(b) + 1)] for _ in range(len(a) + 1)]
    # Fill in dp in bottom up manner
    for i in range(1, len(a) + 1):
        for j in range(1, len(b) + 1):
            # Case a[i] = b[j]
            if a[i-1] == b[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            # Otherwise, the characters are different
            else:
                # Find larger longest common subsequence between:
                # 1. Removing a character from a
                # 2. Removing a character from b
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    return dp[-1][-1]
```
