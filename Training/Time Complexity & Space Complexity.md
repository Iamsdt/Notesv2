---
Created by: Shudipto Trafder
Created time: 2024-11-11T23:32
Last edited by: Shudipto Trafder
Last edited time: 2024-11-11T23:32
tags:
  - leetcode
  - bigo
---


![[Pasted image 20241028195940.png]]

## Time and Space Complexity

Time and space complexity are crucial concepts in computer science for analyzing the efficiency of algorithms. They help us understand how the resources (time and memory) required by an algorithm scale with the input size.  Analyzing complexity allows us to compare different algorithms and choose the most efficient one for a given task.

**1. Time Complexity:**

Time complexity measures the amount of time an algorithm takes to run as a function of the input size. We typically express it using Big O notation (e.g., O(n), O(log n), O(n^2)), which describes the growth rate of the runtime in the worst-case scenario.

**Common Time Complexities:**

* **O(1) - Constant Time:** The algorithm's runtime is independent of the input size.  Example: Accessing an element in an array by index.
* **O(log n) - Logarithmic Time:** The runtime grows logarithmically with the input size. Example: Binary search.
* **O(n) - Linear Time:** The runtime grows linearly with the input size. Example: Iterating through an array.
* **O(n log n) - Linearithmic Time:**  Example: Merge sort, Quick sort (average case).
* **O(n^2) - Quadratic Time:** The runtime grows proportionally to the square of the input size.  Example: Nested loops iterating over an array.
* **O(2^n) - Exponential Time:** The runtime doubles with each increase in input size. Example: Recursive Fibonacci calculation (without memoization).
* **O(n!) - Factorial Time:** The runtime grows factorially with the input size. Example: Traveling Salesperson Problem (brute-force).


**Example (Python):**
```python
import time
import random

def constant_time(n):
    """O(1) - Constant Time"""
    return n * 2  # The operation takes the same time regardless of n

def logarithmic_time(n):
    """O(log n) - Logarithmic Time"""
    count = 0
    while n > 1:  # Halving n in each iteration
        n //= 2
        count += 1
    return count

def linear_time(n):
    """O(n) - Linear Time"""
    total = 0
    for i in range(n):
        total += i
    return total

def linearithmic_time(arr):
    """O(n log n) - Linearithmic Time (example: merge sort)"""
    # Python's built-in sorted() uses Timsort, which has O(n log n) average case complexity
    return sorted(arr)

def quadratic_time(n):
    """O(n^2) - Quadratic Time"""
    count = 0
    for i in range(n):  # Nested loops
        for j in range(n):
            count += 1
    return count



def exponential_time(n):
    """O(2^n) - Exponential Time (example: recursive Fibonacci without memoization)"""
    if n <= 1:
        return n
    return exponential_time(n - 1) + exponential_time(n - 2)



def factorial_time(n):
    """O(n!) - Factorial Time (simplified example - permutations)"""
    if n == 0:
        return 1
    else:
        return n * factorial_time(n - 1)

```

**2. Space Complexity:**

Space complexity measures the amount of memory an algorithm uses as a function of the input size.  It's also expressed using Big O notation.  We consider both auxiliary space (extra space used by the algorithm) and input space.


**Common Space Complexities:**

* **O(1) - Constant Space:**  The algorithm uses a fixed amount of memory, regardless of the input size.
* **O(log n) - Logarithmic Space:** The space used grows logarithmically with the input size.  Often related to recursive algorithms with logarithmic depth.
* **O(n) - Linear Space:** The space used grows linearly with the input size. Example: Creating a copy of an array.
* **O(n^2) - Quadratic Space:**  Example: Creating a 2D array where both dimensions are proportional to the input size.
