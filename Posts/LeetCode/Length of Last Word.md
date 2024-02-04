---
title: Length of Last Word
problemUrl: https://leetcode.com/problems/length-of-last-word/
tags:
  - javascript
  - strings
---

## My Solution

### JavaScript

```javascript
/**
 * @param {string} s
 * @return {number}
 */

const lengthOfLastWord = (s) => {
  return s
    .split(" ")
    .filter((str) => str.length > 0)
    .pop().length;
};
```
