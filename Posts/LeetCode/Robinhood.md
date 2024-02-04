---
title: Robinhood
problemUrl: https://binarysearch.com/problems/Robinhood
tags:
  - python
---

## My Solution

### Python

```py
from __future__ import division

def solve(n, e, o, t):
    year = 0
    target = n

    if n > t:
        return year

    while min(target, t) != t:
        if year % 2 == 0:
            target += target*e/100
        else:
            target += target*o/100

        year += 1

    return year
```
