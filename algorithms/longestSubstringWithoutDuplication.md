---
layout: post
title: Longest Substring Without Repeating Characters
subtitle: LeetCode
---

## Problem
Given a string, find the length of the longest substring without repeating characters.

## Solution

The solution uses a sliding window approach and a lookup table that maps visited characters to its last occurrence position.

The sliding window approach uses two pointers $start$ and $end$ to mark the start and end position of the substring. In each iteration, we increment the end pointer to include the next character.

1. If the next character has not been visited, continue.
2. If the next character has been visited, update $start$ pointer up to the index that removes the duplicated character.

Example: Given string "abbcabcbb"

Iteration 1: $start = 0$, $end = 0$, substring = "a"

Iteration 2: $start = 0$, $end = 1$, substring = "ab"

Iteration 3: $start = 2$, $end = 2$, substring = "b"

Iteration 4: $start = 2$, $end = 3$, substring = "bc"

Iteration 5: $start = 2$, $end = 4$, substring = "bca"

Iteration 6: $start = 3$, $end = 5$, substring = "cab"

Iteration 7: $start = 4$, $end = 6$, substring = "abc"

Iteration 8: $start = 6$, $end = 7$, substring = "cb"

Iteration 9: $start = 8$, $end = 8$, substring = "b"


In each iteration, we update the length of maximum substring. Notice $start$ is only updated (moved forward) if the current substring includes a duplicated character. In iteration 5, although 'a' was previously visited, the current starting (position 2) does not include the previously visited 'a' (position 0)


```python
def lengthOfLongestSubstring(string: str) -> int:
    # Lookup table to store visited character and its last occurrence
    visited = {}
    # Keep track of length of maximum substring
    maximum = 0
    # $start$ pointer
    start = 0
    # Slide $end$ pointer along string
    for end, char in enumerate(string):
        # If character was visited
        if char in visited:
            # Update $start$ pointer
            start = max(start, visited[char] + 1)
        # Update maximum length
        maximum = max(maximum, end - start + 1)
        # Add character to visited table
        visited[char] = end
    return maximum
```

## Variations

Variation 1: Longest substring without repeating characters
```python
def lengthOfLongestSubstring(string: str) -> str:
    # Lookup table to store visited character and its last occurrence
    visited = {}
    # Keep track of length of maximum substring
    substring = ""
    # $start$ pointer
    start = 0
    # Slide $end$ pointer along string
    for end, char in enumerate(string):
        # If character was visited
        if char in visited:
            # Update $start$ pointer
            start = max(start, visited[char] + 1)
        # Update maximum length
        if len(substring) < end - start + 1:
            substring = string[start:end + 1]
        # Add character to visited table
        visited[char] = end
    return substring
```
