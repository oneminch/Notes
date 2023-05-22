---
title: Valid Palindrome
problemUrl: https://leetcode.com/problems/valid-palindrome/
tags:
  - javascript
  - python
  - palindrome
---

**My Solution**:

## JavaScript

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function (s) {
	let stripped = s.toLowerCase().replace(/[^a-z0-9]/gi, "");

	let reversed = stripped.split("").reverse().join("");

	return stripped === reversed;
};
```

## Python

```py
def isPalindrome(s: str) -> bool:
    my_str = ''.join(c for c in s if c.isalnum()).lower()

    return my_str == my_str[::-1]
```
