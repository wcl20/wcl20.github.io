---
layout: post
title: Coin Change 2
subtitle: LeetCode
---

## Problem
You are given coins of different denominations and a total amount of money. Write a function to compute the number of combinations that make up that amount. You may assume that you have infinite number of each kind of coin.

## Solution

1. Start with base case $amount = 0$, there is only 1 possible way to make the change.
2. Consider the list of coins one by one, when a new coin $c$ is considered, we update all the subproblems:

$$
change(amount) =
\begin{cases}
change(amount)
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
\text{if } amount < c\\
change(amount) + change(amount - c)
\;\;\;\text{Otherwise}\\
\end{cases}
$$

```python
def change(amount: int, coins: List[int]):
    # Create array to store subproblems (Dynamic Programming)
    dp = [0] * (amount + 1)
    # Base case when amount is 0, only one way to make change
    dp[0] = 1
    # Consider each coin
    for coin in coins:
        # Update all subproblems where $amount > coin$
        for i in range(coin, amount + 1):
            dp[i] = dp[i] + dp[i - coin]
    # Return last value
    return dp[-1]
```
