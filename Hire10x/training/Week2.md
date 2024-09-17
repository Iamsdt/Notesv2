### Problem 1: Calculate the Tri-Fib Sequence
1137

You are given an integer `n`. Instead of the classic Fibonacci sequence, this problem follows a modified version where each number is the sum of the previous **three** numbers. The sequence starts as follows:

- `Tri(0) = 0`
- `Tri(1) = 1`
- `Tri(2) = 1`

For any number `n ≥ 3`, the formula is:

```
Tri(n) = Tri(n-1) + Tri(n-2) + Tri(n-3)
```

Your task is to calculate the value of `Tri(n)` for a given `n`.

### Example:
1. **Input:** `n = 4`  
   **Output:** `4`
   - Explanation: The sequence is `0, 1, 1, 2, 4`.

2. **Input:** `n = 25`  
   **Output:** `1389537`

### Constraints:
- `0 ≤ n ≤ 37`
- You should use an efficient solution, ideally applying dynamic programming or memoization to avoid recalculating values unnecessarily.

```python
class Solution:
    def tribonacci(self, n: int) -> int:
        @lru_cache(None)
        def trib(n: int) -> int:
            if n == 0:
                return 0
            if n <= 2:
                return 1
            return trib(n-1) + trib(n-2) + trib(n-3)
        
        return trib(n)
```

### Problem 2: Substring Permutation Check
567

You are given two strings: `pattern` and `source`. Your task is to determine if any permutation of `pattern` exists as a contiguous substring within `source`.

In other words, can you rearrange the characters of `pattern` to form a substring of `source`? You are allowed to use each character of `pattern` exactly once, and the order of characters in the substring matters.

### Example:
1. **Input:**  
   `pattern = "abc"`  
   `source = "eidbaooo"`  
   **Output:** `True`  
   - Explanation: One possible permutation of "abc" is "bca", which appears in "eidbaooo".

2. **Input:**  
   `pattern = "ab"`  
   `source = "eidboaoo"`  
   **Output:** `False`  
   - Explanation: No permutation of "ab" is a substring of "eidboaoo".

### Constraints:
- The length of `pattern` and `source` are both between `1` and `10^4`.
- The strings consist of lowercase English letters only.

### Hints:
- Use an efficient approach to avoid recalculating for each substring. Think about how you can move through the `source` string while maintaining character counts.

---
### Problem 3: Missing Numbers in Sequence

```python
class Solution:
    # useless tricky solution
    def findDisappearedNumbers2(self, nums: List[int]) -> List[int]:
        return list(set(range(1, len(nums)+1)).difference(set(nums)))

    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        for n in nums:
            i = abs(n)-1
            nums[i] = -1 * abs(nums[i])

        res = []
        for i, n in enumerate(nums):
            if n > 0:
                res.append(i+1)
        return res
```

You are given an array `arr` of size `n`, where each element `arr[i]` is a number between `1` and `n` (inclusive). Some numbers in this range may be missing from the array, and your task is to find all the numbers that are missing.

Return a list of all numbers from `1` to `n` that do **not** appear in `arr`.

### Example:

1. **Input:**  
   `arr = [3, 1, 2, 2, 5, 3]`  
   **Output:** `[4, 6]`  
   - Explanation: The numbers 4 and 6 are missing from the array.

2. **Input:**  
   `arr = [2, 2]`  
   **Output:** `[1]`  
   - Explanation: The number 1 is missing from the array.

### Constraints:
- `n == arr.length`
- `1 ≤ n ≤ 100,000`
- `1 ≤ arr[i] ≤ n`

### Follow-up:  
Can you solve this problem in `O(n)` time complexity and without using extra space (besides the output array)?

---
### Problem 4: Maximum Path Sum in a Binary Tree
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
Given a binary tree, where each node contains an integer value, your task is to find the maximum possible sum of values along any path. A path is defined as a sequence of connected nodes, and each node can only appear once in the sequence. The path can start and end at any node, and does not need to pass through the root.

Your goal is to return the largest path sum that can be formed from any non-empty path in the tree.

### Example:

1. **Input:**  
   ```
   root = [1, 2, 3]
   ```  
   **Output:** `6`  
   - Explanation: The optimal path is `2 -> 1 -> 3` with a path sum of `2 + 1 + 3 = 6`.

2. **Input:**  
   ```
   root = [-10, 9, 20, null, null, 15, 7]
   ```  
   **Output:** `42`  
   - Explanation: The optimal path is `15 -> 20 -> 7` with a path sum of `15 + 20 + 7 = 42`.

### Constraints:
- The number of nodes in the tree is between `1` and `30,000`.
- Each node contains a value in the range `[-1000, 1000]`.
