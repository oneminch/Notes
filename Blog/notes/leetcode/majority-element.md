---
title: Majority Element
problemUrl: https://leetcode.com/problems/majority-element/
tags:
  - python
  - hash tables
  - sorting
---

**My Solution**:

```py
def majorityElement(nums: List[int]) -> int:
    sorted_nums = sorted(nums)
    uniques = {}

    for i in sorted_nums:
        if i not in uniques:
            uniques[i] = 1
        else:
            uniques[i] += 1

    uniques_keys = list(uniques.keys())
    uniques_vals = list(uniques.values())

    return uniques_keys[uniques_vals.index(max(uniques_vals))]
```
