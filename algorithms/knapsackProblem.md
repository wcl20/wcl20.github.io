---
layout: post
title: Knapsack Problem
---

## Problem
Given weights and values of $n$ items, put these items in a knapsack of capacity $W$ to get the maximum total value in the knapsack.

Given two arrays:
* $values$: The value of each of the items.
* $weights$: The weight of each of the items.

An item cannot be picked multiple times.
For each item, either take it or leave it. (Cannot pick up a fraction of an item).

## Solution

Consider each of the items one by one. Start from item $n$, then item $n - 1$, $n-2$ ...

$$
knapsack(W,n) =
\begin{cases}
0,
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
min(W,n) = 0\\
knapsack(W,n-1),
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
W_{n} > W\\
max
\begin{cases}
knapsack(W, n-1)\\
knapsack(W - W_{n}, n-1) + V_{n}
\end{cases}
\;\text{Otherwise}
\end{cases}
$$

1. Create a 2D matrix of size $(W+1) \times (n+1)$.
2. Fill the matrix from upper left to lower right corner.
3. The final result is the value at lower right corner.

```python
def knapsack(W: int, values: List[int], weights: List[int]) -> int:
    # Get number of items $n$
    n = len(values)
    # Create 2D matrix to store subproblems (Dynamic Programming)
    dp = [[0 for _ in range(n + 1)] for _ in range(W + 1)]
    # Fill in table from upper left to lower right corner
    for w in range(W + 1):
        for i in range(n + 1):
            # Case $min(w, n) == 0$
            if min(w, i) == 0:
                dp[w][i] = 0
            elif w < weights[i - 1]:
                dp[w][i] = dp[w][i - 1]
            else:
                # Take item
                take = dp[w - weights[i - 1]][i - 1] + values[i - 1]
                # Leave item
                leave = dp[w][i - 1]
                # Select max of two options
                dp[w][i] = max(take, leave)

    # Return lower right corner
    return dp[-1][-1]
```

## Variations

Variation 1: In an unbound knapsack problem, an item can be picked up multiple times.

```python
def knapsack(W: int, values: List[int], weights: List[int]) -> int:
    # Get number of items $n$
    n = len(values)
    # Create 1D matrix to store subproblems (Dynamic Programming)
    dp = [0 for _ in range(W + 1)]
    # Find maximum value for each weight
    for w in range(W + 1):
        for i in range(n):
            # If weight of item can be fitted
            if weights[i] <= w:
                # Try adding item to knapsack
                take = dp[w - weights[i]] + values[i]
                dp[w] = max(dp[w], take)
    # Return result
    return dp[-1]
```
