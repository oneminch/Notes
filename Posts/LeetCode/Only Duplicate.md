---
title: Detect the Only Duplicate in a List
problemUrl: https://binarysearch.com/problems/Detect-the-Only-Duplicate-in-a-List
tags:
  - python
  - two pointers
  - array
---

## My Solution

### Python

```py
def solve(nums):
    nums_sorted = sorted(nums)

    for i in range(len(nums)):
        if i > len(nums) - 2:
            break

        a = nums_sorted[i]
        b = nums_sorted[i+1]

        if a == b:
            return a
```
