---
layout: post
title: Group Anagrams
subtitle: LeetCode
---

## Problem
Given an array of strings, group anagrams together.

Example: ["eat", "tea", "tan", "ate", "nat", "bat"] should output [["ate","eat","tea"], ["nat","tan"], ["bat"]]

## Solution

Use a dictionary that maps a string to a list of string. Strings that are anagrams should map to the same list. To do this, we can simply use the sorted string as key.

```python
def groupAnagrams(strings: List[str]) -> List[List[str]]:
    # Create a dictionary that maps string to lists
    dictionary = {}
    # Iterate each string
    for string in strings:
        # Sort the string as key
        key = "".join(sorted(string))
        # Get list of anagrams with same key and append string
        dictionary.setdefault(key, []).append(string)
    # Return lists of lists
    return list(dictionary.values())
```
