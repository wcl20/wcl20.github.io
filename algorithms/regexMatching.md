---
layout: post
title: Regular Expression Matching
subtitle: LeetCode
---

## Problem
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '\*'.

* '.' Matches any single character.
* '\*' Matches zero or more of the preceding element.

s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like . or \*.

## Solution

### Base cases:

1. $s$ is empty and $p$ is empty, returns True.
2. $s$ is not empty and $p$ is empty, returns False.
3. $s$ is empty and $p$ is not empty. (Check after handling \* Case) For example: $s$ = "". $p$ = "a*"

### Handling \* Case:

Iteratively compare remaining $s$ with remaining pattern. For example: $s$ = "bbbc". $p$ = "b*c".

Compare "bbbc" with "c",

Compare "bbc" with "c",

Compare "bc" with "c",

Compare "c" with "c"

Compare "" with "c"

In each iteration, if the remaining string is not the same as the remaining pattern. Then the first character of the remaining string must match the preceding character of \*.

### Handling . Case:

Move one character in both $s$ and $p$ and continue checking.

### Handling character Case:

If Characters are the same, move one character in both $s$ and $p$ and continue checking. Otherwise return False.




```python
def isMatch(string: str, pattern: str) -> bool:
    # Base Cases
    if not string and not pattern:
        return True
    if string and not pattern:
        return False
    # Handling * Case
    if len(pattern) > 1 and pattern[1] == "*":
        # Iterate remaining string
        for i in range(len(string) + 1):
            # Check remaining string with remaining pattern
            if isMatch(string[i:], pattern[2:]):
                return True
            # Remaining string is empty and does not match with remaining pattern
            if not string[i:]:
                return False
            # First character of string does not match preceding character
            if not pattern[0] == "." and not string[i] == pattern[0]:
                return False
    # Remaining base case after handling * case
    if not string and pattern:
        return False
    # Handling . Case
    if pattern[0] == ".":
        # Check remaining string and pattern
        return isMatch(string[1:], pattern[1:])
    # Handling character Case
    if pattern[0] == string[0]:
        # Check remaining string and pattern
        return isMatch(string[1:], pattern[1:])
    else:
        # Character mismatch
        return False
```
