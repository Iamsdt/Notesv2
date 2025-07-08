## What is an Array?
- **Array**: An ordered collection of elements, identified by index.
- Fixed size (in most languages).
- Elements are stored in contiguous memory locations.
- Common operations: access by index, update, iterate, insertion, deletion.

---

## Where to Use Arrays

**Use arrays when:**
- You need fast, constant-time access to elements by index.
- The number of elements is known and does not change frequently.
- You need to store items of the same data type.
- Memory should be allocated contiguously for performance (cache friendliness).
- You want to perform bulk operations (sorting, searching, etc.) efficiently.

**Examples:**
- Storing a fixed list of grades, scores, IDs, etc.
- Implementing algorithms that require random access (binary search, quicksort, etc.).
- As the base structure for higher-level data structures (matrices, heaps, etc.).
- When working with APIs or libraries that require arrays.

---

## Where NOT to Use Arrays (and Why)

**Avoid arrays when:**
- You need to frequently insert or remove elements at arbitrary positions (not just at the end).
  - **Why?**: Arrays require shifting elements, which is O(n) time.
- The number of elements is highly dynamic or unknown in advance.
  - **Why?**: Fixed-size arrays may waste memory or run out of space; resizing is costly.
- You need to store different data types together.
  - **Why?**: Arrays are homogeneous (all elements are the same type).
- Memory usage is a concern and you want to avoid allocating large contiguous blocks.
  - **Why?**: Arrays require contiguous memory; linked structures do not.

**Better alternatives:**
- **Linked List**: For frequent insertions/deletions.
- **Dynamic Array/List (e.g., Python's list, Java's ArrayList)**: For variable-sized collections.
- **HashMap/Set**: For lookup-heavy or key-value data.
- **Stack/Queue**: For LIFO/FIFO access patterns.

---

## 1. Contains Duplicate ([LeetCode #217](https://leetcode.com/problems/contains-duplicate/))
### Problem:
Given an array of integers, determine if any value appears at least twice.

### Approach:
- Use a HashSet to track seen numbers.
- If a number is already in the set, return `True`.
- Otherwise, add it to the set and continue.
- If loop completes, return `False`.

### Code Example

#### Python
```python
def containsDuplicate(nums):
    seen = set()
    for num in nums:
        if num in seen:
            return True
        seen.add(num)
    return False
```

#### Java
```java
import java.util.HashSet;

public class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return true;
            }
            seen.add(num);
        }
        return false;
    }
}
```

#### JavaScript
```javascript
function containsDuplicate(nums) {
    const seen = new Set();
    for (let num of nums) {
        if (seen.has(num)) return true;
        seen.add(num);
    }
    return false;
}
```

- **Time Complexity**: O(n)
- **Space Complexity**: O(n)

### Approach (2):
- Use a dictionary (`di`) to keep track of elements already seen.
- For each number in the list:
    - If the number is already a key in the dictionary, return `True` (duplicate found).
    - Otherwise, add the number as a key in the dictionary.
- If the loop finishes without finding a duplicate, return `False`.

#### Python
```python
class Solution:
    def containsDuplicate(self, nums):
        di = {}
        for i in nums:
            if i in di:
                return True
            else:
                di[i] = 1
        return False
```

#### Java
```java
import java.util.HashMap;

public class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            if (map.containsKey(num)) {
                return true;
            } else {
                map.put(num, 1);
            }
        }
        return false;
    }
}
```

#### JavaScript
```javascript
function containsDuplicate(nums) {
    const map = {};
    for (let num of nums) {
        if (map[num]) {
            return true;
        } else {
            map[num] = 1;
        }
    }
    return false;
}
```

---

## 2. Two Sum ([LeetCode #1](https://leetcode.com/problems/two-sum/))
### Problem:
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to target.

### Approach:
- Use a HashMap to store number and its index.
- For each number, check if `target - num` exists in the map.
- If yes, return indices.
- If not, add current num and index to map.

### Code Example

#### Python
```python
def twoSum(nums, target):
    lookup = {}
    for i, num in enumerate(nums):
        diff = target - num
        if diff in lookup:
            return [lookup[diff], i]
        lookup[num] = i
```

#### Java
```java
import java.util.HashMap;

public class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int diff = target - nums[i];
            if (map.containsKey(diff)) {
                return new int[] { map.get(diff), i };
            }
            map.put(nums[i], i);
        }
        return new int[0];
    }
}
```

#### JavaScript
```javascript
function twoSum(nums, target) {
    const map = {};
    for (let i = 0; i < nums.length; i++) {
        let diff = target - nums[i];
        if (map.hasOwnProperty(diff)) {
            return [map[diff], i];
        }
        map[nums[i]] = i;
    }
}
```

- **Time Complexity**: O(n)
- **Space Complexity**: O(n)

#### Similar Problem:
- **Two Sum II – Input Array Is Sorted** ([LeetCode #167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/))

---

## 3. Best Time to Buy and Sell Stock ([LeetCode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/))
### Problem:
Given an array where the ith element is the price of a stock on day i, find the max profit you can achieve by buying and selling once.

### Approach:
- Track the minimum price seen so far while iterating through the list.
- For each price, calculate the profit if sold at that point and update the maximum profit if it is higher than the current maximum.
- If a new lower price is found, update the minimum price accordingly.

### Code Example

#### Python
```python
def maxProfit(prices):
    profit = 0
    invest = prices[0]
    for i in range(1, len(prices)):
        if prices[i] < invest:
            invest = prices[i]
        else:
            profit = max(prices[i] - invest, profit)
    return profit
```

#### Java
```java
public class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        int invest = prices[0];
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] < invest) {
                invest = prices[i];
            } else {
                profit = Math.max(prices[i] - invest, profit);
            }
        }
        return profit;
    }
}
```

#### JavaScript
```javascript
function maxProfit(prices) {
    let profit = 0;
    let invest = prices[0];
    for (let i = 1; i < prices.length; i++) {
        if (prices[i] < invest) {
            invest = prices[i];
        } else {
            profit = Math.max(prices[i] - invest, profit);
        }
    }
    return profit;
}
```

- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

#### Similar Problem:
**Best Time to Buy and Sell Stock II** ([LeetCode #122](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/))

---

## Key Takeaways
- Arrays are fundamental data structures.
- HashSet/HashMap are powerful for solving many array problems efficiently.
- Always consider edge cases (empty array, one element, etc.).
- Choose arrays when you need fast indexing and predictable memory layout.
- Use other data structures when your usage pattern doesn’t fit arrays.