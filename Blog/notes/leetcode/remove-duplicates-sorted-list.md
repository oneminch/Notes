---
title: Remove Duplicates from Sorted List
problemUrl: https://leetcode.com/problems/remove-duplicates-from-sorted-list/
tags:
  - python
  - data structures
  - linked list
---

**My Solution**:

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

def deleteDuplicates(head: Optional[ListNode]) -> Optional[ListNode]:
		# empty or single item list
		if not head or not head.next:
				return head

		cur_node = head

		while cur_node.next:
				nxt_node = cur_node.next

				if cur_node.val == nxt_node.val:
						cur_node.next = nxt_node.next
				else:
						cur_node = cur_node.next
						nxt_node = nxt_node.next

		return head
```
