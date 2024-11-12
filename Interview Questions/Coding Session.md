---
Created by: Shudipto Trafder
Created time: 2023-12-11T23:56
Last edited by: Shudipto Trafder
Last edited time: 2023-12-12T16:20
tags:
  - coding
  - interview
---
1. Sorted Two sum (medium) 167

**Problem Description:**  
You are given a sorted array of integers, where each element is unique. Your task is to find two numbers in the array that add up to a given target. The array is 1-indexed, meaning the indices start from 1. Return the indices of the two numbers as a 2-element array. The solution should use only constant extra space, and there is exactly one solution in the given array.  

**Input:**

- A sorted array of unique integers (non-decreasing order).
- A target sum to find.

**Output:**

- An array containing two indices (1-indexed) representing the positions of the two numbers in the array, such that the numbers at those positions add up to the target.

**Example:**

```Plain
Input: numbers = [2, 7, 11, 15], target = 9
Output: [1, 2]
Explanation: The numbers at positions 1 and 2 (2 and 7) add up to the target 9.
```

  

Solution:

1. Binary Search
2. Two sum

```JavaScript
from typing import List
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        p, n = 0, len(numbers) -1

        while p < n:
            v = numbers[p]  + numbers[n]
            if v == target:
                return p+1, n+1

            if v < target:
                 p += 1
            else:
                n -= 1
```

  

1. Reorder Linkedin List (medium) 143

**Problem Description:**  
Given the head of a singly linked list  

`L0 → L1 → … → Ln - 1 → Ln`

reorganize the list in a way such that the reordered list follows the pattern:

```Plain
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
```

You are not allowed to modify the values within the nodes. Only the connections between nodes can be changed.

**Input:**

- The head of a singly linked list.

**Output:**

- The head of the reordered linked list.

**Example:**

```Plain
Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 1 -> 5 -> 2 -> 4 -> 3
Explanation: The reordered list follows the specified pattern.
```

**Note:**

- The length of the linked list is always even.
- The solution should be in place and use only constant extra space.

  

```Python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        slow, fast = head, head.next

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # Here slow is the second half
        second = slow.next
        prev = slow.next = None
        while second:
            t = second.next
            second.next = prev
            prev = second
            second = t

        # here prev is the reversed list
        first, second = head, prev
        while second:
            t1, t2 = first.next, second.next
            first.next = second
            second.next = t1
            first, second = t1, t2
```

1. Invert Binary Tree (easy) 226

Given the `root` of a binary tree, invert the tree, and return _its root_.

```JavaScript
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

import collections

class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if root == None:
            return None
        
        root.left, root.right = root.right, root.left
        
        self.invertTree(root.left)
        self.invertTree(root.right)
        
        return root
```

1. Merge Two sorted arrays (easy) 88

**Scenario:**  
You are a librarian tasked with organizing two separate shelves of books, each sorted in ascending order based on their publication dates. The shelves, represented by linked lists, are named  
`list1` and `list2`. Your mission is to merge these two collections into a single, well-organized shelf.

**Problem Description:**  
Given the heads of the two sorted linked lists (  
`list1` and `list2`), your goal is to create a unified and sorted collection of books. This involves merging the nodes of the two original lists to form a single, sorted linked list that encompasses all the books from both shelves.

**Input:**

- The head nodes of two sorted linked lists, `list1` and `list2`, where each node represents a book on the respective shelves.

**Output:**

- The head of the merged sorted linked list, which serves as the organized shelf containing all the books in a sorted order.

**Visual Representation:**  
Imagine two bookshelves with books arranged in ascending order based on their publication dates. Your task is to merge these shelves into a single, coherent bookshelf while maintaining the sorted order. The resulting bookshelf, represented by a linked list, should have all the books from both shelves in a seamlessly organized manner.  

**Example:**  
Suppose  
`list1` represents the first bookshelf with books [2000, 2005, 2010], and `list2` represents the second bookshelf with books [2002, 2008, 2012]. The merged bookshelf (sorted linked list) should look like [2000, 2002, 2005, 2008, 2010, 2012].

**Note:**

- The books are organized in ascending order based on their publication dates.
- The solution should efficiently merge the two bookshelves while maintaining the sorted order.
- The output is the head of the merged sorted linked list, representing the organized bookshelf.

**Example:**

```Plain
Input: list1 = 1 -> 2 -> 4, list2 = 1 -> 3 -> 4
Output: 1 -> 1 -> 2 -> 3 -> 4 -> 4
Explanation: The merged list is sorted in ascending order.
```

**Note:**

- The input linked lists are guaranteed to be sorted in ascending order.
- The solution should be in-place and use only constant extra space.

  

```JavaScript
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        current = dummy

        while list1 and list2:
            if list1.val <= list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next

            current = current.next

        if list1:
            current.next = list1

        elif list2:
            current.next = list2
        
        return dummy.next
```

  

1. Stock Trading (easy) 121

**Problem Description:**  
You are an aspiring stock trader looking to maximize your profit through strategic buying and selling of a particular stock. The stock prices are represented in an array,  
`prices`, where `prices[i]` is the price of the stock on the `i`-th day.

