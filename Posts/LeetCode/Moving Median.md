---
title: Moving Median
problemUrl: https://coderbyte.com/information/Moving%20Median
tags:
  - javascript
  - arrays
  - median
---

## My Solution

### JavaScript

```javascript
function MovingMedian(arr) {
  let subArr = [],
    midpoint = 0,
    predecessors = arr[0] - 1;

  let nums = arr.slice(1);
  nums = nums.map((num, i) => {
    if (i == 0) return num;

    // get the range of arr elements for moving window
    if (i <= predecessors) {
      subArr = nums.slice(0, i + 1).sort((a, b) => a - b);
    } else {
      subArr = nums.slice(i - predecessors, i + 1).sort((a, b) => a - b);
    }

    // get midpoint
    midpoint = Math.floor(subArr.length / 2);

    // calculate the median for each range / subarray
    return subArr.length % 2
      ? subArr[midpoint]
      : (subArr[midpoint] + subArr[midpoint - 1]) / 2;
  });

  // return median list as string
  return nums.join(",");
}
```
