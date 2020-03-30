---
layout: post
title: Longest Palindromic Substring
subtitle: LeetCode
---

## Problem
Given a string $s$, find the longest palindromic substring in $s$.

## Solution
1. For each letter in the input string, start by expanding to the left and right to check for even and odd length palindromes.
2. For each palindrome found, update longest palindromic substring.

```python
def longestPalindrome(string: string) -> string:
    # Check string is not empty
    if string is None or len(string) < 1:
        return string
    # Store longest palindromic substring
    longest = string[0]
    # Iterate through each character in the string
    for i in range(len(string)):
        # Find palindrome substring of even length
        left, right = i, i + 1
        while left >= 0 and right < len(string):
            # If characters at both end are not the same ...
            if not string[left] == string[right]:
                # ... stop searching
                break
            # Otherwise, extend substring
            left -= 1
            right += 1
        # Found palindrome (even length)
        palindrome = string[left + 1 : right]
        # Update longest palindrome
        if len(palindrome) > len(longest):
            longest = palindrome
        # Find palindrome substring of odd length
        left, right = i - 1, i + 1
        while left >= 0 and right < len(string):
            # If characters at both end are not the same ...
            if not string[left] ==  string[right]:
                # ... stop searching
                break
            # Otherwise, extend substring
            left -= 1
            right += 1
        # Found palindrome (odd length)
        palindrome = string[left + 1 : right]
        # Update longest palindrome
        if len(palindrome) > len(longest):
            longest = palindrome
    return longest
```
