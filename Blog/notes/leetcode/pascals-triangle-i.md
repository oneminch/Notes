---
title: Pascal's Triangle I
problemUrl: https://leetcode.com/problems/pascals-triangle
tags:
  - python
  - arrays
---

**My Solution**:

```py
def generate(numRows: int) -> List[List[int]]:
    pascals_triangle = [[1]]

    if numRows > 1:
        pascals_triangle.append([1,1])

    for i in range(2, numRows):
        l = []
        l.append(1)
        prev_triangle = pascals_triangle[i-1]
        
        for j in range(len(prev_triangle) - 1):
            l.append(prev_triangle[j] + prev_triangle[j+1])
        
        l.append(1)
        pascals_triangle.append(l)

    return pascals_triangle
```
