---
title: Length of Last Word
problemUrl: https://leetcode.com/problems/length-of-last-word/
tags:
  - javascript
  - strings
---

**My Solution**:

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
    return s.split(" ").filter(str => str.length > 0).pop().length;
};
```
