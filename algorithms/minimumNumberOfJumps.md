---
layout: post
title: Jump Game II
subtitle: LeetCode
---

## Problem
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

## Solution
Think of each number $n$ as a ladder starting at that position, where $n$ is the number of steps (Spaces between $X$) of the ladder. The greedy algorithm climbs the current ladder until it reaches the end before it switches to a new ladder (if there is one available).

For example: Given array [2, 3, 1, 1, 4].

The ladders will look like this

$$
\begin{align*}
&XXX\\
&\;\;\;XXXX\\
&\;\;\;\;\;\;XX\\
&\;\;\;\;\;\;\;\;\;XX\\
\end{align*}
$$

In the example above, the greedy algorithm climbs the first ladder $XXX$ until it reaches the end, where it switches to next ladder $XXXX$. Notice when climbing the second ladder, there is an option to switch to another ladder $XX$. But the greedy algorithms sticks to the same ladder because it wants to minimize the number of jumps.

Keep track of:
1. The number ladders used $jumps$
2. Remaining steps of the current ladder $steps$
3. The maximum reachable distance $furthest$

We start with the first ladder, decrement $steps$ each time we take a step. And save the next ladder that brings us to the furthest reachable distance.

We only switch to the next ladder when we finished climbing the current ladder. In this case we update $steps$ to $furthest$ minus the current position.

We start with $furthest = 2$, $steps = 2$, $jumps = 1$.

$i = 1$: 3. $furthest = 1 + 3 = 4$, $steps = 1$, $jumps = 1$.

$i = 2$: 1. $furthest = 4$, $steps = 4 - i = 2$, $jumps = 2$.

$i = 3$: 1. $furthest = 4$, $steps = 1$, $jumps = 2$.

$i = 4$: 4. Return $jumps = 2$.

```python
def jump(array: List[int]):
    # If array has 0 or 1 element
    if len(array) < 2:
        # Takes 0 jumps to reach end
        return 0;
    # Remaining steps of current ladder
    steps = array[0]
    # Furthest Reachable distance is length of current ladder
    furthest = array[0]
    # Number of jumps (ladders used)
    jumps = 1
    # Iterate array
    for i in range(1, len(array)):
        # If we reached the end
        if i == len(array) - 1:
            # Return number of jumps
            return jumps
        # Update ladder to furthest distance
        furthest = max(furthest, i + array[i])
        # Take a step on the ladder
        steps -= 1
        # If reached the end of current ladder ...
        if steps == 0:
            # Switch to ladder that goes furthest
            steps = furthest - i
            # Update number of jumps (ladders used)
            jumps += 1
    return jumps
```
