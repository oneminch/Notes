---
title: Best Time to Buy and Sell Stock
problemUrl: https://leetcode.com/problems/best-time-to-buy-and-sell-stock
tags:
  - javascript
  - arrays
---

## My Solution

### JavaScript

```javascript
function maxProfit(prices: number[]): number {
  let min = prices[0],
    max = 0;

  for (let price of prices) {
    if (price < min) {
      min = price;
    }
    if (price - min > max) {
      max = price - min;
    }
  }

  return max;
}
```
