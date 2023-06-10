---
title: Reverse Integer
problemUrl: https://leetcode.com/problems/reverse-integer
tags:
  - javascript
  - math 
---

**My Solution**:

```javascript
/**
 * @param {number} x
 * @return {number}
 */

var reverse = function(x) {
    var n = Number((Math.abs(x)).toString().split('').reverse().join(''));
    if (n > 0x7FFFFFFF) return 0;
    else return (x<0) ? -n : n;
};
```
