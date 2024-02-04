---
title: Palindrome Number
problemUrl: https://leetcode.com/problems/palindrome-number/
tags:
  - python
  - palindrome
---

## My Solution

### Python

```py
def isPalindrome(x: int) -> bool:
    num_str = str(x)
    if x < 0 or num_str != num_str[::-1]:
        return False
    else:
        return True
```
