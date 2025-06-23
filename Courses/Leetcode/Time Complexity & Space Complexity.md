## Time and Space Complexity

Time and space complexity are essential for analyzing the efficiency of algorithms. They describe how an algorithm's resource usage (time and memory) grows with input size, helping us compare and choose the best solution for a problem.

---

### 1. Time Complexity

Time complexity measures how the runtime of an algorithm increases as the input size grows. It's usually expressed in Big O notation.

**O(1) – Constant Time**  
The algorithm's runtime does not depend on input size.
```python
def get_first(arr):
    return arr[0]
```

**O(log n) – Logarithmic Time**  
The runtime grows logarithmically, often by halving the input each step (e.g., binary search).
```python
def binary_search(arr, target):
    left, right = 0, len(arr)-1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**O(n) – Linear Time**  
The runtime grows directly with input size.
```python
def sum_all(arr):
    total = 0
    for x in arr:
        total += x
    return total
```

**O(n log n) – Linearithmic Time**  
Common in efficient sorting algorithms like merge sort.
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

**O(n²) – Quadratic Time**  
Nested loops over the input, e.g., all pairs.
```python
def all_pairs(arr):
    for i in arr:
        for j in arr:
            print(i, j)
```

**O(2ⁿ) – Exponential Time**  
The runtime doubles with each increase in input size (e.g., naive recursion).
```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

**O(n!) – Factorial Time**  
All possible permutations, grows extremely fast.
```python
def permute(arr):
    if len(arr) <= 1:
        return [arr]
    result = []
    for i in range(len(arr)):
        rest = arr[:i] + arr[i+1:]
        for p in permute(rest):
            result.append([arr[i]] + p)
    return result
```


Visualize:
![[Pasted image 20241028195940.png]]

---

### 2. Space Complexity

Space complexity measures how much extra memory an algorithm uses as input size grows.

**O(1) – Constant Space**  
Uses a fixed amount of memory regardless of input size.
```python
def sum_in_place(arr):
    total = 0
    for x in arr:
        total += x
    return total
```

**O(log n) – Logarithmic Space**  
Memory grows logarithmically, often due to recursion stack (e.g., binary search).
```python
def log_space_recursion(n):
    if n <= 1:
        return 1
    return log_space_recursion(n//2) + 1
```

**O(n) – Linear Space**  
Memory grows directly with input size.
```python
def copy_array(arr):
    return arr[:]
```

**O(n²) – Quadratic Space**  
Memory grows with the square of input size, e.g., 2D arrays.
```python
def create_matrix(n):
    return [[0]*n for _ in range(n)]
```

---

**Summary:**  
- **Time complexity** tells you how fast your code runs as input grows.
- **Space complexity** tells you how much extra memory your code uses as input grows.
- Aim for lower complexity for better performance and scalability.
