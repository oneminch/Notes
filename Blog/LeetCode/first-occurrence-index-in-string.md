---
title: Find the Index of the First Occurrence in a String
problemUrl: https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/
tags:
  - javascript
  - strings
---

**My Solution**:

```javascript
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
    if (needle.length === 0) {
        return 0;
    }

    return haystack.indexOf(needle);
};
```
