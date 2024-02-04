---
title: Reverse String
problemUrl: https://leetcode.com/problems/reverse-string/
tags:
  - python
---

## My Solution

### Python

**Modified In-Place.**

```py
def reverseString(s: List[str]) -> None:
    for i in range(len(s)//2):
        s[i], s[-(i+1)] = s[-(i+1)], s[i]
```
