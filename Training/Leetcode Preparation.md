---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - leetcode
---
# Problem 1: Make Profit Everyday

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`th day. 

You are allowed to complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times). However, **you must sell the stock before you buy it again**.

Return the maximum profit you can achieve from these transactions. If no profit can be achieved, return `0`.

#### Constraints:
- You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
- The number of days will be between `1` and `10^5`.
- Prices for each day will be between `0` and `10^4`.

#### Examples:

**Example 1:**
- Input: `prices = [7,1,5,3,6,4]`
- Output: `7`
- Explanation: 
  - Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5 - 1 = 4.
  - Buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6 - 3 = 3.
  - Total profit is 4 + 3 = 7.

**Example 2:**
- Input: `prices = [1,2,3,4,5]`
- Output: `4`
- Explanation:
  - Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5 - 1 = 4.
  - Total profit is 4, as prices are increasing continuously.

**Example 3:**
- Input: `prices = [7,6,4,3,1]`
- Output: `0`
- Explanation:
  - In this case, no transactions are done as the prices are decreasing, so the max profit is 0.

**Example 4:**
- Input: `prices = [2,4,1,7,6,9,3]`
- Output: `10`
- Explanation:
  - Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4 - 2 = 2.
  - Buy on day 3 (price = 1) and sell on day 6 (price = 9), profit = 9 - 1 = 8.
  - Total profit is 2 + 8 = 10.

---

# Problem 2: Remove Duplicates from Sorted Linked List

Given the `head` of a **sorted** linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

#### Constraints:
- The number of nodes in the list is in the range `[0, 300]`.
- `-100 <= Node.val <= 100`
- The list is sorted in non-decreasing order.

#### Examples:

**Example 1:**
- Input: `head = [1,1,2]`
- Output: `[1,2]`

**Example 2:**
- Input: `head = [1,1,2,3,3]`
- Output: `[1,2,3]`

**Example 3:**
- Input: `head = [0, 0, 1, 2, 2, 3]`
- Output: `[0,1,2,3]`

---
# Problem 3: Path Sum
Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a **root-to-leaf** path such that adding up all the values along the path equals `targetSum`.

A **leaf** is a node with no children.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg)

**Input:** root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
**Output:** true
**Explanation:** The root-to-leaf path with the target sum is shown.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

**Input:** root = [1,2,3], targetSum = 5
**Output:** false
**Explanation:** There two root-to-leaf paths in the tree:
(1 --> 2): The sum is 3.
(1 --> 3): The sum is 4.
There is no root-to-leaf path with sum = 5.

**Example 3:**

**Input:** root = [], targetSum = 0
**Output:** false
**Explanation:** Since the tree is empty, there are no root-to-leaf paths.

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`

---

# Problem 4: Remove Nth Node From End of List
Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2
**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1
**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1
**Output:** [1]

**Constraints:**

- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

---
# Problem 5: Find Duplicate Words in a String

**Description:**
Given a string, write a function to identify and print the duplicate words in the string. The comparison should be case-insensitive, meaning that "Word" and "word" are treated as the same word. The function should print each duplicate word only once.

**Examples:**

Example 1:
```
Input: "Big black bug bit a big black dog on his big black nose"
Output:
big
black
```

Example 2:
```
Input: "The cat chased the rat and the bat"
Output:
the
```

Example 3:
```
Input: "Hello world"
Output:
(No duplicates)
```

Example 4:
```
Input: "Red red Red BLUE blue"
Output:
red
blue
```

**Constraints:**
- The string can contain uppercase and lowercase letters.
- Words are separated by spaces.
- There are no punctuation marks in the string. 

---

# Problem 6: Move All Zeroes to End of Array

**Description:**
Given an array of integers, write a function to move all the zeroes to the end of the array, while maintaining the relative order of the non-zero elements. You must do this in-place without using extra space for another array.

**Examples:**

Example 1:
```
Input: [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]
```

Example 2:
```
Input: [1, 2, 0, 0, 4, 3]
Output: [1, 2, 4, 3, 0, 0]
```

Example 3:
```
Input: [0, 0, 0, 0]
Output: [0, 0, 0, 0]
```

Example 4:
```
Input: [1, 2, 3, 4]
Output: [1, 2, 3, 4]
```

**Constraints:**
- The array can contain any integer, including negative numbers and zero.
- The input array may have one or more zeroes.
- The function should run in O(n) time.

---
# Questions:
1. Can you tell me the difference between JVM, JRE, and JDK?
2. How does garbage collection work in Java?
3. What is JIT (Just-In-Time) compilation