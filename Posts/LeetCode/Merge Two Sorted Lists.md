---
title: Merge Two Sorted Lists
problemUrl: https://leetcode.com/problems/merge-two-sorted-lists
tags:
  - python
  - javascript
  - linked lists
  - sorting
---

## My Solution

### Python

```py
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


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

### JavaScript

```javascript
// Definition for singly-linked list.
class ListNode {
  val: number;
  next: ListNode | null;
  constructor(val?: number, next?: ListNode | null) {
    this.val = val === undefined ? 0 : val;
    this.next = next === undefined ? null : next;
  }
}

function mergeTwoLists(
  list1: ListNode | null,
  list2: ListNode | null
): ListNode | null {
  const mergedList = new ListNode();
  let head1 = list1,
    head2 = list2,
    head3 = mergedList;

  while (head1 && head2) {
    if (head1.val <= head2.val) {
      head3.next = new ListNode(head1.val, null);
      head1 = head1.next;
    } else {
      head3.next = new ListNode(head2.val, null);
      head2 = head2.next;
    }
    head3 = head3.next;
  }

  if (head1 && !head2) head3.next = head1;
  if (head2 && !head1) head3.next = head2;

  return mergedList.next;
}
```
