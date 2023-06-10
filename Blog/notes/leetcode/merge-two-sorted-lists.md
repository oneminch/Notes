---
title: Merge Two Sorted Lists
problemUrl: https://leetcode.com/problems/merge-two-sorted-lists
tags:
  - python
  - linked lists
  - sorting
---

**My Solution**:

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

def mergeTwoLists(list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
    # if either list is empty 
    if not list1:
        return list2
    elif not list2:
        return list1
    
    head1, head2 = list1, list2
    nodes = []
    
    # break down linkedlists into a regular list
    while True:
        if head1:
            nodes.append(head1.val)
            head1 = head1.next
        
        if head2:
            nodes.append(head2.val)
            head2 = head2.next

        if not head1 and not head2:
            break

    # build up sorted linkedlist from sorted list
    sorted_nodes = sorted(nodes)
    
    merged_list = ListNode(sorted_nodes[0])
    merged_head = merged_list
    
    for node in sorted_nodes[1:]:
        temp = ListNode(node)
        merged_list.next = temp
        merged_list = temp

    return merged_head
```
