---
layout: post
title: Palindrome Check
subtitle: Hackerrank
---

## Problem
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

## Solution

```python
def isPalindrome(string: string) -> bool:
    # Remove non alphanumeric characters
    string = "".join(filter(str.isalnum, string))
    # Convert all characters to lower case
    string = string.lower()
    # Iterate string ...
    for i in range(len(string) // 2):
        # If first and last characters are different ...
        if not string[i] == string[-i-1]:
            # ... this string is not a palindrome
            return False
    return True
```
