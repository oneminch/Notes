---
title: Contains Duplicate
problemUrl: https://leetcode.com/problems/contains-duplicate
tags:
  - python
  - hash table
---

**My Solution**:

```py
def containsDuplicate(self, nums: List[int]) -> bool:
    hash_table = {}

    for num in nums:

        if num in hash_table:
            return True
        else:
            hash_table[num] = num

    return False
```
