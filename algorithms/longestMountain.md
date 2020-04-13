---
layout: post
title: Longest Mountain
subtitle: LeetCode
---

## Problem
Let's call any (contiguous) subarray B (of A) a mountain if the following properties hold:

* $B.length \geq 3$
* There exists some $0 < i < B.length - 1$ such that that $B[0] < B[i] < \dots < B[i - 1] < B[i] > B[i + 1] > \dots > B[B.length - 1]$

(Note that $B$ could be any subarray of $A$, including the entire array $A$.)

Given an array $A$ of integers, return the length of the longest mountain.

Return 0 if there is no mountain.

## Solution

Example: Given $A$ = [2, 1, 4, 7, 3, 2]

$$
\begin{align*}
&  &&  &&  &&X &&  && \\
&  &&  &&  &&X &&  && \\
&  &&  &&  &&X &&  && \\
&  &&  &&X &&X &&  && \\
&  &&  &&X &&X &&X && \\
&X &&  &&X &&X &&X &&X\\
&X &&X &&X &&X &&X &&X\\
\end{align*}
$$

By definition of a mountain, a mountain cannot begin at index 0. Therefore we start from index 1.

We used two variables $up$ and $down$ to keep track of the largest increment and decrement up to the current index. At each iteration:

1. Reset $up$ and $down$ to zero if reached end of a mountain.
2. Increment $up$ if current height is higher than previous.
3. Increment $down$ is current height is smaller than previous.
4. Calculate mountain as $up + down + 1$ and update maximum.

```python
def longestMountain(array: List[int]) -> int:
    # Keep track of increment up to current
    up = 0
    # Keep track of decrement up to current
    down = 0
    # Longest mountain
    longest = 0
    # Iterate index starting from 1
    for i in range(1, len(array)):
        # Current height
        current = array[i]
        # Previous height
        previous = array[i - 1]
        # Check if reached end of mountain
        #   1. A plateau
        #   2. New beginning of uphill
        if current == previous or (down > 0 and current > previous):
            # Start finding new mountain
            up = down = 0
        # If going uphll
        if current > previous:
            up += 1
        # If going downhill
        if current < previous:
            down += 1
        # A mountain is made of uphill and downhill
        if up > 0 and down > 0:
            # Compute length of mountain
            mountain = up + down + 1
            # Update longest mountain
            longest = max(longest, mountain)
    return longest
```
