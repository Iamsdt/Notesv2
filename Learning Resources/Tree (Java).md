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

![[Pasted image 20240903161658.png]]


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
- **Java Code**:
```java
import java.util.LinkedList;
import java.util.Queue;

class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinaryTree {
    
    Node root;

    void insert(Node root, int key) {
        if (root == null) {
            this.root = new Node(key);
            return;
        }
        
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);
        
        while (!queue.isEmpty()) {
            Node temp = queue.poll();
            
            if (temp.left == null) {
                temp.left = new Node(key);
                break;
            } else {
                queue.add(temp.left);
            }
            
            if (temp.right == null) {
                temp.right = new Node(key);
                break;
            } else {
                queue.add(temp.right);
            }
        }
    }

    void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.val + " ");
            inorder(root.right);
        }
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.insert(tree.root, 1);
        tree.insert(tree.root, 2);
        tree.insert(tree.root, 3);
        tree.insert(tree.root, 4);
        tree.insert(tree.root, 5);

        System.out.println("Inorder traversal:");
        tree.inorder(tree.root);
    }
}

```

##### 4.1.2 Deletion
- **Details**: Deleting a node from a binary tree involves finding the node to delete, replacing it with the deepest and rightmost node, and then removing the deepest node.
- **Time Complexity**: O(n)
- **Java Code**:
```java
import java.util.LinkedList;
import java.util.Queue;

class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinaryTree {

    Node root;

    Node delete(Node root, int key) {
        if (root == null) {
            return null;
        }

        if (root.left == null && root.right == null) {
            if (root.val == key) {
                return null;
            } else {
                return root;
            }
        }

        Node keyNode = null;
        Node temp = null;
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            temp = queue.poll();

            if (temp.val == key) {
                keyNode = temp;
            }

            if (temp.left != null) {
                queue.add(temp.left);
            }

            if (temp.right != null) {
                queue.add(temp.right);
            }
        }

        if (keyNode != null) {
            keyNode.val = temp.val;
            deleteDeepest(root, temp);
        }

        return root;
    }

    void deleteDeepest(Node root, Node dNode) {
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            Node temp = queue.poll();

            if (temp == dNode) {
                temp = null;
                return;
            }

            if (temp.right != null) {
                if (temp.right == dNode) {
                    temp.right = null;
                    return;
                } else {
                    queue.add(temp.right);
                }
            }

            if (temp.left != null) {
                if (temp.left == dNode) {
                    temp.left = null;
                    return;
                } else {
                    queue.add(temp.left);
                }
            }
        }
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        System.out.println("Before deletion:");
        tree.inorder(tree.root);
        
        tree.delete(tree.root, 3);

        System.out.println("\nAfter deletion:");
        tree.inorder(tree.root);
    }

    void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.val + " ");
            inorder(root.right);
        }
    }
}
```
##### 4.1.3 Searching
- **Details**: Searching in a binary tree involves traversing the tree to find a node with a given key.
- **Time Complexity**: O(n)
- **Java Code**:

```java
class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinaryTree {

    Node root;

    Node search(Node root, int key) {
        if (root == null || root.val == key) {
            return root;
        }

        Node res1 = search(root.left, key);
        if (res1 != null) {
            return res1;
        }

        return search(root.right, key);
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        int key = 4;
        Node result = tree.search(tree.root, key);
        if (result != null) {
            System.out.println("Node with key " + key + " found.");
        } else {
            System.out.println("Node with key " + key + " not found.");
        }
    }
}
```
##### 4.1.4 Traversal
- **Details**: Traversal refers to visiting all nodes in a specific order. Common traversals include Inorder, Preorder, and Postorder.
- **Time Complexity**: O(n)
- **Java Code**:

```java
class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinaryTree {

    Node root;

    void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.val + " ");
            inorder(root.right);
        }
    }

    void preorder(Node root) {
        if (root != null) {
            System.out.print(root.val + " ");
            preorder(root.left);
            preorder(root.right);
        }
    }

    void postorder(Node root) {
        if (root != null) {
            postorder(root.left);
            postorder(root.right);
            System.out.print(root.val + " ");
        }
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        System.out.println("Inorder traversal:");
        tree.inorder(tree.root);

        System.out.println("\nPreorder traversal:");
        tree.preorder(tree.root);

        System.out.println("\nPostorder traversal:");
        tree.postorder(tree.root);
    }
}
```

