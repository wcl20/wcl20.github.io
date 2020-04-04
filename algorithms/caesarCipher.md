---
layout: post
title: Caesar Cipher
subtitle: Hackerrank
---

## Problem
Caesar's cipher shifts each letter by a number of letters. If the shift takes you past the end of the alphabet, just rotate back to the front of the alphabet.

Original Alphabets: abcdefghijklmnopqrstuvwxyz
Caesar Cipher Encryption ($k$ = 3): defghijklmnopqrstuvwxyzabc

The cipher only encrypts letters is case sensitive.

## Solution

```python
def caesarCipher(string: string, k: int):
    # Convert string to list of characters
    string = list(string)
    # Iterate string
    for i, char in enumerate(string):
        # Check character is a letter
        if char.isalpha():
            # Check case of character
            a = 'A' if char.isupper() else 'a'
            # Apply rotation
            unicode = ord(a) + (ord(char) - ord(a) + k) % 26
            # Modify character
            string[i] = chr(unicode)
    return "".join(string)
```
