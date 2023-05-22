---
title: Move Zeroes
problemUrl: https://leetcode.com/problems/move-zeroes/
tags:
  - python
  - in-place
---

**My Solution**:

> Modified in-place

```py
def moveZeroes(nums: List[int]) -> None:
    zero_count = 0
    
    while 0 in nums:
        nums.pop(nums.index(0))
        zero_count+=1

    zeroes = [0]*zero_count
    nums += zeroes
```
