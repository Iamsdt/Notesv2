---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:39
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:38
tags:
  - BFS
  - BT
  - DFS
  - easy
  - leetcode
---
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

### Solution

1. if we reach very bottom then return 1 (no left, no right)
2. else add 1 and recursive call
3. return max of left and right

```Plain
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:

        if not root:
            return 0

        # check very bottom
        if not root.left and not root.right:
            return 1

        left = 1 + self.maxDepth(root.left)

        right = 1 + self.maxDepth(root.right)

        return max(left, right)

```