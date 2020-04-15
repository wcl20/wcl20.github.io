---
layout: post
title: Implement Trie (Prefix Tree)
subtitle: LeetCode
---

## Problem
Implement a trie with insert, search, and startsWith methods.

## Solution

```python
# A Trie Node
class Node:
    def __init__(self):
        # Children of the node
        self.children = {}
        # A flag to indicate end of word
        self.end = False

class Trie:
    def __init__(self):
        # Initialise root node
        self.root = Node()

    def insert(self, word: str):
        # Start from root node
        current = self.root
        # Iterate each letter of the word
        for char in word:
            # If current letter does not have a node
            if not char in current.children:
                # Create a node for current letter
                current.children[char] = Node()
            # Move the next node
            current = current.children[char]
        # Mark the end of a word
        current.end = True

    def search(self, word: str) -> bool:
        # Start from root node
        current = self.root
        # Iterate each letter of the word
        for char in word:
            # If current letter does not have a node
            if not char in current.children:
                # Word is not in Trie
                return False
            # Move the next node
            current = current.children[char]
        # Return true if end of word else false
        return current.end

    def startsWith(self, prefix: str) -> bool:
        # Start from root node
        current = self.root
        # Iterate each letter of the word
        for char in prefix:
            # If current letter does not have a node
            if not char in current.children:
                # Word is not in Trie
                return False
            # Move the next node
            current = current.children[char]
        # Every letter in prefix is in trie
        return True
```
