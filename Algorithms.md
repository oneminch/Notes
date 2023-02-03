- An ==algorithm== is a series of steps that solve a particular problem.
    - The steps are clear and unambiguous.
    - The algorithm stops after a finite number of steps.
    - The same output should always be produced for a given input.
- The run time of an algorithm is the amount of time it takes a computer to execute the algorithm.
- The important part of an algorithm is the part that grows the fastest as its input size gets bigger.
- An algorithm's efficiency is usually expressed using [[Big-O]].
- An algorithm's **_order-of-magnitude_** dominates the equation and it describes the [[time complexity]] of an algorithm. Additionally, resource usage [[space complexity]]) should also be considered.

- Complexities ordered from most efficient (best) to least efficient (worst) in [[Big-O]], where n is the size of the input.
    - **Constant Time**: ==$O(1)$==
    - **Logarithmic Time**: ==$O(log(n))$==
        - Usually the algorithm reduces the computation amount by a certain amount in each iteration.
        - e.g. Binary search
    - **Linear Time**: ==$O(n)$==
        - e.g. Linear search
    - **Linearithmic / Log-linear Time**: ==$O(nlog(n))$==
        - e.g. Merge sort
    - **Quadric Time**: ==$O(n^2)$==
        - e.g. Insertion sort, bubble sort
    - **Cubic Time**: ==$O(n^3)$==
    - **Exponential Time**: ==$O(b^n), b > 1$==
        - e.g. Brute-force algorithms - test every possible option.
    - **Factorial Time**: ==$O(n!)$==

- **Best-case complexity** - how an algorithm performs with ideal output.
- **Worst-case complexity** - how an algorithm performs in the worst possible scenario.
- **Average-case complexity** - how an algorithm performs on average; this is often used as a starting point when comparing algorithms.

## Recursion

- A recursive algorithm must:
    - have a base case
    - move closer to the base case
    - call itself recursively
- Recursive algorithms typically take up more memory than their iterative alternatives.

## Searching

### Sequential / Linear search

- Iterates thru every element in a data set and compare it with the target value.
- Python's built-in `in` operator is linear.

- **Best case**: $O(1)$
- **Worst case**: $O(n)$
- **Average case**: $O(n/2)$

### Binary search

- List must be sorted.
- After $x$ iterations, the number of items in the list will be reduced to $n/2^x$.
- To calculate how many iterations it will take a binary search to determine an item is not there, solve for $x$ in $2^x = n$, where $n$ is the input size.

- **Best case**: $O()$
- **Worst case**: $O(n)$
- **Average case**: $O(n/2)$

---
  
- BFS / DFS
- Dijkstra's Algorithm
- String Search

- Divide & Conquer
- Shortest Paths
- Greedy algorithms
    - Dynamic programming
- Minimum spanning trees
- NP-completeness
- Sorting
    - Selection
    - Insertion
    - Heap
    - Quick
    - Merge
    - Bubble
- Hashing

## Further

### Learn 🧠

- [Algorithmic Design and Techniques - edX](https://www.edx.org/course/algorithmic-design-and-techniques)

### Books 📚

- [Cracking the Coding Interview](https://app.thestorygraph.com/books/61084720-073b-4d8b-b71a-7cc3fb77daa2)

- [Introduction to the Design and Analysis of Algorithms](https://app.thestorygraph.com/books/7b23f4fb-42ec-48e5-a0d4-f5b8575e6b2c)

- [The Algorithm Design Manual](https://app.thestorygraph.com/books/8783f581-7ded-4bd6-b8b7-67e464419018)

### Resources 🧩

- [Algorithm Visualizer](https://algorithm-visualizer.org/)

- [The Algorithms](https://the-algorithms.com/)

- [VisuAlgo](https://visualgo.net/en)
