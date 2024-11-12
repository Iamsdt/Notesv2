---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - tree
  - leetcode
---

A tree is a hierarchical data structure consisting of nodes connected by edges. It's a special type of graph with no cycles, meaning there is exactly one path between any two nodes.

![[Pasted image 20240903160211.png]]


### 1. **Introduction to Trees**
   - **Terminology**:
     - **Node**: The fundamental unit of a tree. It contains data and references to its child nodes.
     - **Root**: The topmost node in a tree, from which all nodes descend.
     - **Child**: A node directly connected to another node when moving away from the root.
     - **Parent**: The node connected to another node when moving towards the root.
     - **Leaf**: A node with no children.
     - **Subtree**: A tree formed by a node and its descendants.
     - **Height**: The length of the longest path from a node to a leaf. The height of the tree is the height of the root.
     - **Depth**: The length of the path from the root to a node.
     - **Sibling**: Nodes that share the same parent.

![[Pasted image 20240903160911.png]]

### 2. **Types of Trees**
   - **Binary Tree**: Each node has at most two children (left and right).
   - **Binary Search Tree (BST)**: A binary tree where the left subtree contains values less than the node, and the right subtree contains values greater than the node.
   - **Balanced Trees**: Trees where the height of the left and right subtrees differ by at most one, ensuring logarithmic depth for efficient operations (e.g., AVL trees, Red-Black trees).
   - **Trie (Prefix Tree)**: A special type of tree used for storing associative data structures, typically strings
   - **N-ary Tree**: A tree where each node can have at most N children.

![[Pasted image 20240903162035.png]]

### 3. **Tree Traversal Techniques**
   - **Depth-First Traversal (DFT)**:
     - **Pre-order**: Visit the root, traverse the left subtree, then traverse the right subtree.
     - **In-order**: Traverse the left subtree, visit the root, then traverse the right subtree (commonly used in BSTs for sorted order).
     - **Post-order**: Traverse the left subtree, traverse the right subtree, then visit the root.
   - **Breadth-First Traversal (BFT)**:
     - Also known as Level-order traversal. Visit nodes level by level from the root down to the leaves.

### 4. Binary Tree (BT): 
A Binary Tree is a hierarchical data structure in which each node has at most two children, referred to as the left child and the right child. It is not necessarily ordered, and the structure of the tree can vary widely.

![[Pasted image 20240903164037.png]]

- **Full Binary Tree**: A binary tree where every node has either 0 or 2 children.
- **Complete Binary Tree**: A binary tree in which all levels are fully filled except possibly the last level, which is filled from left to right.
- **Degenerate (or Pathological) Binary Tree**: A binary tree where each parent node has only one child, resulting in a structure that resembles a linked list.
- **Perfect Binary Tree**: A binary tree where all internal nodes have exactly two children, and all leaf nodes are at the same level.
- **Balanced Binary Tree**: A binary tree where the height difference between the left and right subtrees for every node is at most one.

#### 4.1 Operations
##### 4.1.1 Insert
- **Details**: In a binary tree, the insertion operation typically involves adding a new node at the first available position in level order. This ensures the tree remains as compact as possible.
- **Time Complexity**: O(n) (where n is the number of nodes in the tree, as you might need to traverse the entire tree in the worst case).
- **Python Code**:
    ```python
    class Node:
        def __init__(self, key):
            self.left = None
            self.right = None
            self.val = key

    def insert(root, key):
        if root is None:
            return Node(key)
        
        queue = [root]
        
        while queue:
            temp = queue.pop(0)
            
            if not temp.left:
                temp.left = Node(key)
                break
            else:
                queue.append(temp.left)
                
            if not temp.right:
                temp.right = Node(key)
                break
            else:
                queue.append(temp.right)
    ```

