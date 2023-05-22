---
title: Single Number
problemUrl: https://leetcode.com/problems/single-number/
tags:
  - python
---

**My Solution**:

```py
def singleNumber(nums: List[int]) -> int:
    stack = []

    for n in nums:
        if n in stack:
            i = stack.index(n)
            stack.pop(i)
        else:
            stack.append(n)
        
    return stack[0]
```
