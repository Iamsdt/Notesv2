---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:47
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:46
tags:
  - easy
  - leetcode
  - linkedlist
  - recursion
---
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

### Solution

take dummy nodes and take current  
compare l1 value with l2, and save into current.next  
also update l1 and l2 based on condition and current  
on edge case take the remaining one  

```Plain
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        current = dummy

        while list1 and list2:
            if list1.val <= list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next

            current = current.next

        if list1:
            current.next = list1

        elif list2:
            current.next = list2

        return dummy.next

```