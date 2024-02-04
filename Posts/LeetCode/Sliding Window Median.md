---
title: Sliding Window Median
problemUrl: https://leetcode.com/problems/sliding-window-median/
tags:
  - python
  - sliding window
  - arrays
---

## My Solution

### Python

```py
def medianSlidingWindow(nums: List[int], k: int) -> List[float]:
    sublist = []
    midpoint = 0
    medians = []

    for i in range(0, len(nums)-k+1):
        sublist = sorted(nums[i : i+k])

        midpoint = math.floor(len(sublist) / 2)

        medians.append(sublist[midpoint] if len(sublist) % 2 else (sublist[midpoint] + sublist[midpoint-1]) / 2)


    return medians
```
