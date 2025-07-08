## Time and Space Complexity

Time and space complexity are essential for analyzing the efficiency of algorithms. They describe how an algorithm's resource usage (time and memory) grows with input size, helping us compare and choose the best solution for a problem.

---
### Big O Notation Basics
Big O notation is a mathematical way to describe the upper bound of an algorithm's growth rate. It expresses how the runtime or space requirements grow as the input size increases, focusing on the dominant term and ignoring constants and lower-order terms.

**Example:**  
If an algorithm takes `3n^2 + 2n + 7` steps for input size `n`, its Big O is **O(n²)** because, as `n` grows, the `n²` term dominates.

---

### 1. Time Complexity

Time complexity measures how the runtime of an algorithm increases as the input size grows. It's usually expressed in Big O notation.

**O(1) – Constant Time**  
The algorithm's runtime does not depend on input size.

#### Python
```python
def get_first(arr):
    return arr[0]
```
#### Java
```java
int getFirst(int[] arr) {
    return arr[0];
}
```
#### JavaScript
```javascript
function getFirst(arr) {
    return arr[0];
}
```

---

**O(log n) – Logarithmic Time**  
The runtime grows logarithmically, often by halving the input each step (e.g., binary search).

#### Python
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
#### Java
```java
int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```
#### JavaScript
```javascript
function binarySearch(arr, target) {
    let left = 0, right = arr.length - 1;
    while (left <= right) {
        let mid = Math.floor((left + right) / 2);
        if (arr[mid] === target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

---

**O(n) – Linear Time**  
The runtime grows directly with input size.

#### Python
```python
def sum_all(arr):
    total = 0
    for x in arr:
        total += x
    return total
```
#### Java
```java
int sumAll(int[] arr) {
    int total = 0;
    for (int x : arr) total += x;
    return total;
}
```
#### JavaScript
```javascript
function sumAll(arr) {
    let total = 0;
    for (let x of arr) total += x;
    return total;
}
```

---

**O(n log n) – Linearithmic Time**  
Common in efficient sorting algorithms like merge sort.

#### Python
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
#### Java
```java
int[] mergeSort(int[] arr) {
    if (arr.length <= 1) return arr;
    int mid = arr.length / 2;
    int[] left = Arrays.copyOfRange(arr, 0, mid);
    int[] right = Arrays.copyOfRange(arr, mid, arr.length);
    return merge(mergeSort(left), mergeSort(right));
}

int[] merge(int[] left, int[] right) {
    int[] result = new int[left.length + right.length];
    int i = 0, j = 0, k = 0;
    while (i < left.length && j < right.length) {
        if (left[i] < right[j]) result[k++] = left[i++];
        else result[k++] = right[j++];
    }
    while (i < left.length) result[k++] = left[i++];
    while (j < right.length) result[k++] = right[j++];
    return result;
}
```
#### JavaScript
```javascript
function mergeSort(arr) {
    if (arr.length <= 1) return arr;
    let mid = Math.floor(arr.length / 2);
    let left = mergeSort(arr.slice(0, mid));
    let right = mergeSort(arr.slice(mid));
    return merge(left, right);
}

function merge(left, right) {
    let result = [];
    let i = 0, j = 0;
    while (i < left.length && j < right.length) {
        if (left[i] < right[j]) result.push(left[i++]);
        else result.push(right[j++]);
    }
    return result.concat(left.slice(i)).concat(right.slice(j));
}
```

---

**O(n²) – Quadratic Time**  
Nested loops over the input, e.g., all pairs.

#### Python
```python
def all_pairs(arr):
    for i in arr:
        for j in arr:
            print(i, j)
```
#### Java
```java
void allPairs(int[] arr) {
    for (int i : arr) {
        for (int j : arr) {
            System.out.println(i + ", " + j);
        }
    }
}
```
#### JavaScript
```javascript
function allPairs(arr) {
    for (let i of arr) {
        for (let j of arr) {
            console.log(i, j);
        }
    }
}
```

---

**O(2ⁿ) – Exponential Time**  
The runtime doubles with each increase in input size (e.g., naive recursion).

#### Python
```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```
#### Java
```java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```
#### JavaScript
```javascript
function fib(n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

---

**O(n!) – Factorial Time**  
All possible permutations, grows extremely fast.

#### Python
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
#### Java
```java
List<List<Integer>> permute(List<Integer> arr) {
    if (arr.size() <= 1) return Arrays.asList(new ArrayList<>(arr));
    List<List<Integer>> result = new ArrayList<>();
    for (int i = 0; i < arr.size(); i++) {
        List<Integer> rest = new ArrayList<>(arr);
        Integer curr = rest.remove(i);
        for (List<Integer> p : permute(rest)) {
            List<Integer> temp = new ArrayList<>();
            temp.add(curr);
            temp.addAll(p);
            result.add(temp);
        }
    }
    return result;
}
```
#### JavaScript
```javascript
function permute(arr) {
    if (arr.length <= 1) return [arr];
    let result = [];
    for (let i = 0; i < arr.length; i++) {
        let rest = arr.slice(0, i).concat(arr.slice(i + 1));
        for (let p of permute(rest)) {
            result.push([arr[i]].concat(p));
        }
    }
    return result;
}
```

---

Visualize:  
![[Pasted image 20241028195940.png]]

---

### 2. Space Complexity

Space complexity measures how much extra memory an algorithm uses as input size grows.

**O(1) – Constant Space**  
Uses a fixed amount of memory regardless of input size.

#### Python
```python
def sum_in_place(arr):
    total = 0
    for x in arr:
        total += x
    return total
```
#### Java
```java
int sumInPlace(int[] arr) {
    int total = 0;
    for (int x : arr) total += x;
    return total;
}
```
#### JavaScript
```javascript
function sumInPlace(arr) {
    let total = 0;
    for (let x of arr) total += x;
    return total;
}
```

---

**O(log n) – Logarithmic Space**  
Memory grows logarithmically, often due to recursion stack (e.g., binary search).

#### Python
```python
def log_space_recursion(n):
    if n <= 1:
        return 1
    return log_space_recursion(n//2) + 1
```
#### Java
```java
int logSpaceRecursion(int n) {
    if (n <= 1) return 1;
    return logSpaceRecursion(n / 2) + 1;
}
```
#### JavaScript
```javascript
function logSpaceRecursion(n) {
    if (n <= 1) return 1;
    return logSpaceRecursion(Math.floor(n / 2)) + 1;
}
```

---

**O(n) – Linear Space**  
Memory grows directly with input size.

#### Python
```python
def copy_array(arr):
    return arr[:]
```
#### Java
```java
int[] copyArray(int[] arr) {
    return Arrays.copyOf(arr, arr.length);
}
```
#### JavaScript
```javascript
function copyArray(arr) {
    return arr.slice();
}
```

---

**O(n²) – Quadratic Space**  
Memory grows with the square of input size, e.g., 2D arrays.

#### Python
```python
def create_matrix(n):
    return [[0]*n for _ in range(n)]
```
#### Java
```java
int[][] createMatrix(int n) {
    int[][] matrix = new int[n][n];
    for (int i = 0; i < n; i++) {
        Arrays.fill(matrix[i], 0);
    }
    return matrix;
}
```
#### JavaScript
```javascript
function createMatrix(n) {
    return Array.from({length: n}, () => Array(n).fill(0));
}
```

---

**Summary:**  
- **Time complexity** tells you how fast your code runs as input grows.
- **Big O notation** is used to express both, focusing on the dominant growth term.
- **Space complexity** tells you how much extra memory your code uses as input grows.
- Aim for lower complexity for better performance and scalability.