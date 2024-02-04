---
title: Number of Good Pairs
problemUrl: https://leetcode.com/problems/number-of-good-pairs
tags:
  - javascript
  - hash table
---

## My Solution

### JavaScript

```typescript
function numIdenticalPairs(nums: number[]): number {
  let pairCount = 0;
  const hashMap: Record<string, number[]> = {};

  for (let i = 0; i < nums.length; i++) {
    if (nums[i] in hashMap) {
      hashMap[nums[i]].push(i);
      pairCount += hashMap[nums[i]].length - 1;
    } else {
      hashMap[nums[i]] = [i];
    }
  }

  return pairCount;
}
```