##### 4.1.2 Deletion
- **Details**: Deleting a node from a binary tree involves finding the node to delete, replacing it with the deepest and rightmost node, and then removing the deepest node.
- **Time Complexity**: O(n)
- **Python Code**:
    ```python
    def delete(root, key):
        if root is None:
            return None
        
        if root.left is None and root.right is None:
            if root.val == key:
                return None
            else:
                return root
        
        key_node = None
        queue = [root]
        temp = None
        
        while queue:
            temp = queue.pop(0)
            
            if temp.val == key:
                key_node = temp
            
            if temp.left:
                queue.append(temp.left)
                
            if temp.right:
                queue.append(temp.right)
        
        if key_node:
            key_node.val = temp.val
            delete_deepest(root, temp)
        
        return root

    def delete_deepest(root, d_node):
        queue = [root]
        while queue:
            temp = queue.pop(0)
            
            if temp is d_node:
                temp = None
                return
            
            if temp.right:
                if temp.right is d_node:
                    temp.right = None
                    return
                else:
                    queue.append(temp.right)
                    
            if temp.left:
                if temp.left is d_node:
                    temp.left = None
                    return
                else:
                    queue.append(temp.left)
    ```

##### 4.1.3 Searching
- **Details**: Searching in a binary tree involves traversing the tree to find a node with a given key.
- **Time Complexity**: O(n)
- **Python Code**:
    ```python
    def search(root, key):
        if root is None or root.val == key:
            return root
        
        res1 = search(root.left, key)
        if res1:
            return res1
        
        return search(root.right, key)
    ```

##### 4.1.4 Traversal
- **Details**: Traversal refers to visiting all nodes in a specific order. Common traversals include Inorder, Preorder, and Postorder.
- **Time Complexity**: O(n)
- **Python Code**:
    ```python
    def inorder(root):
        if root:
            inorder(root.left)
            print(root.val, end=' ')
            inorder(root.right)

    def preorder(root):
        if root:
            print(root.val, end=' ')
            preorder(root.left)
            preorder(root.right)

    def postorder(root):
        if root:
            postorder(root.left)
            postorder(root.right)
            print(root.val, end=' ')
    ```

### 5. Binary Search Tree (BST)
A Binary Search Tree is a binary tree with the property that the value of each node is greater than all the values in its left subtree and less than all the values in its right subtree.

![[Pasted image 20240903164456.png]]

#### 5.1 Operations
##### 5.1.1 Insert
- **Details**: In a BST, the insertion is done by comparing the key with the value of the current node and moving to the left or right subtree accordingly until the appropriate position is found.
- **Time Complexity**: O(log n) on average, O(n) in the worst case.
- **Python Code**:
    ```python
    def insert_bst(root, key):
        if root is None:
            return Node(key)
        
        if key < root.val:
            root.left = insert_bst(root.left, key)
        else:
            root.right = insert_bst(root.right, key)
        
        return root
    ```

##### 5.1.2 Deletion
- **Details**: Deleting a node from a BST involves three cases: the node is a leaf, the node has one child, or the node has two children.
- **Time Complexity**: O(log n) on average, O(n) in the worst case.
- **Python Code**:
    ```python
    def delete_bst(root, key):
        if root is None:
            return root
        
        if key < root.val:
            root.left = delete_bst(root.left, key)
        elif key > root.val:
            root.right = delete_bst(root.right, key)
        else:
            if root.left is None:
                return root.right
            elif root.right is None:
                return root.left
            
            temp = min_value_node(root.right)
            root.val = temp.val
            root.right = delete_bst(root.right, temp.val)
        
        return root

    def min_value_node(node):
        current = node
        while current.left:
            current = current.left
        
        return current
    ```

##### 5.1.3 Searching
- **Details**: Searching in a BST is efficient because you can discard half of the tree at each step by following the BST property.
- **Time Complexity**: O(log n) on average, O(n) in the worst case.
- **Python Code**:
    ```python
    def search_bst(root, key):
        if root is None or root.val == key:
            return root
        
        if key < root.val:
            return search_bst(root.left, key)
        
        return search_bst(root.right, key)
    ```

