---
layout: post
title: Coin Change
subtitle: LeetCode
---

## Problem
You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

## Solution

The solution is to consider each coin one by one, and each time a new coin is considered we update the minimum coins to make the change.

The base case is no consider there is no coins.
* Number of coins to make amount 0 is 0
* Number of coins to make amount $>0$ is infinite (impossible)

Each time a new coin $c$ is considered, we update all subproblems

$$
minCoins(amount) =
\begin{cases}
minCoins(amount)
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
\text{if } amount < c\\
min
\begin{cases}
minCoins(amount),\\
1 + minCoins(amount - c)\\
\end{cases}
\;\;\;\text{Otherwise}\\
\end{cases}
$$

```python
def change(coins: List[int], amount: int):
    # Create array to store subproblems (Dynamic Programming)
    dp = [float("inf")] * (amount + 1)
    # Base case amount is 0, 0 coins to make change
    dp[0] = 0
    # Consider each coin 
    for coin in coins:
        # Update all subproblems where $amount > c$
        for i in range(coin, amount + 1):
            dp[i] = min(dp[i], 1 + dp[i - coin])
    # If last element is inf meaning impossible to make change
    return -1 if dp[-1] == float("inf") else dp[-1]
```
