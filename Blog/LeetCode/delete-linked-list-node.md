---
title: Delete Node in a Linked List
problemUrl: https://leetcode.com/problems/delete-node-in-a-linked-list/
tags:
  - python
  - linked lists
  - in-place
---

**My Solution**:

> Modified In-Place

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

def deleteNode(node):
    while node.next is not None:
        node.val = node.next.val
        
        if node.next.next is None:
            node.next = None
        else:
            node = node.next
```
