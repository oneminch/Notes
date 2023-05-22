---
title: Valid Palindrome II
problemUrl: https://leetcode.com/problems/valid-palindrome-ii/
tags:
  - javascript
  - strings
  - dynamic programming
---

**My Solution**:

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */

// Checks if string passed 
// is a palindrome or not
const isPalindrome = function(s) {
  return s === s.split("").reverse().join("");
};

const validPalindrome = function(s) {
  let halfLen = Math.floor(s.length / 2);
  let first, last;
    
  for (var i = 0; i < halfLen; i++) {
    first = i;
    last = s.length - i - 1;
    if (s[first] !== s[last]) {
      return isPalindrome(s.substring(first, last)) || isPalindrome(s.substring(first + 1, last + 1));
    }
  }
  return isPalindrome(s);
};
```
