---
alias: DS
---

## Introduction

- A data structure is a way of organizing data in a way that it can be accessed or updated efficiently.
- An abstract data type (ADT) is an abstraction of a data structure which provides only the interface to which a data structure must adhere to.
    - This interface doesn't give any specific details about how something should be implemented or in what language.
    - The interface (or ADT) describes what a DS does, while an implementation describes how the DS does it. An ADT defines the set of operations supported by a DS and the semantics, or meaning, of those operations.
    - A DS implementation includes the internal representation of the DS as well as the definitions of the algorithms that implement the supported operations.
    - **List** (Interface / ADT) can be implemented using **Array**s or using pointer-based data structures like a **Linked List**s (Implementation / DS).
- Operations on data structures:
    - Access
    - Insertion
    - Deletion
    - Traversal
    - Searching
    - Sorting

> [!quote]- Big-O Cheat Sheet
> ![Common DS Operations](dsa-common-ops.png)
> **Source**: [Big-O Cheat Sheet](https://www.bigocheatsheet.com)

## Arrays

- Items are organized sequentially in memory.
- Cost of operations on arrays:
    - Lookup, Update & Push - $O(1)$
    - Traverse, Insert & Delete - $O(n)$
- **Static arrays** are fixed size arrays. 
    - Number of elements is specified ahead of time.
    - C++ uses static arrays.
- **Dynamic arrays** are flexible size arrays.
    - When pushing new elements to the array, they are automatically resized by copying the entire array and moving it to a new area in memory with extra space allocation (usually double the original size).
        - Due to this fact, a `push` operation can be $O(n)$ with dynamic arrays.
    - [[JavaScript]] & [[Python]] use dynamic arrays.

## Hash Tables

- uses hash functions.
- **Collision** -  when two items hash to the same slot.

## Linked Lists

- Items are scattered across memory.
- Cost of operations on linked lists:
    - Prepend, Insert, Delete & Append - $O(1)$
    - Lookup & Traverse - $O(n)$
- When compared to arrays, linked lists:
    - have faster insertion and deletion.
    - have flexible size.
    - have slower lookups.
    - requires more memory.

## Stacks

- Cost of operations on stacks:
    - Lookup - $O(n)$
    - Peek, Pop & Push - $O(1)$

## Queues

- Cost of operations on queues:
    - Lookup - $O(n)$
    - Dequeue, Enqueue & Peek - $O(1)$

## Trees

### Binary Trees

### Binary Search Trees

- Cost of operations on BSTs:
    - Access, Lookup, Insert & Delete - $O(n)$ ==?==

### Priority Queues

- Abstract data types where each piece of data contains a key and a priority. Instead of FIFO approach, a priority value is used to enqueue and dequeue items.

### Heaps

- Tree-based implementation of priority queues.
- Can be created from other data structures like arrays. This is known as ==heapifying==.
- After heapifying an array, inserting a node or removing a node, the keys might become out of order. The process of reordering keys that are out of order is known as ==balancing a heap==.
- Cost of operations on heaps:
    - Finding the maximum value in a max heap or minimum value in a min heap - $O(1)$
    - Inserting data, removing the maximum value from a max heap or minimum value from a min heap - $O(log(n))$
    - Lookup - $O(n)$
- Helpful when executing tasks according to priority. 
    - e.g. Dijkstra's algorithm to find shortest path between two graph nodes can be implemented using heaps.

#### Binary Heap

- A heap built using a binary tree as an underlying data structure.

##### Min Heap

- A heap where a parent node's priority is always less than or equal to that of its children's priorities.

> [!note]
> The root node of the tree has the lowest priority.

##### Max Heap

- A heap where a parent node's priority is always greater than or equal to that of its children's priorities.

> [!note]
> The root node of the tree has the highest priority.

### AVL Trees / Red Black Trees (?)

### Tries (?)

### Tree Traversals

![Tree Traversals](tree-traversal.png)
- **Source**: [The Roadmap](https://roadmap.sh)

## Graphs

- Graphs can contain information in both the nodes and edges.
    - **Directed Graphs** - traversal can only be done in certain explicitly-stated directions. 
    - **Undirected Graphs** - traversal is bidirectional between any two nodes / vertices.
- Graphs can contain information in both the nodes and edges.
    - **Weighted Graphs** - information is associated with the edges. 
    - **Unweighted Graphs** - edges don't hold any information.
- Graphs can also be either **cyclic** or **acyclic**.
- Adjacency Matrix / List

### Graph Traversals

- BFS
- DFS

## Interfaces

- **Queue** Interface - represents a collection of elements to which we can all elements and remove the next element. Supported operations:
    - `add(x)`: add value of x to the Queue
    - `remove()`: remove the previously added value `y` from the Queue and return it.
        - The Queue's _queueing discipline_ decides which element to remove.
        - Most common disciplines: _FIFO_, _Priority_, & _LIFO_
    - A **FIFO Queue** removes items in the same order they were added. It works in the same way a grocery store checkout queue works. This is the most common kind of **Queue**, hence the "_FIFO_" is usually omitted. The operations `add(x)` and `remove()` are often called `enqueue(x)` and `dequeue()`, respectively.
    - A **Priority Queue** always removes the smallest element from the Queue, breaking ties arbitrarily. The `remove()` op on a priority Queue is usually called `delete_min()`.
    - In a **LIFO Queue** (also rta a **Stack**), the most recently added element is the next one removed. This can be best visualized in terms of a stack of plates, where plates are place on top of a stack and removed from the top of the stack.
        - To avoid confusion between LIFO and FIFO queueing disciplines, operations of a **Stack** are usually called `push(x)` and `pop()` instead of `add(x)` and `remove()`.
    - A **Deque** is a generalization of both the FIFO Queue and LIFO Queue. It represents a sequence of elements, with a front and a back, and elements can be added to either side of the sequence using these self-explanatory operations: `add_first(x)`, `remove_first()`, `add_last(x)`, & `remove_last()`.
        - A **Stack** can be implemented using only `add_first(x)` & `remove_first()`.
        - A FIFO Queue (or just a **Queue**) can be implemented using `add_last(x)`, & `remove_first()`.

- **List** Interface - represents a linear sequence of values: x*{0},..., x*{n−1}.
    - Supported operations are:
        - `size()` - return n, the length of the list
        - `get(i)` - return the value x\_{i}
        - `set(i, x)` - set the value of x\_{i} equal to x
        - `add(i, x)` - insert x at position i, displacing x*{i},..., x*{n−1}. Set x*{j+1} = x*{j}, for all j ∈ {n −1, ..., i}, increment n, and set x\_{i} = x
        - `remove(i)` - remove the value x*{i}, displacing x*{i+1}, ..., x*{n−1}. Set x*{j} = x\_{j+1}, for all j ∈ {i, ..., n −2} and decrement n
    - The above operations are sufficient to implement the Deque interface:
        - `add_first(x)` -> `add(0,x)`
        - `remove_first()` -> `remove(0)`
        - `add_last(x)` -> `add(size(),x)`
        - `remove_last()` -> `remove(size() −1)`
- **USet** Interface (Unordered Sets) - represents an unordered set of unique elements.
    - It contains `n` distinct elements; no element appears more than once & the elements are in no specific order.
    - Operations are:
        - `size()` - return the number of elements in a set.
        - `add(x)` - add an element `x` if not already present; Return `true` on success and `false` otherwise.
        - `remove(x)` - remove an element `y` from a set where `y` equals `x`; Return `y`, or `nil` if no such element exists.
        - `find(x)` - find an element `y` such that `y` equals `x` in a set if it exists; Return `y`, or `nil` if no such element exists.
    - Dictionaries/maps are formed with compound objects or pairs, each of which contains a key and a value.
    - Two pairs are treated as equal if their keys are equal.
- **SSet** Interface (Sorted Sets) - represents a sorted set of elements.
    - It stores elements from some total order, so that any two elements x and y can be compared.
    - $$
    compare(x,y)
    \begin{cases}
    < 0, & \text{if } x < y\\
    > 0, & \text{if } x > y\\
    = 0, & \text{if } x = y
    \end{cases}
    $$
    - An **SSet**s supports the same operations as the **USet**, with the exception of `find(x)`. In the case of **SSet**s, `find(x)`, usually rta _successor search_, finds the smallest element `y` such that `y` $\ge$ `x` in a set if it exists; Return `y`, or `nil` if no such element exists.
        - `SSet.find(x)` differs fundamentally from `USet.find(x)` since it returns a meaning full result even when there is no element in the set that's equal to `x`.
        - This extra functionality provided by `SSet.find(x)` is usually expensive both in terms of runtime and implementation complexity.

---

> [!question]- Interview Emphasis Points
> > Concepts / sections to focus on when reading
> - Arrays
> - Maps
> - Sets
> - Stacks / Queues
> - Linked Lists
> - Trees
> - Graphs
> - Matrix (2D Arrays)
