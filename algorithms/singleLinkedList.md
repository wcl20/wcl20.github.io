---
layout: post
title: Single Linked List
---

## Problem
A linked list is a sequence of data elements, which are connected together via links. Each node contains a value and a link to the next node in form of a pointer. In a Single Linked List, there is only one link between any two data elements.

Implement Single Linked List Class.

## Solution

```python
class Node:
    def __init__(self, value):
        # Value stored in node
        self.value = value
        # Next value in list
        self.next = None

class LinkedList:
    def __init__(self):
        # Store pointer to head
        self.head = None

    def add(self, value):
        """ Adds value to end of list """
        # Create node for new value
        node = Node(value)
        # If list is empty ...
        if self.head is None:
            # ... Insert at head
            self.head = node
        # Otherwise,
        else:
            # Find last element in list
            current = self.head
            while current.next:
                current = current.next
            # Append new node to list
            current.next = node

    def insert(self, value, index):
        """ Inserts value at specified index """
        # Create node for new value
        node = Node(value)
        # Insert at head
        if index == 0:
            node.next = self.head
            self.head = node
        else:
            # Find node at position index
            prev, current = None, self.head
            for _ in range(index):
                prev, current = current, current.next
                # If reached end of list
                if not current:
                    break
            # Insert node
            node.next = current
            prev.next = node

    def remove(self, value):
        """ Remove first occurrence of value from list """

        # Check list is not empty
        if not self.head:
            return
        # Remove head
        if self.head.value == value:
            self.head = self.head.next
        else:
            # Search for element with value
            prev, current = None, self.head
            while current:
                if current.value == value:
                    break
                prev, current = current, current.next
            # Remove element
            prev.next = current.next

```
