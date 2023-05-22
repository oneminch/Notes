---
title: Pascal's Triangle II
problemUrl: https://leetcode.com/problems/pascals-triangle-ii
tags:
  - python
  - arrays
---

**My Solution**:

```py
def getRow(rowIndex: int) -> List[int]:
    pascals_triangle = [[1], [1,1]]

    if rowIndex < 2:
        return pascals_triangle[rowIndex]

    for i in range(2, rowIndex + 1):
        l = []
        l.append(1)
        prev_triangle = pascals_triangle[i-1]
        
        for j in range(len(prev_triangle) - 1):
            l.append(prev_triangle[j] + prev_triangle[j+1])
        
        l.append(1)
        pascals_triangle.append(l)

    return pascals_triangle[-1]
```
