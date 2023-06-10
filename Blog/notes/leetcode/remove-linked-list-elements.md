---
title: Remove Linked List Elements
problemUrl: https://leetcode.com/problems/remove-linked-list-elements/
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

def removeElements(head: Optional[ListNode], val: int) -> Optional[ListNode]:
    new_node = ListNode(0, head)
    
    curr = new_node
    
    while curr:
        if curr.next and curr.next.val == val:
            curr.next = curr.next.next
        else:
            curr = curr.next

    return new_node.next
```
