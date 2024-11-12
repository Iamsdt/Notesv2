---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - leetcode
---


# Linked List:
Simple traversal:
don't modify head. Use temporary variable to keep tracking of current node.

Two Pointer:
1. Slow and Fast -> slow takes one step and fast takes 2 steps (find the middle point or cycle in linked list)
2. prev and current -> prev node and current node

Dummy head:
when the head is not fixed, for example you need to merge two list into one, there dummy node will be helpful. At the end, return `dummy.next` it will return actual value.

Divide and Conquer:
Divide the problem into smaller problems and solve the small problem first. Example: Merging K Sorted Lists. 


# Tree:
DFS
BFS
Use recursion, code will be easy compare to iterative solution


# Array:
1. brute force
2. two pointers
3. IF array is sorted always think about binary search
4. Use dictionary/map to cache computed result
5. Sorting algo: 
	1. Bubble sort
	2. Merge sort
	3. Selection sort
6. Searching Algo:
	1. binary search
	2. linear search