---
title: Roman to Integer
problemUrl: https://leetcode.com/problems/roman-to-integer/
tags:
  - python
  - math
  - numbers
---

**My Solution**:

```py
def romanToInt(s: str) -> int:
		basis = {
				"I": 1,
				"V": 5,
				"X": 10,
				"L": 50,
				"C": 100,
				"D": 500,
				"M": 1000,
		}

		nums = list(s)
		value = i = 0

		while i < len(nums):
				if i == len(nums) - 1 or basis[nums[i]] >= basis[nums[i+1]]:
						value += basis[nums[i]]
						i+=1
				else:
						value += (basis[nums[i+1]] - basis[nums[i]])
						i+=2

		return value
```
