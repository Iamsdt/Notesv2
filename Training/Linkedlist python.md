---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - leetcode
  - linkedlist
---
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
```python
def insert_at_beginning(head, data):
    new_node = Node(data)
    new_node.next = head
    return new_node  # New head of the list
```
  - **Time Complexity**: O(1).

- **At the End**:
```python
def insert_at_end(head, data):
    new_node = Node(data)
    if head is None:
        return new_node
    current = head
    while current.next:
        current = current.next
    current.next = new_node
    return head

```
  - **Time Complexity**: O(n).

- **At a Specific Position**:
```python
def insert_at_position(head, data, position):
    new_node = Node(data)
    if position == 0:
        new_node.next = head
        return new_node
    current = head
    for i in range(position - 1):
        if current is None:
            return head
        current = current.next
    new_node.next = current.next
    current.next = new_node
    return head

```
  - **Time Complexity**: O(n).

### **Deletion**:
- **From the Beginning**:
```python
def delete_from_beginning(head):
    if head is None:
        return None
    return head.next

```
  - **Time Complexity**: O(1).

- **From the End**:
```python
def delete_from_end(head):
    if head is None or head.next is None:
        return None
    current = head
    while current.next.next:
        current = current.next
    current.next = None
    return head

```
  - **Time Complexity**: O(n).

- **From a Specific Position**:
```python
def delete_from_position(head, position):
    if head is None:
        return None
    if position == 0:
        return head.next
    current = head
    for i in range(position - 1):
        if current is None:
            return head
        current = current.next
    if current.next:
        current.next = current.next.next
    return head

```
  - **Time Complexity**: O(n).

### **Traversal**:
- **Iterative Traversal**:
```python
def traverse(head):
    current = head
    while current:
        print(current.data)
        current = current.next

```
  - **Time Complexity**: O(n).

## **3. Advanced LinkedList Operations**

### **Reversing a LinkedList**:
- **Iterative Approach**:
```python
def reverse_linkedlist(head):
    prev = None
    current = head
    while current:
        temp = current.next
        current.next = prev
        prev = current
        current = temp
    return prev
```
  - **Time Complexity**: O(n).
  - **Space Complexity**: O(1).

- **Recursive Approach**:
```python
def reverse_linkedlist_recursive(head):
    if head is None or head.next is None:
        return head
    new_head = reverse_linkedlist_recursive(head.next)
    head.next.next = head
    head.next = None
    return new_head

```
  - **Time Complexity**: O(n).
  - **Space Complexity**: O(n) due to recursion stack.

### **Detecting a Cycle in a LinkedList**:
- **Floyd’s Cycle Detection Algorithm**:
```python
def detect_cycle(head):
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

```
  - **Time Complexity**: O(n).
  - **Space Complexity**: O(1).

### **Finding the Middle of a LinkedList**:
- **Two-Pointer Technique**:
```python
def find_middle(head):
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow

```
  - **Time Complexity**: O(n).

### **Merging Two Sorted LinkedLists**:
- **Merge Process**:
```python
def merge_two_sorted_lists(l1, l2):
    dummy = Node(0)
    current = dummy
    while l1 and l2:
        if l1.data < l2.data:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    current.next = l1 or l2
    return dummy.next

```
  - **Time Complexity**: O(n).

###  **Merging K Sorted Lists**:
```python
class Solution:

	def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
		if not lists:
			return None

		while len(lists) > 1:
			ans = []
			for i in range(0, len(lists), 2):
				l1 = lists[i]
				l2 = lists[i + 1] if (i + 1) < len(lists) else None
				ans.append(self.mergesorted(l1, l2))
			# update the main loop
			lists = ans

	return lists[0]

	def mergesorted(self, l1, l2):
```
**Time Complexity**: O(n*k).
### **Remove Nth Node From End of List**:
```java
def remove_nth_from_end(head, n):
    dummy = Node(0)
    dummy.next = head
    fast = slow = dummy
    for _ in range(n + 1):
        fast = fast.next
    while fast:
        fast = fast.next
        slow = slow.next
    slow.next = slow.next.next
    return dummy.next

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

