
## **Introduction to LinkedLists**

![[Pasted image 20240830171614.png]]
### **What is a LinkedList?**
- **Definition**: A LinkedList is a linear data structure where elements, called nodes, are stored in sequence but not in contiguous memory locations. Each node contains two parts:
  - **Data**: The value or information stored in the node.
  - **Pointer (or Reference)**: A link to the next node in the sequence.

### **Types of LinkedLists**:
1. **Singly Linked List**: Each node points to the next node in the list. The last node points to `null`.
2. **Doubly Linked List**: Each node has two pointers, one pointing to the next node and one to the previous node.
3. **Circular Linked List**: In this variation, the last node points back to the first node, forming a circle.


![[Pasted image 20240830172201.png]]

### Use Cases:
- **Dynamic Memory Allocation**: Efficiently manages memory usage for lists where the size is not known upfront.
- **Insertions/Deletions**: More efficient than arrays for frequent insertions and deletions, especially at the beginning or middle of the list.


### LinkedList vs Array: When to Use Which?

### **Overview**
- **Array**: A collection of elements stored in contiguous memory locations, allowing random access to elements.
- **LinkedList**: A linear data structure where elements (nodes) are stored non-contiguously, each node pointing to the next.

### **Comparison Based on Operations**

| Operation                   | Array (Time Complexity)      | LinkedList (Time Complexity) | When to Use Which?                                                                                                      |
| --------------------------- | ---------------------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **Accessing Elements**      | O(1)                         | O(n)                         | Use arrays when you need fast, direct access to elements using an index.                                                |
| **Insertion at Beginning**  | O(n)                         | O(1)                         | Use LinkedLists when you frequently insert at the beginning.                                                            |
| **Insertion at End**        | O(1) (if space available)    | O(1) (with tail pointer)     | Both are efficient; prefer arrays if space is pre-allocated, otherwise LinkedLists.                                     |
| **Insertion at Middle**     | O(n)                         | O(n)                         | LinkedLists might be slightly more efficient in practice due to no shifting of elements, but both have O(n) complexity. |
| **Deletion from Beginning** | O(n)                         | O(1)                         | LinkedLists are better when you frequently delete from the beginning.                                                   |
| **Deletion from End**       | O(1) (if space is available) | O(n) (singly linked list)    | Use arrays when deleting from the end, but if you need to delete efficiently, consider a doubly linked list (O(1)).     |
| **Deletion from Middle**    | O(n)                         | O(n)                         | Both have similar complexity; LinkedLists avoid shifting elements but require traversal.                                |
| **Search for an Element**   | O(n)                         | O(n)                         | Neither structure excels in unsorted searches; both have linear time complexity.                                        |

---
## **2. Basic Operations on LinkedLists**

