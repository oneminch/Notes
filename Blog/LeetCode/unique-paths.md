---
title: Unique Paths
problemUrl: https://leetcode.com/problems/unique-paths
tags:
  - javascript
  - dynamic programming
---

**My Solution**:

```javascript
var uniquePaths = (function(m, n) {
    let cache = {}
    
    const func = function(m, n) {
        if (m === 1 && n === 1) return 1
        if (m === 0 || n === 0) return 0
        
        const key1 = `${m},${n}`
        const key2 = `${n},${m}`
        
        if (key1 in cache || key2 in cache) {
            result = cache[key1]
        } else {
            result= func(m-1, n) + func(m, n-1)
            cache[key1] = result
            cache[key2] = result
        }
        
        return result
    }

    return func;
})();
```
