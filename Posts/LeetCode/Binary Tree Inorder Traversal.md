---
title: Binary Tree Inorder Traversal
problemUrl: https://leetcode.com/problems/binary-tree-inorder-traversal/
tags:
  - python
  - binary trees
  - inorder traversal
  - dfs
---

## My Solution

### Python

**Recursive Approach**

```py
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def inorderTraversal(root: Optional[TreeNode]) -> List[int]:
    if not root:
        return []

    return [*inorderTraversal(root.left), root.val, *inorderTraversal(root.right)]
```
