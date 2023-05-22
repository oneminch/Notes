---
title: Running Sum of a 1D Array
problemUrl: https://leetcode.com/problems/running-sum-of-1d-array/
tags:
  - python
  - prefix sum
---

**My Solution**:

```py
def runningSum(nums: List[int]) -> List[int]:
    lst = [None]*len(nums)
    
    for i in range(len(nums)):
        lst[i] = sum(nums[0:i+1])

    return lst
```