### 5. Binary Search Tree (BST)
A Binary Search Tree is a binary tree with the property that the value of each node is greater than all the values in its left subtree and less than all the values in its right subtree.

![[Pasted image 20240903164456.png]]

#### 5.1 Operations
##### 5.1.1 Insert
- **Details**: In a BST, the insertion is done by comparing the key with the value of the current node and moving to the left or right subtree accordingly until the appropriate position is found.
- **Time Complexity**: O(log n) on average, O(n) in the worst case.
- **Java Code**:

```java
class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinarySearchTree {

    Node root;

    Node insert(Node root, int key) {
        if (root == null) {
            return new Node(key);
        }

        if (key < root.val) {
            root.left = insert(root.left, key);
        } else {
            root.right = insert(root.right, key);
        }

        return root;
    }

    public static void main(String[] args) {
        BinarySearchTree bst = new BinarySearchTree();
        bst.root = bst.insert(bst.root, 50);
        bst.insert(bst.root, 30);
        bst.insert(bst.root, 20);
        bst.insert(bst.root, 40);
        bst.insert(bst.root, 70);
        bst.insert(bst.root, 60);
        bst.insert(bst.root, 80);

        System.out.println("BST created with the inserted nodes.");
    }
}
```

This Java code mirrors the functionality of the `insert_bst` Python function, constructing a Binary Search Tree by recursively inserting nodes based on their values.
##### 5.1.2 Deletion
- **Details**: Deleting a node from a BST involves three cases: the node is a leaf, the node has one child, or the node has two children.
- **Time Complexity**: O(log n) on average, O(n) in the worst case.
- **Java Code**:


```java
class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinarySearchTree {

    Node root;

    Node delete(Node root, int key) {
        if (root == null) {
            return root;
        }

        if (key < root.val) {
            root.left = delete(root.left, key);
        } else if (key > root.val) {
            root.right = delete(root.right, key);
        } else {
            if (root.left == null) {
                return root.right;
            } else if (root.right == null) {
                return root.left;
            }

            Node temp = minValueNode(root.right);
            root.val = temp.val;
            root.right = delete(root.right, temp.val);
        }

        return root;
    }

    Node minValueNode(Node node) {
        Node current = node;

        while (current.left != null) {
            current = current.left;
        }

        return current;
    }

    public static void main(String[] args) {
        BinarySearchTree bst = new BinarySearchTree();
        bst.root = bst.insert(bst.root, 50);
        bst.insert(bst.root, 30);
        bst.insert(bst.root, 20);
        bst.insert(bst.root, 40);
        bst.insert(bst.root, 70);
        bst.insert(bst.root, 60);
        bst.insert(bst.root, 80);

        System.out.println("BST created with the inserted nodes.");

        bst.delete(bst.root, 20);
        System.out.println("Node with key 20 deleted.");

        bst.delete(bst.root, 30);
        System.out.println("Node with key 30 deleted.");

        bst.delete(bst.root, 50);
        System.out.println("Node with key 50 deleted.");
    }

    Node insert(Node root, int key) {
        if (root == null) {
            return new Node(key);
        }

        if (key < root.val) {
            root.left = insert(root.left, key);
        } else {
            root.right = insert(root.right, key);
        }

        return root;
    }
}
```

##### 5.1.3 Searching
- **Details**: Searching in a BST is efficient because you can discard half of the tree at each step by following the BST property.
- **Time Complexity**: O(log n) on average, O(n) in the worst case.

```java
class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinarySearchTree {

    Node root;

    Node search(Node root, int key) {
        if (root == null || root.val == key) {
            return root;
        }

        if (key < root.val) {
            return search(root.left, key);
        }

        return search(root.right, key);
    }

    public static void main(String[] args) {
        BinarySearchTree bst = new BinarySearchTree();
        bst.root = bst.insert(bst.root, 50);
        bst.insert(bst.root, 30);
        bst.insert(bst.root, 20);
        bst.insert(bst.root, 40);
        bst.insert(bst.root, 70);
        bst.insert(bst.root, 60);
        bst.insert(bst.root, 80);

        int key = 40;
        Node result = bst.search(bst.root, key);
        if (result != null) {
            System.out.println("Node with key " + key + " found.");
        } else {
            System.out.println("Node with key " + key + " not found.");
        }
    }

    Node insert(Node root, int key) {
        if (root == null) {
            return new Node(key);
        }

        if (key < root.val) {
            root.left = insert(root.left, key);
        } else {
            root.right = insert(root.right, key);
        }

        return root;
    }
}
```

