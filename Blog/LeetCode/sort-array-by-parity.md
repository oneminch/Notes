---
title: Sort Array By Parity
problemUrl: https://leetcode.com/problems/sort-array-by-parity/
tags:
  - javascript
  - arrays
---

**My Solution**:

```javascript
/**
 * @param {number[]} A
 * @return {number[]}
 */
var sortArrayByParity = function(A) {
    let sorted_A = [];
    A.forEach(function (n) {
      if (n % 2 === 0) 
        sorted_A.unshift(n);    // if even, add to beginning of array
      else 
        sorted_A.push(n);       // if odd, add to end of array
    });

    return sorted_A;
};
```
