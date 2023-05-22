- The computational complexity or just simply complexity of an algorithm is the amount of resources required to run it, especially with respect to time and memory requirements.
    - How much time does an algorithm need to finish?
    - How much space does an algorithm need for its computation?
- [[Big-O]] gives an asymptotic upper bound of the growth rate in the worst case, which helps to quantify algorithmic performance as input size grows infinitely.
- It describes how the time and space requirements of an algorithm increase as its input size grows.

- The three most important things when it comes to studying the performance of data structures:
    - **Correctness** - correct implementation of interface.
    - **[[Time Complexity]]** - The running times of operations should be as small as possible.
    - **[[Space Complexity]]** - Memory use should be as little as possible.

## [[Time Complexity]]

- Things that cause time in a function:
    - Arithmetic operations
    - Comparisons
    - Loops
    - Outside function calls
- In most (but not all) cases, recursion complexities are $O(d^h)$, where d is the degree (the number of nodes coming out of a node when program is visualized as a tree) and h is the depth (height) of the tree.
- In the Fibonacci algorithm below, the degree is `2` because we are making two recursive calls.

```python
def fib(n):
    if n < 0:
        return -1
    elif n == 1:
        return 1
    else:
        return fib(n-1) + fib(n-2)
```

- In situations where calling a function recursively can be avoided, time complexity can be different. e.g. The time complexity of a DFS algorithm in a 2D matrix where movement is allowed in all directions is $O(n)$, where `n` is the number of items in the matrix. If a node is already visited, it can be marked as such and the algorithm can be optimized.

## [[Space Complexity]]

- Things that cause space complexity:
    - Variables
    - Function calls
    - Allocations
    - Data structures

- Data structures that don't grow with respect to input size usually have a constant space complexity.
- Copying and slicing methods are expensive in both time and space.
- Built-in functions like Python's `sort()` and operators like `n` have their own complexities under the hood.
- Sets are highly optimized, so set operations are fast in most circumstances.

---

- [[Time Complexity]]
    - Cost Model
    - Order of Growth
    - [[Big-O]]
- [[Space Complexity]]
- NP Completeness
- Amortization

## Further

### Reads 📄

- [[Math]]