##### 5.1.4 Traversal
- **Details**: Traversal in a BST is the same as in a binary tree, but Inorder traversal will return nodes in sorted order.
- **Time Complexity**: O(n)
- Java Code

```java
class Node {
    int val;
    Node left, right;

    public Node(int key) {
        val = key;
        left = right = null;
    }
}

public class BinaryTree {

    Node root;

    void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.val + " ");
            inorder(root.right);
        }
    }

    void preorder(Node root) {
        if (root != null) {
            System.out.print(root.val + " ");
            preorder(root.left);
            preorder(root.right);
        }
    }

    void postorder(Node root) {
        if (root != null) {
            postorder(root.left);
            postorder(root.right);
            System.out.print(root.val + " ");
        }
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        System.out.println("Inorder traversal:");
        tree.inorder(tree.root);

        System.out.println("\nPreorder traversal:");
        tree.preorder(tree.root);

        System.out.println("\nPostorder traversal:");
        tree.postorder(tree.root);
    }
}
```

### 6. AVL Tree
An AVL Tree is a self-balancing binary search tree where the difference between the heights of the left and right subtrees cannot be more than one for all nodes.
![[Pasted image 20240903164545.png]]
#### 6.1 Operations

##### 6.1.1 Insert
- **Details**: Inserting in an AVL tree is similar to a BST, but after each insertion, the tree is checked for balance, and rotations are performed if necessary to maintain the AVL property.
- **Time Complexity**: O(log n)
- Java Code:

```java
class AVLNode {
    int val, height;
    AVLNode left, right;

    AVLNode(int key) {
        val = key;
        height = 1;
    }
}

public class AVLTree {

    AVLNode root;

    int height(AVLNode node) {
        if (node == null) {
            return 0;
        }
        return node.height;
    }

    int getBalance(AVLNode node) {
        if (node == null) {
            return 0;
        }
        return height(node.left) - height(node.right);
    }

    AVLNode rightRotate(AVLNode y) {
        AVLNode x = y.left;
        AVLNode T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = Math.max(height(y.left), height(y.right)) + 1;
        x.height = Math.max(height(x.left), height(x.right)) + 1;

        // Return new root
        return x;
    }

    AVLNode leftRotate(AVLNode x) {
        AVLNode y = x.right;
        AVLNode T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        // Return new root
        return y;
    }

    AVLNode insert(AVLNode node, int key) {
        if (node == null) {
            return new AVLNode(key);
        }

        if (key < node.val) {
            node.left = insert(node.left, key);
        } else if (key > node.val) {
            node.right = insert(node.right, key);
        } else {
            return node; // Duplicate keys are not allowed in AVL Tree
        }

        // Update the height of this ancestor node
        node.height = 1 + Math.max(height(node.left), height(node.right));

        // Get the balance factor of this ancestor node
        int balance = getBalance(node);

        // If the node becomes unbalanced, then perform the appropriate rotations

        // Left Left Case
        if (balance > 1 && key < node.left.val) {
            return rightRotate(node);
        }

        // Right Right Case
        if (balance < -1 && key > node.right.val) {
            return leftRotate(node);
        }

        // Left Right Case
        if (balance > 1 && key > node.left.val) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.val) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        return node;
    }

    public static void main(String[] args) {
        AVLTree tree = new AVLTree();

        tree.root = tree.insert(tree.root, 10);
        tree.root = tree.insert(tree.root, 20);
        tree.root = tree.insert(tree.root, 30);
        tree.root = tree.insert(tree.root, 40);
        tree.root = tree.insert(tree.root, 50);
        tree.root = tree.insert(tree.root, 25);

        System.out.println("AVL Tree created with the inserted nodes.");
    }
}
```

- Key Points:
- **AVLNode Class**: Represents a node in the AVL tree with attributes for the value, height, and pointers to the left and right children.
- **Height Calculation**: The height of each node is maintained and updated during insertions.
- **Balance Factor**: The difference in heights between the left and right subtrees, used to determine if the tree is balanced.
- **Rotations**: The four cases for rotations (Left-Left, Right-Right, Left-Right, and Right-Left) are handled to maintain the AVL tree properties during insertions.
##### 6.1.2 Deletion
- **Details**: Deletion in an AVL tree is similar to a BST, followed by rebalancing the tree by performing rotations
##### 6.1.3 Full code:

