---
title: Single Number II
problemUrl: https://leetcode.com/problems/single-number-ii/
tags:
  - python
---

**My Solution**:

```py
def singleNumber(nums: List[int]) -> int:
    hashmap = {}
    for n in nums:
        if n in hashmap:
            hashmap[n]+=1
        else:
            hashmap[n] = 1

    return [k for k, v in hashmap.items() if v == 1][0]
```
