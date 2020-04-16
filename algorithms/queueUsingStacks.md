---
layout: post
title: Implement Queue Using Stacks
subtitle: LeetCode
---

## Problem
Implement the following operations of a queue using stacks.

* push(x) -- Push element x to the back of queue.
* pop() -- Removes the element from in front of queue.
* peek() -- Get the front element.
* empty() -- Return whether the queue is empty.

## Solution

```python
class Queue:

    def __init__(self):
        # Initialize two stacks
        self.stack1 = []
        self.stack2 = []

    def push(self, x):
        # Push element to stack1
        self.stack1.append(x)

    def pop(self):
        # If stack2 is empty
        if not self.stack2:
            # Transfer data from stack1 to stack2
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        # Pop first element from stack 2
        return self.stack2.pop()

    def peek(self):
        # If stack2 is empty
        if not self.stack2:
            # Transfer data from stack1 to stack2
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        # Return top element of stack2
        return self.stack2[-1]

    def empty(self):
        # Check if stack1 and stack2 is empty
        return not self.stack1 and not self.stack2
```
