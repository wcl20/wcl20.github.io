---
layout: post
title: Implement Stack Using Queues
subtitle: LeetCode
---

## Problem
Implement the following operations of a stack using queues.

* push(x) Push element x onto stack.
* pop() - Removes the element on top of the stack.
* top() -- Get the top element.
* empty() -- Return whether the stack is empty.

## Solution

```python
class Stack:

    def __init__(self):
        # Initialize two queues
        self.queue1 = []
        self.queue2 = []

    def push(self, x):
        # Add data to queue 2
        self.queue2.append(x)
        # Transfer data from queue1 to queue2
        while self.queue1:
            self.queue2.append(self.queue1.pop(0))
        # Transfoer data from queue2 to queue1
        while self.queue2:
            self.queue1.append(self.queue2.pop(0))

    def pop(self):
        # Get first of queue1
        return self.queue1.pop(0)

    def top(self):
        # Get first element of queue1
        return self.queue1[0]

    def empty(self):
        # Check if queue1 is empty
        return len(self.queue1) == 0

```
