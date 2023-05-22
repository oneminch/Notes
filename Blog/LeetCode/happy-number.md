---
title: Happy Number
problemUrl: https://leetcode.com/problems/happy-number/
tags:
  - python
---

**My Solution**:

```py
def isHappy(n: int) -> bool:
    digits = [int(digit) for digit in list(str(n))]

    digit_sums = []

    while 1 not in digit_sums:
        digit_sum = 0
        for d in digits:
            digit_sum += d**2

        if digit_sum not in digit_sums:
            digit_sums.append(digit_sum)
            digits = [int(digit) for digit in list(str(digit_sum))]
        else: 
            return False

    return True
```