##### 5.1.4 Traversal
- **Details**: Traversal in a BST is the same as in a binary tree, but Inorder traversal will return nodes in sorted order.
- **Time Complexity**: O(n)
- **Python Code**:
    ```python
    # Inorder, Preorder, and Postorder traversal functions are the same as above
    ```

### 6. AVL Tree
An AVL Tree is a self-balancing binary search tree where the difference between the heights of the left and right subtrees cannot be more than one for all nodes.
![[Pasted image 20240903164545.png]]
#### 6.1 Operations

##### 6.1.1 Insert
- **Details**: Inserting in an AVL tree is similar to a BST, but after each insertion, the tree is checked for balance, and rotations are performed if necessary to maintain the AVL property.
- **Time Complexity**: O(log n)
- **Python Code**:
    ```python
    class AVLNode:
        def __init__(self, key):
            self.val = key
            self.left = None
            self.right = None
            self.height = 1

    def insert_avl(root, key):
        if root is None:
            return AVLNode(key)
        
        if key < root.val:
            root.left = insert_avl(root.left, key)
        else:
            root.right = insert_avl(root.right, key)
        
        root.height = 1 + max(height(root.left), height(root.right))
        
        balance = get_balance(root)
        
        if balance > 1 and key < root.left.val:
            return right_rotate(root)
        
        if balance < -1 and key > root.right.val:
            return left_rotate(root)
        
        if balance > 1 and key > root.left.val:
            root.left = left_rotate(root.left)
            return right_rotate(root)
        
        if balance < -1 and key < root.right.val:
            root.right = right_rotate(root.right)
            return left_rotate(root)
        
        return root

    def height(node):
        if not node:
            return 0
        return node.height

    def get_balance(node):
        if not node:
            return 0
        return height(node.left) - height(node.right)

    def right_rotate(y):
        x = y.left
        T2 = x.right
        
        x.right = y
        y.left = T2
        
        y.height = 1 + max(height(y.left), height(y.right))
        x.height = 1 + max(height(x.left), height(x.right))
        
        return x

    def left_rotate(x):
        y = x.right
        T2 = y.left
        
        y.left = x
        x.right = T2
        
        x.height = 1 + max(height(x.left), height(x.right))
        y.height = 1 + max(height(y.left), height(y.right))
        
        return y
    ```

##### 6.1.2 Deletion
- **Details**: Deletion in an AVL tree is similar to a BST, followed by rebalancing the tree by performing rotations

### 7. **Applications of Trees**
   - **Binary Search Trees (BSTs)**: Used in searching, sorting algorithms, and dynamic sets.
   - **Heaps**: Used in priority queues and heap sort algorithms.
   - **Tries**: Used in autocomplete systems, spell checkers, and IP routing.
   - **B-trees**: Used in databases and file systems for efficient data retrieval.
   - **Suffix Trees**: Used in string processing algorithms, like finding the longest repeated substring.

### 8. **Complexity Analysis**
   - **Time Complexity**:
     - **Insertion/Deletion/Search** in a balanced tree (e.g., AVL, Red-Black) is O(log n).
     - In an unbalanced BST, the worst-case time complexity can degrade to O(n).
   - **Space Complexity**:
     - Trees require O(n) space for n nodes.

### 9. **Balanced vs. Unbalanced Trees**
   - **Balanced Trees**: Ensure that operations such as insertion, deletion, and search have optimal time complexity (O(log n)).
   - **Unbalanced Trees**: Can degrade to a linear structure, making operations inefficient (O(n)).

