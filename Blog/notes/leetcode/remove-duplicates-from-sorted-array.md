---
title: Remove Duplicates from Sorted Array
problemUrl: https://leetcode.com/problems/remove-duplicates-from-sorted-array/
tags:
  - javascript
  - arrays
---

**My Solution**:

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let i = 0;
    while (i < nums.length) {
        if (nums.indexOf(nums[i]) !== i) {
            nums.splice(i, 1);
        } else {
            i+=1;
        }
        
    };
    return nums.length;
};
```
