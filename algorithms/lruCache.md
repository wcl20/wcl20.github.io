---
layout: post
title: LRU Cache
subtitle: LeetCode
---

## Problem
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

* get(value) -- Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
* put(key, value) --  Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

## Solution

```python
class LRUCache:

    def __init__(self, capacity: int):
        # Set maximum capacity
        self.capacity = capacity
        # Use a Linked List to maintain eviction order
        self.values = LinkedList()
        # Use hashmap to lookup cached keys
        self.map = {}

    def get(self, key: int) -> int:
        # If key is not in cache ...
        if key not in self.map:
            return -1
        # Otherwise, value is in cache
        node = self.map[key]
        # Move value to end to evict last
        self.values.remove(node)
        self.values.add(node)
        # Return value
        return node.value

    def put(self, key: int, value: int) -> None:
        # If key is already in cache
        if key in self.map:
            node = self.map[key]
            # Change cached value
            node.value = value
            # Move value to end to evict last
            self.values.remove(node)
            self.values.add(node)
        # Otherwise, key is not in cache
        else:
            # Create node for value
            node = Node(key, value)
            # If cache reached full capacity
            if self.values.size() == self.capacity:
                # Get head of list
                head = self.values.head
                # Remove head from list
                self.values.remove(head)
                # Remove head from cache
                self.map.pop(head.key)
            # Put node in list
            self.values.add(node)
            # Put node in cache
            self.map[key] = node        
```

Linked List
```python
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def add(self, node):
        """ Adds value to end of list """
        if self.head is None:
            self.head = node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = node

    def remove(self, node):
        """ Remove a node from list """
        if not self.head:
            return
        if self.head == node:
            self.head = self.head.next
        else:
            prev, current = None, self.head
            while current:
                if current is node:
                    break
                prev, current = current, current.next
            prev.next = current.next
        node.next = None

    def size(self):
        """ Return size of linked list """
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count
```
