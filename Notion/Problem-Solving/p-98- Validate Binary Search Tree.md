---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:36
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:37
tags:
  - BT
  - DFS
  - Medium
  - Tree
  - bst
  - leetcode
---
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.  
The right subtree of a node contains only nodes with keys greater than the node's key.  
Both the left and right subtrees must also be binary search trees.  

### Solution

create a sub function and there compare node value with left and right  
if not left < node value < right, then it false  
and do the recursive call  
first time,  
node is left node and left value will be same and right value is node value  
node is right one, left is node value and right is right  

```Plain
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:

        def check(node, left, right):
            if not node:
                return True

            if not (left < node.val < right):
                return False

            return check(node.left, left, node.val) and check(node.right, node.val, right)


        return check(root, float("-inf"), float("inf"))


```