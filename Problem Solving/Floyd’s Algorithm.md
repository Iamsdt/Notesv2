---
Created by: Shudipto Trafder
Created time: 2023-10-18T19:55
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:24
tags:
  - algo
---
In order to detect cycles in any given singly linked list, we must set two pointers that traverse the data structure at different speeds. If they meet, we can determine that the list was circular. Then if we set the first pointer back to the head and slow them both down to the same speed, the next time they will meet will be the point where the node started pointing backward. The pseudo-code is as follows:

1. Initialize two pointers (tortoise and hare) that both point to the head of the linked list
2. Loop as long as the hare does not reach null
3. Set tortoise to next node
4. Set hare to next, next node
5. If they are at the same node, reset the tortoise back to the head.
6. Have both tortoise and hare both move one node at a time until they meet again
7. Return the node in which they meet
8. Else, if the hare reaches null, then return null