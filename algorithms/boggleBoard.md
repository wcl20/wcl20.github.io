---
layout: post
title: Word Search II
subtitle: LeetCode
---

## Problem
Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

## Solution

Method 1: Depth First Search

Perform a depth first search starting from each cell until a word is found.
```python
def findWords(board: List[List[str]], words: List[str]) -> List[str]:
    # Get number of rows
    n = len(board)
    # Get number of columns
    m = len(board[0])
    # Create visited map
    visited = [[False] * m for _ in range(n)]
    # Create set to store results
    result = set({})
    # Search starting from each letter
    for i in range(n):
        for j in range(m):
            dfs(board, words, visited, i, j, "", result)
    return result

def dfs(board, words, visited: List[List[bool]], i: int, j: int, word: str, result: Set):
    # Check index
    if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]):
        return
    # Check cell is visited
    if visited[i][j]:
        return
    # Visit current cell
    visited[i][j] = True
    word = word + board[i][j]
    # Check word in dictionary
    if word in words:
        result.add(word)
    # Visit neighbours
    dfs(board, words, visited, i + 1, j, word, result)
    dfs(board, words, visited, i - 1, j, word, result)
    dfs(board, words, visited, i, j + 1, word, result)
    dfs(board, words, visited, i, j - 1, word, result)
    # Backtrack
    visited[i][j] = False
    word = word[:-1]
```

Method 2: Depth First Search and Trie

The above solution can be optimize using a Prefix Trie, if the current word is not a prefix of any word in the dictionary, we can stop the search immediately.
```python
def findWords(board: List[List[str]], words: List[str]) -> List[str]:
    # Get number of rows
    n = len(board)
    # Get number of columns
    m = len(board[0])
    # Create visited map
    visited = [[False] * m for _ in range(n)]
    # Create set to store results
    result = set({})
    # # Create Trie from words
    trie = Trie()
    for word in words:
        trie.insert(word)
    # Search starting from each letter
    for i in range(n):
        for j in range(m):
            dfs(board, trie, visited, i, j, "", result)
    return result

def dfs(board, trie, visited: List[List[bool]], i: int, j: int, word: str, result: Set):
    # Check index
    if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]):
        return
    # Check words beginning with prefix
    if not trie.startsWith(word):
        return
    # Check cell is visited
    if visited[i][j]:
        return
    # Visit current cell
    visited[i][j] = True
    word = word + board[i][j]
    # Check word in trie
    if trie.search(word):
        result.add(word)
    # Visit neighbours
    dfs(board, trie, visited, i + 1, j, word, result)
    dfs(board, trie, visited, i - 1, j, word, result)
    dfs(board, trie, visited, i, j + 1, word, result)
    dfs(board, trie, visited, i, j - 1, word, result)
    # Backtrack
    visited[i][j] = False
    word = word[:-1]
```

A Trie
```python
# A Trie Node
class Node:
    def __init__(self):
        self.children = {}
        self.end = False

class Trie:
    def __init__(self):
        self.root = Node()

    def insert(self, word: str):
        current = self.root
        for char in word:
            if not char in current.children:
                current.children[char] = Node()
            current = current.children[char]
        current.end = True

    def search(self, word: str) -> bool:
        current = self.root
        for char in word:
            if not char in current.children:
                return False
            current = current.children[char]
        return current.end

    def startsWith(self, prefix: str) -> bool:
        current = self.root
        for char in prefix:
            if not char in current.children:
                return False
            current = current.children[char]
        return True
```
