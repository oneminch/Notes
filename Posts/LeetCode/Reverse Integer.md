---
title: Reverse Integer
problemUrl: https://leetcode.com/problems/reverse-integer
tags:
  - javascript
  - math
---

## My Solution

### JavaScript

```javascript
/**
 * @param {number} x
 * @return {number}
 */

const reverse = (x) => {
  var n = Number(Math.abs(x).toString().split("").reverse().join(""));
  if (n > 0x7fffffff) return 0;
  else return x < 0 ? -n : n;
};
```
