---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:46
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:43
tags:
  - easy
  - leetcode
  - linkedlist
  - recursion
---
Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

### Solution just like deleting node from Linked List (multiple same values need to remove)

for edge case, check the head value after the loop

```Plain
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        if head is None:
            return []

        temp = head

        while temp.next:
            if temp.next.val == val:
                temp.next = temp.next.next
                continue

            temp = temp.next

        # for edge cases
        if head.val == val:
            return head.next

        return head

```