Your goal is to find the best opportunity to make a profitable transaction by buying one share of the stock on a specific day and selling it on a different day in the future.

Return the maximum profit you can achieve from this transaction. If there is no opportunity to make a profit, return 0.

**Scenario:**  
Imagine you have been closely monitoring the stock market for a certain stock. Each element in the array  
`prices` corresponds to the closing price of the stock on a particular day. Your task is to analyze this historical data and determine the maximum profit you could have earned by strategically buying and selling one share of the stock.

**Input:**

- An array `prices` where `prices[i]` represents the price of the stock on the `i`th day.

**Output:**

- The maximum profit achievable from a single profitable transaction. If no profit can be made, return 0.

**Example:**

```Plain
Input: prices = [7, 1, 5, 3, 6, 4]
Output: 5
Explanation: On the second day, you could have bought the stock at a price of 1 and sold it on the fifth day at a price of 6, achieving a profit of 6 - 1 = 5.
```

**Note:**

- The profit is calculated as the selling price minus the buying price.
- If there is no opportunity to make a profit, return 0.

  

```JavaScript
from typing import List


class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        invest = prices[0]
        for i in range(1, len(prices)):
            if prices[i] < invest:
                invest = prices[i]
            else:
                profit = max(prices[i] - invest, profit)

        return profit
```

  

1. Group Anagram (medium)

**Scenario:**  
Imagine you are organizing a collection of words, and you want to group words that are actually anagrams of each other. Anagrams are words or phrases that can be created by rearranging the letters of another word or phrase, using all the original letters exactly once. Your task is to create groups of these anagrams from a given array of words.  

**The Anagram Grouping Task:**  
You are provided with an array of strings, where each string represents a word. Your goal is to group these words based on whether they are anagrams of each other. Two words are considered anagrams if they can be formed by rearranging the same set of letters.  

**Example:**  
Suppose you have the array  
`strs = ["eat","tea","tan","ate","nat","bat"]`. Your job is to group these words into anagrams. In this case, the expected output is `[["bat"],["nat","tan"],["ate","eat","tea"]]`. The words "bat," "tan," and "nat" are anagrams, as well as "ate," "eat," and "tea."

**Additional Examples:**

- If the input is `strs = [""]`, the output should be `[[""]]` because there's only one word, and it's considered an anagram of itself.
- If the input is `strs = ["a"]`, the output should be `[["a"]]` since there's only one word in the array.

**Your Role as a Candidate:**  
As a candidate, your task is to come up with an efficient algorithm to group these anagrams and provide the solution as a nested array. Keep in mind that the order of the output doesn't matter; you can return the answer in any order.  

  

```JavaScript
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:        
        # update
        di = collections.defaultdict(list)
        
        for i in strs:
            ana = tuple(sorted(i))
            if ana in di:
                di[ana] = [i] + di[ana]
            else:
                di[ana] = [i]
                
        return di.values()
```

  

  

1. Longest Consecutive Sequence (medium) 127

**Problem Description:**  
Given an unsorted array of integers  
`nums`, your task is to find the length of the longest consecutive elements sequence. The goal is to return the length of the longest sequence of consecutive integers in the array.

**Input:**

- An unsorted array of integers, `nums`.

**Output:**

- The length of the longest consecutive elements sequence.

**Example 1:**

```Plain
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore, its length is 4.
```

**Example 2:**

```Plain
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

**Note:**

- You need to design an algorithm that runs in O(n) time complexity. This means that the efficiency of your solution should be linear with respect to the size of the input array `nums`.

  

```JavaScript
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        data = set(nums)
        res = 0
        for i in nums:
            if (i - 1) not in data:
                length = 1
                while (i + length) in data:
                    length += 1
                res = max(res, length)

        return res
```

  

1. Top K Frequent Elements (medium) 347

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

```Plain
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```Plain
Input: nums = [1], k = 1
Output: [1]
```

```JavaScript
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # let's use bucket sorts
        # but use the index as values
        di = Counter(nums)
        freq = [[] for i in range(len(nums)+1)]

        for key, value in di.items():
            freq[value].append(key)

        res = []
        for i in range(len(freq)-1, 0, -1):
            res += freq[i]
            if len(res) >= k:
                return res

        return res
```

  

1. Maximum Depth OF binary Tree (easy) 104

Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

[![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

```Plain
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

**Example 2:**

```Plain
Input: root = [1,null,2]
Output: 2
```

  

Solution:

```JavaScript
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
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

  

1. Climb Stair (easy) 70

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

```Plain
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```Plain
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

  

```JavaScript
class Solution:
    def climbStairs(self, n: int) -> int:
        one, two = 1, 1
        for i in range(n - 1):
            one, two = one + two, one

        return one
```

  

  

Some pandas problem:

1. Rank Score:[https://leetcode.com/problems/rank-scores/description/](https://leetcode.com/problems/rank-scores/description/)
2. Count Salary Categories: [https://leetcode.com/problems/count-salary-categories/description/](https://leetcode.com/problems/count-salary-categories/description/)
3. Second Highest Salary: [https://leetcode.com/problems/second-highest-salary/](https://leetcode.com/problems/second-highest-salary/)