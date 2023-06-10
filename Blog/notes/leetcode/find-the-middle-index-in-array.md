---
title: Find the Middle Index in Array
problemUrl: https://leetcode.com/problems/find-the-middle-index-in-array/
tags:
  - python
  - lists
---

**My Solution**:

```py
def findMiddleIndex(nums: List[int]) -> int:
    for i in range(len(nums)):
        if sum(nums[:i]) == sum(nums[i+1:]):
            return i

    return -1
```
