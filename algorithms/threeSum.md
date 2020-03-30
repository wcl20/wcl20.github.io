---
layout: post
title: Three Sum
subtitle: LeetCode
---

## Problem
Given an array $nums$ of $n$ integers, are there elements $a$, $b$, $c$ in $nums$ such that $a + b + c = 0$. Find all unique triplets in the array which gives the sum of zero.

The solution set must not contain duplicate triplets.

Example:
* $nums = [-1, 0, 1, 2, -1, -4]$. Solution set: [[-1, 0, 1], [-1, -1, 2]]
* $nums = [0, 0, 0, 0]$. Solution set: [[0, 0, 0]]
* $nums = [-2, 0, 0, 2, 2]$. Solution set: [[-2, 0, 2]]

## Solution
1. Sort the array
2. Iterate through each element treating it as $a$
3. Find $b$ and $c$ in the remaining array such that $b + c = -a$

Method 1: Find $b$ and $c$ using hash table.
```python
def threeSum(nums: List[int]) -> List[List[int]]:
      results = []
      # Sort the array of integers
      nums = sorted(nums)
      # Iterate array, treating each value as $a$
      for i, a in enumerate(nums):
          # Skip visited values to avoid duplicate solutions
          if i > 0 and a == nums[i - 1]:
              continue
          # Find $b$ and $c$ such that $b + c = -a$
          target = -a
          # Store visited elements
          visited = set()
          # Store added solution to avoid duplicate solutions
          added = set()
          # Iterate the rest of the array ...
          for b in nums[i + 1:]:
              # Skip added values to avoid duplicate solutions
              if b in added:
                  continue
              # If target - $b$ is in hash table ...
              if target - b in visited:
                  # ... add solution to solution set ...
                  results.append([a, b, target - b])
                  # ... add $b$ to added solution ...
                  added.add(b)
                  # ... add target - $b$ to added solution
                  added.add(target - b)
              # Mark $b$ as visited
              visited.add(b)
      return results
```

Method 2: Find $b$ and $c$ using sliding window and two pointers.
```python
def threeSum(nums: List[int]) -> List[List[int]]:
      results = []
      # Sort the array of integers
      nums = sorted(nums)
      # Iterate array, treating each value as $a$
      for i, a in enumerate(nums):
          # Skip visited values to avoid duplicate solutions
          if i > 0 and a == nums[i - 1]:
              continue
          # Find $b$ and $c$ such that $b + c = -a$
          target = -a
          # Create two pointers: left ($b$) and right ($c$)
          b_ptr, c_ptr = i + 1, len(nums) - 1
          # Iterate the rest of the array ...
          while b_ptr < c_ptr:
              # Skip visited values to avoid duplicate solutions
              if c_ptr < len(nums) - 1 and nums[c_ptr] == nums[c_ptr + 1]:
                  c_ptr -= 1
              # If $b + c = -a$ ...
              elif nums[b_ptr] + nums[c_ptr] == target:
                  # ... add solution to solution set
                  results.append([a, nums[b_ptr], nums[c_ptr]])
                  b_ptr += 1
                  c_ptr -= 1
              # If $b + c < -a$ ...
              elif nums[b_ptr] + nums[c_ptr] < target:
                  # ... Increment left pointer to increase $b$
                  b_ptr += 1
              # Otherwise, $b + c > -a$ ...
              else:
                  # ... Decrement right pointer to decrease $c$
                  c_ptr -= 1
      return results
```
