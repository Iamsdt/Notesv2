---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:39
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:40
tags:
  - BT
  - DFS
  - Stack
  - easy
  - leetcode
---
Given the root of a binary tree, return the preorder traversal of its nodes' values.

### Notes:

### Depth First Traversals:

- Inorder (Left, Root, Right) : 4 2 5 1 3
- Preorder (Root, Left, Right) : 1 2 4 5 3
- Postorder (Left, Right, Root) : 4 5 2 3 1
- Breadth-First or Level Order Traversal: 1 2 3 4 5

### Solution

```Plain
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        data = []

        if root and root.val:
            data.append(root.val)

        if root and root.left:
            data += self.preorderTraversal(root.left)


        if root and root.right:
            data += self.preorderTraversal(root.right)

        return data

```

Tricky Solution:

```Plain
def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []

        return [root.val] + self.preorderTraversal(root.left) + self.preorderTraversal(root.right)
```