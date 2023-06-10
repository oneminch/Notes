---
title: Undirected Path
problemUrl: https://structy.net/problems/undirected-path
tags:
  - python
  - graph
  - traversal
---

**My Solution**:

```py
def undirected_path(edges, node_A, node_B):
    adj_list = {}

    # Convert edge list into adjacency list
    for e in edges:   
        if e[0] not in adj_list:
            adj_list[e[0]] = []
        if e[1] not in adj_list:
            adj_list[e[1]] = []

        adj_list[e[1]].append(e[0])
        adj_list[e[0]].append(e[1])

    stack = [node_A]
    visited = []

    # Traverse the undirected graph
    while len(stack) > 0:
        current = stack.pop(0)

        if current == node_B:
            return True

        if current in visited:
            continue

        visited.append(current)

        for e in adj_list[current]:
            stack.append(e)

    return False
```
