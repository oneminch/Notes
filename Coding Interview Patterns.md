## Two Pointers

- Input: One or two arrays / strings, typically sorted
- Look at two different indices at the same time.
- Variations
    - **Opposite Pointers**
        - Pointers start at opposite ends of an input and move towards each other.
        - e.g. Reverse a string in-place, Determine if a string is a palindrome
    - **Slow & Fast Pointers**
        - Pointers start near the start and move towards the end at different speeds / steps.
        - Useful when dealing with cyclic arrays or linked lists
        - e.g. Merge 2 sorted arrays, Determine the intersection of 2 arrays
    - **2-Array Pointers**
        - Pointers are used to traverse 2 different inputs.
        - e.g. Merge 2 sorted arrays, Determine the intersection of 2 arrays

## Sliding Window

- **Input**: A linear data structure (linked list, array or string)
- **Keywords:** substring, subarray, range, window, contiguous, consecutive, anagram, longest, shortest, length.
- Perform an operation on a specific window size of a given data structure.
- A typical question involves finding a contiguous subset that fulfills certain criteria like finding longest/shortest substring/subarray.
- **Examples**
    - Find the longest subarray containing all 0s.
    - Longest substring with "K" distinct characters
    - String anagrams

## Merge Intervals

- **Keywords:** `mutually exclusive`, `overlapping intervals`
- Typically used for finding or merging overlapping intervals.

## Backtracking

- Explore all possible solutions, then correct path if wrong by backtracking 

## Dynamic Programming

- Knapsack

## Greedy

## Cyclic Sort

- Find the missing / duplicate / smallest numbers in a sorted list.

## Topological Sort

## Two Heaps

- Find the smallest / largest / median elements of a given set.

## Tree: BFS & DFS

- **BFS Keywords:** `Level-order traversal`
- **DFS Keywords:** `in-order / post-order / pre-order DFS traversal`

- Tree BFS uses a queue for traversal.
- Tree DFS uses a stack (iteratively) or recursion for traversal.

## In-place Linked List Reversal

- Useful for reversing a linked list without using extra memory.
- Accomplished by keeping track of two variables (for current node and previous node).
    - Each step updates the `next` pointer of the current node to point to the previous node.

## Subsets

- Make use of BFS.
- For exploring all subsets of a given set.
- Find the combinations / permutations of a given set.

## K-way Merge

- Input involves a set of sorted lists.
- **Example:** Merge K-sorted lists

## Top 'K' Elements

- Find the top frequent / smallest `K` elements in a given set.
- Heaps can be useful.

![Find 3 largest numbers in an array|300](assets/compsci.top-k.png)
- **Source:** [HackerNoon](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)


## Further

## Reads 📄

- [14 Patterns to Ace Any Coding Interview Question](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)

- [Grokking the Coding Interview: Mastering the 20 Coding Patterns](https://www.designgurus.io/blog/Grokking-the-Coding%20Interview-Patterns)