### **Node Class (Java)**
```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

### **Insertion**:
- **At the Beginning**:
```java
public static Node insertAtBeginning(Node head, int data) {
    Node newNode = new Node(data);
    newNode.next = head;
    return newNode;
}
```
  - **Time Complexity**: O(1).

- **At the End**:
```java
public static Node insertAtEnd(Node head, int data) {
    Node newNode = new Node(data);
    if (head == null) {
        return newNode;
    }
    Node current = head;
    while (current.next != null) {
        current = current.next;
    }
    current.next = newNode;
    return head;
}
```
  - **Time Complexity**: O(n).

- **At a Specific Position**:
```java
public static Node insertAtPosition(Node head, int data, int position) {
    Node newNode = new Node(data);
    if (position == 0) {
        newNode.next = head;
        return newNode;
    }
    Node current = head;
    for (int i = 0; i < position - 1 && current != null; i++) {
        current = current.next;
    }
    if (current == null) { 
        return head; // Position not found
    }
    newNode.next = current.next;
    current.next = newNode;
    return head;
}
```
  - **Time Complexity**: O(n).

### **Deletion**:
- **From the Beginning**:
```java
public static Node deleteFromBeginning(Node head) {
    if (head == null) {
        return null;
    }
    return head.next;
}
```
  - **Time Complexity**: O(1).

- **From the End**:
```java
public static Node deleteFromEnd(Node head) {
    if (head == null || head.next == null) {
        return null;
    }
    Node current = head;
    while (current.next.next != null) {
        current = current.next;
    }
    current.next = null;
    return head;
}
```
  - **Time Complexity**: O(n).

- **From a Specific Position**:
```java
public static Node deleteFromPosition(Node head, int position) {
    if (head == null) {
        return null;
    }
    if (position == 0) {
        return head.next;
    }
    Node current = head;
    for (int i = 0; i < position - 1 && current.next != null; i++) {
        current = current.next;
    }
    if (current.next == null) { 
        return head; // Position not found
    }
    current.next = current.next.next;
    return head;
}
```
  - **Time Complexity**: O(n).

### **Traversal**:
- **Iterative Traversal**:
```java
public static void traverse(Node head) {
    Node current = head;
    while (current != null) {
        System.out.print(current.data + " ");
        current = current.next;
    }
    System.out.println();
}
```
  - **Time Complexity**: O(n).

## **3. Advanced LinkedList Operations**
### **Reversing a LinkedList**:
- **Iterative Approach**:
```java
public static Node reverseLinkedList(Node head) {
    Node prev = null;
    Node current = head;
    while (current != null) {
        Node nextNode = current.next;
        current.next = prev;
        prev = current;
        current = nextNode;
    }
    return prev;
}
```
  - **Time Complexity**: O(n).
  - **Space Complexity**: O(1).

- **Recursive Approach**:
```java
public static Node reverseLinkedListRecursive(Node head) {
    if (head == null || head.next == null) {
        return head;
    }
    Node newHead = reverseLinkedListRecursive(head.next);
    head.next.next = head;
    head.next = null;
    return newHead;
}
```
  - **Time Complexity**: O(n).
  - **Space Complexity**: O(n) due to recursion stack.

### **Detecting a Cycle in a LinkedList**:
- **Floyd’s Cycle Detection Algorithm**:
```java
public static boolean detectCycle(Node head) {
    Node slow = head;
    Node fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) {
            return true;
        }
    }
    return false;
}
```
  - **Time Complexity**: O(n).
  - **Space Complexity**: O(1).

### **Finding the Middle of a LinkedList**:
- **Two-Pointer Technique**:
```java
public static Node findMiddle(Node head) {
    Node slow = head;
    Node fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```
  - **Time Complexity**: O(n).

### **Merging Two Sorted LinkedLists**:
- **Merge Process**:
```java
public static Node mergeTwoSortedLists(Node l1, Node l2) {
    Node dummy = new Node(0); 
    Node current = dummy;
    while (l1 != null && l2 != null) {
        if (l1.data < l2.data) {
            current.next = l1;
            l1 = l1.next;
        } else {
            current.next = l2;
            l2 = l2.next;
        }
        current = current.next;
    }
    current.next = (l1 != null) ? l1 : l2;
    return dummy.next; 
}
```
  - **Time Complexity**: O(n).

###  **Merging K Sorted Lists**:
```java
public static Node mergeKLists(Node[] lists) {
    if (lists == null || lists.length == 0) {
        return null;
    }

    while (lists.length > 1) {
        Node[] mergedLists = new Node[(lists.length + 1) / 2];
        for (int i = 0; i < lists.length; i += 2) {
            Node l1 = lists[i];
            Node l2 = (i + 1 < lists.length) ? lists[i + 1] : null;
            mergedLists[i / 2] = mergeTwoSortedLists(l1, l2);
        }
        lists = mergedLists;
    }
    return lists[0];
}
```
**Time Complexity**: O(n*k).
### **Remove Nth Node From End of List**:
```java
public static Node removeNthFromEnd(Node head, int n) {
    Node dummy = new Node(-1); 
    dummy.next = head;
    Node slow = dummy;
    Node fast = head;

    while (n > 0 && fast != null) {
        fast = fast.next;
        n--;
    }

    while (fast != null) {
        fast = fast.next;
        slow = slow.next;
    }

    slow.next = slow.next.next;

    return dummy.next;
}
```
**Time Complexity**: O(n).

---
## **5. Best Practices and Optimization**

### **Memory Management**:
- **Handling Memory Leaks**: Always ensure that nodes are properly deallocated, especially in languages like C++ where manual memory management is required.

### **Edge Cases**:
- **Empty Lists**: Handle operations gracefully when the list is empty.
- **Single-Node Lists**: Ensure that operations do not break when the list has only one node.
- **Even vs. Odd Length**: Some algorithms, like finding the middle, need to consider whether the list length is even or odd.

### **Use of Recursion**:
- **When to Use**: Recursion is elegant but can lead to stack overflow if the list is too long. Prefer iteration when performance is critical.

---

## **6.Practice**
### Linked List
https://leetcode.com/discuss/general-discussion/460599/blind-75-leetcode-questions

- [Reverse a Linked List](https://leetcode.com/problems/reverse-linked-list/)
- [Detect Cycle in a Linked List](https://leetcode.com/problems/linked-list-cycle/)
- [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
- [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
- [Remove Nth Node From End Of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- [Reorder List](https://leetcode.com/problems/reorder-list/)



Linked List:
Simple traversal:
don't modify head. Use temporary variable to keep tracking of current node.

Two Pointer:
1. Slow and Fast -> slow takes one step and fast takes 2 steps (find the middle point or cycle in linked list)
2. prev and current -> prev node and current node

Dummy head:
when the head is not fixed, for example you need to merge two list into one, there dummy node will be helpful. At the end, return `dummy.next` it will return actual value.

Divide and Conquer:
Divide the problem into smaller problems and solve the small problem first. Example: Merging K Sorted Lists. 