---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:38
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:37
tags:
  - BFS
  - BT
  - DFS
  - Tree
  - easy
  - leetcode
---
Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

### Solution

Iterative (BFS):

1. use queue and root two times
2. in loop, take pops two times
3. if both are none continue or one is none return false
4. if value doesn't match return False
5. now need to add
6. For Symmetric,  
    we need to compare node1 left with node2 right  
    add this things into queue this way  
    

```Plain
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

import collections

class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if root == None:
            return True

        queue = collections.deque([root, root])

        while queue:
            r1 = queue.pop()
            r2 = queue.pop()
            if r1 == None and r2 == None:
                continue
            if r1 == None or r2 == None:
                return False
            if r1.val != r2.val:
                return False
            queue.append(r1.left)
            queue.append(r2.right)
            queue.append(r1.right)
            queue.append(r2.left)

        return True

```

Iterative (DFS):

```Plain
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root == None:
            return True
        stack = [root,root]
        while stack:
            r1 = stack.pop()
            r2 = stack.pop()
            if r1 == None and r2 == None:
                continue
            if r1 == None or r2 == None:
                return False
            if r1.val != r2.val:
                return False
            stack.append(r1.left)
            stack.append(r2.right)
            stack.append(r1.right)
            stack.append(r2.left)
        return True
```