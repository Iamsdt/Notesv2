---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:39
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:39
tags:
  - BFS
  - BT
  - Medium
  - Tree
  - leetcode
---
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

### Solution:

1. use queue (collections.deque)
2. add the root into queue
3. Now popleft and add the value in level list
4. During popleft, push left and right into queue also

```Plain
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

import collections

class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []

        q = collections.deque()

        q.append(root)

        while q:
            qlen = len(q)
            level = []
            for i in range(qlen):
                node = q.popleft()
                if node:
                    level.append(node.val)
                    q.append(node.left)
                    q.append(node.right)

            if level:
                res.append(level)

        return res

```