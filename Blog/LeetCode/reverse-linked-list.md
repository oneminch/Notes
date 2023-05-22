---
title: Reverse Linked List
problemUrl: https://leetcode.com/problems/reverse-linked-list/
tags:
  - python
  - linked lists
---

**My Solution**:

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

def reverseList(head: Optional[ListNode]) -> Optional[ListNode]:
    curr = head
    stack = []
    reversed_list = None
    
    while curr:
        reversed_list = ListNode(curr.val, reversed_list)
        stack.append(reversed_list)
        curr = curr.next
        
    return reversed_list
```
