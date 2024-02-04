---
title: Remove Element
problemUrl: https://leetcode.com/problems/remove-element/
tags:
  - javascript
  - arrays
  - in-place
---

## My Solution

### JavaScript

```javascript
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */

const removeElement = (nums, val) => {
  while (nums.indexOf(val) >= 0) {
    nums.splice(nums.indexOf(val), 1);
  }
  return nums.length;
};
```
