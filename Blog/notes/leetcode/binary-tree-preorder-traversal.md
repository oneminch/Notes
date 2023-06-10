---
title: Binary Tree Preorder Traversal
problemUrl: https://leetcode.com/problems/binary-tree-preorder-traversal/
tags:
  - python
  - binary trees
  - preorder traversal
  - dfs
---

**My Solution**:

```py
# Recursive Approach

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

def preorderTraversal(root: Optional[TreeNode]) -> List[int]:
    if not root:
        return []

    return [root.val, *preorderTraversal(root.left), *preorderTraversal(root.right)]
```
