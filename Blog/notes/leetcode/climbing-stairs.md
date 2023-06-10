---
title: Climbing Stairs
problemUrl: https://leetcode.com/problems/climbing-stairs/
tags:
  - python
  - javascript
  - memoization
  - dynamic programming
  - fibonacci
---

**My Solution**:

### Iterative Approach

```py
def climbStairs(n: int) -> int:
    seq = [2, 3]
        
    if n <= 3:
        return n
    
    for i in range(4, n+1):
        seq.append(seq[-1] + seq[-2])
        
    return seq[-1]
```

### Memoized Recursive Approach (using Python Classes)

```py
class Solution:
    def __init__(self):
        self.cache = {}


    def climbStairs(self, n: int) -> int:
        # Base Case
        if n <= 3:
            return n

        if n in self.cache:
            return self.cache[n]

        result = self.climbStairs(n-1) + self.climbStairs(n-2)
        self.cache[n] = result

        return result
```

### Memoized Recursive Approach (using JavaScript Closures)

```js
const climbStairs = (function() {
    let cache = {}
    
    const func = function(n) {
        if (n <= 2) return 1
        
        if (n in cache) {
            result = cache[n]
        } else {
            result = func(n-1) + func(n-2)
            cache[n] = result
        }
        
        return result
    }

    return func;
})()
```
