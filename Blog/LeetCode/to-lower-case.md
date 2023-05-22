---
title: To Lower Case
problemUrl: https://leetcode.com/problems/to-lower-case/
tags:
  - javascript
  - strings
---

**My Solution**:

```javascript
/**
 * @param {string} str
 * @return {string}
 */
var toLowerCase = function(str) {
    let char_code = 0;
    let lower_case_arr = [];
    for (let i = 0; i < str.length; i++) {
        char_code = str.charCodeAt(i);
        if (char_code >= 65 && char_code <= 90)
            char_code += 32
        lower_case_arr.push(char_code);
    }
    return String.fromCharCode(...lower_case_arr);
};
```
