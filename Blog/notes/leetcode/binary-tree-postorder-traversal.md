---
title: Binary Tree Postorder Traversal
problemUrl: https://leetcode.com/problems/binary-tree-postorder-traversal/
tags:
  - python
  - binary trees
  - postorder traversal
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

def postorderTraversal(root: Optional[TreeNode]) -> List[int]:
    if not root:
        return []

    return [*postorderTraversal(root.left), *postorderTraversal(root.right), root.val]
```
