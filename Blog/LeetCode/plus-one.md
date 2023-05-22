---
title: Plus One
problemUrl: https://leetcode.com/problems/plus-one/
tags:
  - javascript
  - array
---

**My Solution**:

```js
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function (digits) {
	for (let i = digits.length - 1; i >= 0; i--) {
		if (digits[i] + 1 >= 10) {
			digits[i] = digits[i] + 1 - 10;
			if (i == 0) {
				digits.unshift(1);
			}
		} else {
			digits[i] += 1;
			break;
		}
	}

	return digits;
};
```
