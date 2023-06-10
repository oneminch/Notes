---
title: Remove Element
problemUrl: https://leetcode.com/problems/remove-element/
tags:
  - javascript
  - arrays
  - in-place
---

**My Solution**:

```javascript
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    while (nums.indexOf(val) >= 0) {
        nums.splice(nums.indexOf(val), 1);
    }
    return nums.length;
};
```
