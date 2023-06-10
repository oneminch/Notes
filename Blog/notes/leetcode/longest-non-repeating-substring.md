---
title: Longest Substring Without Repeating Characters
problemUrl: https://leetcode.com/problems/longest-substring-without-repeating-characters/
tags:
  - javascript
  - strings
  - hash tables
---

**My Solution**:

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    if (s.length < 1) return 0;
    
    let arr = [], index = -1, countArr = [];
    
    for (let i = 0; i < s.length; i++) {
        index = arr.indexOf(s[i]);
        if (index >= 0) {
            arr.splice(0, (index+1));
        }
        arr.push(s[i]);
        countArr.push(arr.length);
    }
    
    return Math.max(...countArr);
};
```
