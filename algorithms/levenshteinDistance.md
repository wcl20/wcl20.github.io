---
layout: post
title: Edit Distance
subtitle: Hackerrank
---

## Problem
"Edit distance" (also known as Levenshtein distance) measures the minimum the number of simple changes to move from one string to another. Possible changes include the insertion of a single character, the deletion of a single character, or the substitution from one character to another. Your program must calculate edit distance between pairs of strings.

Mathematically, the Levenshtein Distance between two strings $a$ and $b$ is given by

$$
lev_{a,b}(i,j) =
\begin{cases}
max(i,j),
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
\text{if } min(i,j) = 0\\
min
\begin{cases}
lev_{a,b}(i-1, j) + 1\\
lev_{a,b}(i, j-1) + 1\\
lev_{a,b}(i-1, j-1) + 1_{a_i \neq b_j}
\end{cases}
\;\;\;\text{Otherwise}
\end{cases}
$$

Where
* $a$: First string
* $b$: Second string
* $i$: Character position of string $a$
* $j$: Character position of string $b$

## Solution

1. Create a 2D matrix of size $(m+1) \times (n+1)$ where $m$ is the length of string $a$ and $n$ is the length of string $b$.
2. Fill the matrix from upper left to lower right corner.
3. The final result is the value at lower right corner.

```python
def levenshteinDistance(a: string, b: string) -> int:
    # Create 2D matrix to store subproblems (Dynamic Programming)
    dp = [[0 for _ in range(len(b) + 1)] for _ in range(len(a) + 1)]
    # Fill matrix from upper left to lower right corner
    for i in range(len(a) + 1):
        for j in range(len(b) + 1):
            # Case $min(i,j) = 0$:
            if min(i, j) == 0:
                # $lev_{a,b}(i,j) = max(i,j)$
                dp[i][j] = max(i, j)
            else:
                # Insertion: $lev_{a,b}(i-1, j) + 1$
                insertion = dp[i-1][j] + 1
                # Deletion: $lev_{a,b}(i, j-1) + 1$
                deletion = dp[i][j-1] + 1
                # Substitution: $lev_{a,b}(i-1, j-1) + 1_{a_i \neq b_j}$
                c = 0 if a[i-1] == b[j-1] else 1
                substitution = dp[i-1][j-1] + c
                # Compute $lev_{a,b}(i,j)$
                dp[i][j] = min(insertion, deletion, substitution)
    # Return value at lower right corner
    return dp[-1][-1]
```
