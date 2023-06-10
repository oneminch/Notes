---
title: Binary Search
problemUrl: https://leetcode.com/problems/binary-search/
tags:
  - python
  - binary search
---

**My Solution**:

```py
def search(nums: List[int], target: int) -> int:
    index = 0
    nums_copy = nums[:]
    midpoint = len(nums_copy)//2
    
    while len(nums_copy) > 1 and target != nums_copy[midpoint]:
        if target > nums_copy[midpoint]:
            index += midpoint
            nums_copy[:] = nums_copy[midpoint:]
        else:
            nums_copy = nums_copy[:midpoint]
        
        midpoint = len(nums_copy)//2
        
        
    return index + midpoint if target == nums_copy[midpoint] else -1
```
