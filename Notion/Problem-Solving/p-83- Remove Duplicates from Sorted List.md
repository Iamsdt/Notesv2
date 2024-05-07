---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:46
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:41
tags:
  - easy
  - leetcode
  - linkedlist
---
Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

Solution:  
compare current value with next one if same then update to the next next one  

```Plain
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        temp = head
        while temp.next:
            if temp.val == temp.next.val:
                temp.next = temp.next.next
                continue

            temp = temp.next

        return head

```