```java
class AVLNode {
    int val, height;
    AVLNode left, right;

    AVLNode(int key) {
        val = key;
        height = 1;
    }
}

public class AVLTree {

    AVLNode root;

    int height(AVLNode node) {
        if (node == null) {
            return 0;
        }
        return node.height;
    }

    int getBalance(AVLNode node) {
        if (node == null) {
            return 0;
        }
        return height(node.left) - height(node.right);
    }

    AVLNode rightRotate(AVLNode y) {
        AVLNode x = y.left;
        AVLNode T2 = x.right;

        x.right = y;
        y.left = T2;

        y.height = Math.max(height(y.left), height(y.right)) + 1;
        x.height = Math.max(height(x.left), height(x.right)) + 1;

        return x;
    }

    AVLNode leftRotate(AVLNode x) {
        AVLNode y = x.right;
        AVLNode T2 = y.left;

        y.left = x;
        x.right = T2;

        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        return y;
    }

    AVLNode insert(AVLNode node, int key) {
        if (node == null) {
            return new AVLNode(key);
        }

        if (key < node.val) {
            node.left = insert(node.left, key);
        } else if (key > node.val) {
            node.right = insert(node.right, key);
        } else {
            return node;
        }

        node.height = 1 + Math.max(height(node.left), height(node.right));

        int balance = getBalance(node);

        if (balance > 1 && key < node.left.val) {
            return rightRotate(node);
        }

        if (balance < -1 && key > node.right.val) {
            return leftRotate(node);
        }

        if (balance > 1 && key > node.left.val) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        if (balance < -1 && key < node.right.val) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        return node;
    }

    AVLNode minValueNode(AVLNode node) {
        AVLNode current = node;

        while (current.left != null) {
            current = current.left;
        }

        return current;
    }

    AVLNode delete(AVLNode root, int key) {
        if (root == null) {
            return root;
        }

        if (key < root.val) {
            root.left = delete(root.left, key);
        } else if (key > root.val) {
            root.right = delete(root.right, key);
        } else {
            if (root.left == null || root.right == null) {
                AVLNode temp = (root.left != null) ? root.left : root.right;

                if (temp == null) {
                    temp = root;
                    root = null;
                } else {
                    root = temp;
                }
            } else {
                AVLNode temp = minValueNode(root.right);
                root.val = temp.val;
                root.right = delete(root.right, temp.val);
            }
        }

        if (root == null) {
            return root;
        }

        root.height = Math.max(height(root.left), height(root.right)) + 1;

        int balance = getBalance(root);

        if (balance > 1 && getBalance(root.left) >= 0) {
            return rightRotate(root);
        }

        if (balance > 1 && getBalance(root.left) < 0) {
            root.left = leftRotate(root.left);
            return rightRotate(root);
        }

        if (balance < -1 && getBalance(root.right) <= 0) {
            return leftRotate(root);
        }

        if (balance < -1 && getBalance(root.right) > 0) {
            root.right = rightRotate(root.right);
            return leftRotate(root);
        }

        return root;
    }

    AVLNode search(AVLNode root, int key) {
        if (root == null || root.val == key) {
            return root;
        }

        if (key < root.val) {
            return search(root.left, key);
        }

        return search(root.right, key);
    }

    void inorder(AVLNode root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.val + " ");
            inorder(root.right);
        }
    }

    public static void main(String[] args) {
        AVLTree tree = new AVLTree();

        tree.root = tree.insert(tree.root, 10);
        tree.root = tree.insert(tree.root, 20);
        tree.root = tree.insert(tree.root, 30);
        tree.root = tree.insert(tree.root, 40);
        tree.root = tree.insert(tree.root, 50);
        tree.root = tree.insert(tree.root, 25);

        System.out.println("Inorder traversal of the AVL tree is:");
        tree.inorder(tree.root);

        tree.root = tree.delete(tree.root, 40);
        System.out.println("\nInorder traversal after deleting 40:");
        tree.inorder(tree.root);

        AVLNode result = tree.search(tree.root, 25);
        if (result != null) {
            System.out.println("\nNode 25 found in the AVL tree.");
        } else {
            System.out.println("\nNode 25 not found in the AVL tree.");
        }
    }
}
```

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

### 12. Visualization
1. http://www.btv.melezinek.cz/binary-search-tree.html
2. https://algorithm-visualizer.org/