---
title: Flatten
problemUrl: https://www.greatfrontend.com/questions/javascript/flatten
tags:
  - javascript
  - arrays
  - recursion
---

## My Solution

### JavaScript

```javascript
/**
 * @param {Array<*|Array>} arr
 * @return {Array}
 */

function flatten(arr) {
  let flattenedArray = [];

  for (let x of arr) {
    if (!Array.isArray(x)) {
      flattenedArray.push(x);
    } else {
      flattenedArray.push(...flatten(x));
    }
  }

  return flattenedArray;
}
```
