---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:47
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:43
tags:
  - TwoPointer
  - easy
  - hashtable
  - leetcode
  - linkedlist
---
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

### Solution

use [The Tortoise and the Hare (Floyd’s Algorithm)](https://medium.com/@tuvo1106/the-tortoise-and-the-hare-floyds-algorithm-87badf5f7d41)

### code

```Plain
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
         # Hash set way
         # Time complexity 0(n)
         # space com o(n)
#         temp = head

#         di = {}

#         while temp != None:
#             if temp in di:
#                 return True
#             else:
#                 di[temp] = 1

#             temp = temp.next

        # Lets use Floyd's Tortoise & Hare

        if head == None:
            return False

        tortoise = head
        hare = head

        while hare and hare.next:
            hare = hare.next.next
            tortoise = tortoise.next

            if hare == tortoise:
                return True

        return False

```