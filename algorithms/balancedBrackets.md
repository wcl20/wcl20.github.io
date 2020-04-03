---
layout: post
title: Balanced Brackets
subtitle: Hackerrank
---

## Problem
A bracket is considered to be any one of the following characters: (, ), {, }, [, or ].

Two brackets are considered to be a matched pair if the an opening bracket (i.e., (, [, or {) occurs to the left of a closing bracket (i.e., ), ], or }) of the exact same type.

Determine whether each sequence of brackets is balanced.

## Solution

```python
def isBalanced(string: string) -> bool:
    # Create a stack
    stack = []
    # Iterate string of brackets
    for bracket in string:
        # If opening bracket ...
        if bracket in ["(", "[",  "{"]:
            # ... Add to stack
            stack.append(bracket)
        # Otherwise if closing bracket ...
        else:
            # If no opening brackets
            if not stack:
                return False
            # Get last opening bracket
            last = stack.pop()
            # Check that last opening matches closed
            if last == "(" and bracket in ["]", "}"]:
                return False
            if last == "[" and bracket in [")", "}"]:
                return False
            if last == "{" and bracket in [")", "]"]:
                return False
    # Stack should be empty if brackets are balanced
    return not stack
```