### 10. Leetcode
- [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [Same Tree](https://leetcode.com/problems/same-tree/)
- [Invert/Flip Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
- [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)
- [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
- [Lowest Common Ancestor of BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
- [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)
- [Add and Search Word](https://leetcode.com/problems/add-and-search-word-data-structure-design/)
- [Word Search II](https://leetcode.com/problems/word-search-ii/)

### 11. References
1. [Tree Structure]( https://www.programiz.com/dsa/trees)
2. [Binary Tree](https://www.programiz.com/dsa/binary-tree)
3. [Full Binary Tree](https://www.programiz.com/dsa/full-binary-tree)
4. [Balanced Binary Tree](https://www.programiz.com/dsa/balanced-binary-tree)
5. [Binary Search Tree](https://www.programiz.com/dsa/binary-search-tree)
6. [AVL Tree](https://www.programiz.com/dsa/avl-tree)



Leetcode Solution:
104: [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        
        if not root:
            return 0
        
        # check very bottom
        if not root.left and not root.right:
            return 1
        
        left = 0
        right = 0
        
        left = 1 + self.maxDepth(root.left)
        
        right = 1 + self.maxDepth(root.right)
        
        return max(left, right)
        
```

100: Same Tree:
```python
class Solution:

    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if (not p and not q) or (not p or not q):
            return p == q

        if p.val != q.val:
            return False

        self.isSameTree(p.left, q.left)
        self.isSameTree(p.right, q.right)

        return (self.isSameTree(p.left, q.left)) and (self.isSameTree(p.right, q.right))
```


226: Invert Binary Tree
```python
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if root == None:
            return None
        
        root.left, root.right = root.right, root.left
        
        self.invertTree(root.left)
        self.invertTree(root.right)
        
        return root
```


105: [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

post order: [9, 15, 7, 20, 3]
```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder or not inorder:
            return None

        root = TreeNode(preorder[0])
        mid = inorder.index(preorder[0])
        root.left = self.buildTree(preorder[1:mid+1], inorder[:mid])
        root.right = self.buildTree(preorder[mid+1:], inorder[mid+1:])
        return root
```

And 106

[110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) (amazon)
```python
class Solution:
    def isBalanced(self, root: Optional[TreeNodef]) -> bool:
        
        def dfs(root):
            if not root: return [True, 0]
            
            left, right = dfs(root.left), dfs(root.right)
            
            balanced = (left[0] and right[0] and 
                        abs(left[1] - right[1]) <= 1)

            return [balanced, 1 + max(left[1], right[1])]

        return dfs(root)[0]
```



124. BT Maximum Path Sum (dfs)

```python
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        res =  [root.val]

        def dfs(root):    
            if not root:
                return 0

            left_max = dfs(root.left)
            right_max = dfs(root.right)

            # remove negative
            left_max = max(left_max, 0)
            right_max = max(right_max, 0)

            res[0] = max(res[0], root.val+ left_max+ right_max)

            return root.val + max(left_max, right_max)

        dfs(root)

        return res[0]
```


572. Subtree of Another Tree (same as 100)  (dfs)
```python
class Solution:
    def isSubtree(self, s: TreeNode, t: TreeNode) -> bool:
        if not t: return True
        if not s: return False
        
        if self.sameTree(s, t):
            return True
            
        return (self.isSubtree(s.left, t) or
                self.isSubtree(s.right, t))
    
    def sameTree(self, s, t):
        if not s and not t:
            return True
        if s and t and s.val == t.val:
            return (self.sameTree(s.left, t.left) and
                    self.sameTree(s.right, t.right))
        return False
```

98. [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) (dfs)
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        
        def check(node, left, right):
            if not node:
                return True
            # check actual condition
            if not (left < node.val < right):
                return False
            
            return check(node.left, left, node.val) and check(node.right, node.val, right)
        
        return check(root, float("-inf"), float('inf'))
```

[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        self.bfs(root, 0, res)
        return res
    
    def bfs(self, node: Optional[TreeNode], level: int, res: List[List[int]]):
        if not node:
            return
        
        if len(res) == level:
            res.append([])
        
        res[level].append(node.val)
        
        self.bfs(node.left, level + 1, res)
        self.bfs(node.right, level + 1, res)
```

Tree:
DFS
BFS