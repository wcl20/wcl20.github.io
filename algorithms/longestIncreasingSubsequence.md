---
layout: post
title: Longest Increasing Subsequence
subtitle: LeetCode
---

## Problem
Given an unsorted array of integers, find the length of longest increasing subsequence.

## Solution


$$
lis(i) =
\begin{cases}
1
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
\text{if } i = 0\\
1 + max(lis(j)),
\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;
\forall j. [j < i \text{ and } array[j] < array[i]]\\
\end{cases}
$$

Where
* $lst(i)$ is the Longest increasing subsequence ending at index $i$.

If there is no such $j$ where $0 < j < i$ and $array[j] < array[i]$ then $max(lst(j))$ is 0.

```python
def lengthOfLIS(array: List[int]) -> int:
    # Check array is not empty
    if len(array) < 1:
        return 0
    # Create array to store subproblems (Dynamic Programming)
    dp = [1] * len(array)
    # Iterate array
    for i in range(1, len(array)):
        # Find all $j < i$ ...
        for j in range(i):
            # ... and $arr[j] < arr[i]$
            if array[j] < array[i]:
                # Find 1 + max(lst[j])
                dp[i] = max(dp[i], 1 + dp[j])
    # Return longest increasing subsequence ending at all index
    return max(dp)
```
