---
title: Valid Parentheses
problemUrl: https://leetcode.com/problems/valid-parentheses
tags:
  - python
  - stack
---

## My Solution

### Python

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

### JavaScript

```javascript
function isValid(s: string): boolean {
  const mappings = {
    "(": ")",
    "[": "]",
    "{": "}"
  };
  const stack = [];

  if (s.length % 2 === 1) return false;

  for (let i = 0; i < s.length; i++) {
    if (s[i] in mappings) {
      stack.push(s[i]);
      continue;
    }

    if (stack.length > 0 && mappings[stack[stack.length - 1]] === s[i]) {
      stack.pop();
    } else {
      return false;
    }
  }
  return stack.length === 0;
}
```
