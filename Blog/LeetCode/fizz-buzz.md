---
title: Fizz Buzz
problemUrl: https://leetcode.com/problems/fizz-buzz/
tags:
  - python
---

**My Solution**:

```py
def fizzBuzz(n: int) -> List[str]:
    answer = [None]*n

    for i in range(0,n):
        k = i+1
        if k % 3 == 0 and k % 5 == 0:
            answer[i] = "FizzBuzz"
        elif k % 3 == 0:
            answer[i] = "Fizz"
        elif k % 5 == 0:
            answer[i] = "Buzz"
        else:
            answer[i] = str(k)

    return answer
```
