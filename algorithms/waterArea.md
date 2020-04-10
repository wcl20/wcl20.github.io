---
layout: post
title: Trapping Rain Water
subtitle: LeetCode
---

## Problem
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

Example: Given [3, 0, 0, 2, 0, 4] has the structure

$$
\begin{align*}
&  && && && && &&X\\
&X && && &&  && &&X\\
&X && && &&X && &&X\\
&X &&\_ &&\_ &&X &&\_ &&X
\end{align*}
$$

The area that can trap rain water an marked with $O$

$$
\begin{align*}
&  && && && && &&X\\
&X &&O &&O &&O &&O &&X\\
&X &&O &&O &&X &&O &&X\\
&X &&O &&O &&X &&O &&X
\end{align*}
$$

Therefore this structure can trap 10 units of water.

## Solution

An element of the array can store water if there are higher bars on left and right. The idea is to compute the amount of water that can be stored in every element of array.

At each index $i$, we want to find highest bar to its left, $left[i]$, and the highest bar to its right, $right[i]$. The amount of water that can be trapped at index $i$ is:

$$
min(left[i], right[i]) - height[i]
$$

We can use Dynamic Programming to keep track of the highest bar left and right of $i$ (including itself).

```python
def trap(heights: List[int]) -> int:
    # Check heights in not empty
    if not heights:
        return 0
    # Store highest bar to the left of $i$ (Dynamic Programming)
    left = [0] * len(heights)
    # Store highest bar to the right of $i$ (Dynamic Programming)
    right = [0] * len(heights)
    # Compute left[i] for each position
    left[0] = heights[0]
    for i in range(1, len(heights)):
        left[i] = max(left[i - 1], heights[i])
    # Compute right[i] for each position
    right[-1] = heights[-1]
    for i in range(1, len(heights)):
        right[-1-i] = max(right[-i], heights[-1-i])
    # Accumulate total water trapped in each position
    trapped = 0
    for i, height in enumerate(heights):
        trapped += min(left[i], right[i]) - height
    return trapped
```
