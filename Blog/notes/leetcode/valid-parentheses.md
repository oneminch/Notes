---
title: Valid Parentheses
problemUrl: https://leetcode.com/problems/valid-parentheses
tags:
  - python
  - stack
---

**My Solution**:

```py
def isValid(s: str) -> bool:
    mappings = {
        "(": ")",
        "{": "}",
        "[": "]"
    }
    stack = []

    for parenthesis in list(s):
        if parenthesis in mappings:
            stack.append(parenthesis)
            continue
        
        if len(stack) > 0 and mappings[stack[-1]] == parenthesis:
            stack.pop()
        else:
            return False
            

    return False if (len(stack) > 0 or len(s) <= 1) else True

```
