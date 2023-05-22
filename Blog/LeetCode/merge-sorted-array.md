---
title: Merge Sorted Array
problemUrl: https://leetcode.com/problems/merge-sorted-array/
tags:
  - javascript
  - array
  - sorting
  - two pointers
---

**My Solution**:

```js
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function (nums1, m, nums2, n) {
	nums1.splice(m, nums1.length - m, ...nums2);
	nums1.sort((a, b) => a - b);
};
```
