
- **Memoization** is a common ==dynamic programming== technique that ensures a function doesn't run for the same inputs more than once by keeping a cache of the input-result mappings for the given inputs (usually in a hash map type data structure).

**Wrapping function in a class**

```python
class Fib():
    def __init__(self):
        self.cache = {}

    def calc(self, n):
        # Base Case
        if n in [0, 1]:
            return n

        if n in self.cache:
            return self.cache[n]

        result = self.calc(n-1) + self.calc(n-2)
        self.cache[n] = result

        return result


print(Fib().calc(5))
```

**Using a closure / decorator**

```python
def fib():
    cache = {}
    
    def calc(n):
        # Base Case
        if n in [0, 1]:
            return n

        if n in cache:
            return cache[n]

        result = calc(n-1) + calc(n-2)
        cache[n] = result

        return result
        
    return calc


memoized_fib = fib()
print(memoized_fib(5))
```

- By caching the results of some inputs, the above implementations of the Fibonacci calculator reduces repeated function calls for the same inputs. For the input `6`, the number of repeated calls is reduced by 7, which is significant considering the small input and the memory usage of recursive functions:

> [!example] Function Call Tree Example
> ![Memoized Fibonacci](assets/images/compsci.algo-memoized-fibonacci.svg)
>> [!info]- Source
>> [Interview Cake](https://www.interviewcake.com/concept/python/memoization)