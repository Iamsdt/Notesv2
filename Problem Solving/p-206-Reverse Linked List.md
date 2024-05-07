---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:46
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:42
tags:
  - easy
  - leetcode
  - linkedlist
  - recursion
---
Given the head of a singly linked list, reverse the list, and return the reversed list.

### Solution

maintain two pointer, prev, and curr  
then save current.next into temp and update with prev value  
prev will be current one and current will be temp  

```Plain
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        current = head

        while current:
            temp = current.next
            current.next = prev
            prev = current
            current = temp

        return prev

```