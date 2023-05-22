---
title: Find Pivot Index
problemUrl: https://leetcode.com/problems/find-pivot-index/
alternateQuestion: https://leetcode.com/problems/find-the-middle-index-in-array/
tags:
  - python
  - prefix sum
---

**My Solution**:

```py
def pivotIndex(nums: List[int]) -> int:
    for i in range(len(nums)):
        if sum(nums[:i]) == sum(nums[i+1:]):
            return i

    return -1
```
