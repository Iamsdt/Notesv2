## 1. Prefix Sum

The Prefix Sum pattern addresses the problem of efficiently calculating the sum of elements within a given range (subarray) of an array, especially when you need to perform multiple such queries.  Calculating the sum of a subarray naively each time involves iterating over the elements, resulting in an O(n) time complexity for each query. Prefix Sum optimizes this to O(1) after an initial preprocessing step.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffecae672-60ea-4c0c-800e-4affcb75585b_1456x902.webp)


**Explanation:**
1. **Preprocessing:**  A new array, the "prefix sum array," is created.  The element at index `i` in this array stores the sum of all elements from the beginning of the original array up to and including index `i`.

3. **Querying:** To get the sum of a subarray from index `i` to `j` (inclusive), we use the formula: `prefix_sum[j] - prefix_sum[i-1]` (assuming `i > 0`). If `i` is 0, the sum is simply `prefix_sum[j]`.

**Java Code:**
```java
import java.util.Arrays;

class PrefixSum {

    public static int[] calculatePrefixSum(int[] nums) {
        int n = nums.length;
        int[] prefixSum = new int[n];
        prefixSum[0] = nums[0];
        for (int i = 1; i < n; i++) {
            prefixSum[i] = prefixSum[i - 1] + nums[i];
        }
        return prefixSum;
    }

    public static int rangeSum(int[] nums, int i, int j) {
        int[] prefixSum = calculatePrefixSum(nums);
        if (i == 0) {
            return prefixSum[j];
        } else {
            return prefixSum[j] - prefixSum[i - 1];
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5, 6};
        int i = 1;
        int j = 3;
        int result = rangeSum(nums, i, j); // Output: 9 (2 + 3 + 4)
        System.out.println("Sum of elements from index " + i + " to " + j + ": " + result);
    }
}
```

**When to Use the Prefix Sum Pattern:**

* **Multiple Subarray Sum Queries:** If you need to calculate the sum of subarrays multiple times on the same input array, the Prefix Sum pattern dramatically improves efficiency by reducing query time to O(1).
* **Cumulative Sums:** When you need to calculate running totals or cumulative sums of an array's elements, the prefix sum array directly provides these values.
* **Problems Involving Subarray Target Sums:** Problems that require finding subarrays with a specific sum can often be solved efficiently using variations of the prefix sum technique (e.g., using a hash map to store prefix sums). Examples include LeetCode problems like #525 (Contiguous Array) and #560 (Subarray Sum Equals K).


**Key Benefits:**
* **Improved Time Complexity:** Reduces subarray sum query time from O(n) to O(1).
* **Simplicity:** The implementation is straightforward and easy to understand.

**LeetCode Problems:**

* Range Sum Query - Immutable (LeetCode #303) (Direct application of prefix sums)
* Range Sum Query 2D - Immutable (LeetCode #304) (Extension to 2D arrays)
* Subarray Sum Equals K (LeetCode #560) (Though a hash map is also used, prefix sums are essential)
* Continuous Subarray Sum (LeetCode #523)
* Maximum Size Subarray Sum Equals k (Similar to Subarray Sum Equals K, but find the longest subarray)


## 2. Two Pointer

This pattern utilizes two pointers to traverse a linear data structure like an array or a linked list. It's particularly effective for searching pairs of elements that satisfy a given condition, especially in sorted arrays.  It can also be used in other scenarios like partitioning an array or removing duplicates.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ade4509-2283-473d-b7a2-0ea78ee0d154_1456x813.webp)

**Explanation:**

The core idea is to strategically move two pointers (usually `left` and `right`) within the data structure based on the problem's requirements. This allows efficient exploration of potential pairs or element combinations without resorting to nested loops, thereby reducing time complexity.

**Java Example**:
```java
class TwoPointer {

    public static int[] twoSum(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int currentSum = nums[left] + nums[right];
            if (currentSum == target) {
                return new int[]{left, right};
            } else if (currentSum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[]{-1, -1}; // No pair found
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 6};
        int target = 6;
        int[] result = twoSum(nums, target);
        System.out.println(Arrays.toString(result)); // Output: [1, 3]
    }

    public static int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int slow = 0;
        for (int fast = 1; fast < nums.length; fast++) {
            if (nums[fast] != nums[slow]) {
                slow++;
                nums[slow] = nums[fast];
            }
        }
        return slow + 1;
    }
}
```

**When to Use:**

* **Sorted arrays/lists:** The pattern is highly effective when the input is sorted, enabling optimized searching using the two pointers.
* **Finding pairs with specific sum/difference:**  The classic "two sum" problem and its variations are ideal use cases.
* **Removing duplicates:** When dealing with sorted arrays/lists.
* **Partitioning an array:**  Like separating elements based on a condition (e.g., Dutch National Flag problem).
* **Reversing a linked list:** Though variations may use other techniques, the two-pointer approach is commonly used for iterative list reversal.
* **Finding the middle element of a linked list:** A classic use-case to find the midpoint efficiently.


**Key Benefits:**

* **Efficiency:**  Reduces time complexity from O(n^2) (for nested loops) to O(n) in many cases.
* **Simplicity:** Often leads to concise and easy-to-understand code.
* **Space efficiency:** Typically uses constant extra space (O(1)).

**LeetCode Problems:**
* Two Sum (LeetCode #1)
* 3Sum (LeetCode #15)
* 3Sum Closest (LeetCode #16)
* Container With Most Water (LeetCode #11)
* Trapping Rain Water (LeetCode #42) (While more complex, it utilizes a form of two-pointer approach)
* Remove Duplicates from Sorted Array (LeetCode #26)
* Move Zeroes (LeetCode #283)
* Remove Element (LeetCode #27)
* Sort Colors (LeetCode #75) (Dutch National Flag Problem)
* Reverse Linked List (LeetCode #206)
* Middle of the Linked List (LeetCode #876)


# 3. Sliding Window
The Sliding Window pattern efficiently handles problems involving contiguous subarrays or substrings by maintaining a "window" of elements and sliding it across the data structure. This avoids redundant computations and often reduces time complexity.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1703991f-458b-473e-9451-87a5ac8303ec_1456x1019.webp)

**Explanation:**

Imagine a window moving across your array or string.  The window has a specific size (fixed or dynamic) and contains a subset of the elements. As the window slides, you maintain a certain state (e.g., the sum of elements within the window) and update it based on the element entering and the element leaving the window. This allows you to check various conditions (like maximum sum, longest substring, etc.) without repeatedly iterating through the entire data structure.

**Java Example:**

```Java
class SlidingWindow {
    public static int maxSumSubarray(int[] nums, int k) {
        if (nums.length < k) {
            return 0;
        }
        int maxSum = 0;
        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }
        maxSum = windowSum;
        for (int i = k; i < nums.length; i++) {
            windowSum = windowSum - nums[i - k] + nums[i];
            maxSum = Math.max(maxSum, windowSum);
        }
        return maxSum;
    }

    public static void main(String[] args) {
        int[] nums = {2, 1, 5, 1, 3, 2};
        int k = 3;
        int result = maxSumSubarray(nums, k); // Output: 9
        System.out.println("Maximum sum of a subarray of size " + k + ": " + result);
    }
}
```

**When to Use:**

* **Contiguous subarrays/substrings:**  Problems involving finding a subarray or substring with a specific property.
* **Fixed-size windows:**  Like finding the maximum sum subarray of a given size.
* **Dynamically sized windows:** Like finding the smallest subarray with a sum greater than or equal to a target value.

**Key Benefits:**
* **Efficiency:** Reduces time complexity, commonly from O(n^2) to O(n).
* **Simplicity:** Provides a clear and structured approach to solve a variety of problems.


**LeetCode Problems :**

* Maximum Sum Subarray of Size K (Similar to the example, but not a specific LeetCode problem. Variations exist)
* Minimum Size Subarray Sum (LeetCode #209)
* Longest Substring Without Repeating Characters (LeetCode #3)
* Longest Repeating Character Replacement (LeetCode #424)
* Substring with Concatenation of All Words (LeetCode #30)
* Sliding Window Maximum (LeetCode #239)
* Permutation in String (LeetCode #567)
* Find All Anagrams in a String (LeetCode #438)


## 4. Fast & Slow Pointers (Tortoise and Hare) Pattern

This pattern, also known as the Floyd's cycle-finding algorithm, is highly effective for detecting cycles (loops) in linked lists and other similar data structures.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7c5f3c5c-3762-43d7-81ab-9ec39c3a3203_1456x628.webp)

**Explanation:**

The algorithm uses two pointers, a "slow" pointer and a "fast" pointer. The slow pointer moves one step at a time, while the fast pointer moves two steps at a time.

* **Cycle present:** If there is a cycle, the fast pointer will eventually lap the slow pointer within the cycle.  They are guaranteed to meet.
* **No cycle:** If there's no cycle, the fast pointer will reach the end of the linked list (a null pointer) before the slow pointer.

**Java Example:**

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

class FastSlowPointers {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
}
```

**When to Use:**

* **Cycle detection in linked lists:** The primary use case.
* **Finding the start of a cycle:** With a slight modification, the algorithm can also determine the starting node of the cycle.
* **Cycle detection in other data structures:**  Can be adapted for cycle detection in arrays or graphs (if represented as adjacency lists).
* Middle Node of LinkedList


**Key Benefits:**
* **Efficiency:**  Detects cycles in O(n) time, where n is the number of nodes.
* **Constant space:** Uses only O(1) extra space (for the pointers).


**LeetCode Problems:**
* Linked List Cycle (LeetCode #141)
* Linked List Cycle II (LeetCode #142) (Finding the start of the cycle)
* Happy Number (LeetCode #202) (Can be modeled as a linked list cycle problem)


## 5. In-place Reversal of a Linked List

This pattern reverses a section of a linked list without using any auxiliary data structure for storing the list elements, hence the term "in-place." It involves manipulating pointers to change the direction of links between nodes.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbff7a5b8-4ed9-4265-bbbf-04ceca9808c0_1456x1137.webp)

**Explanation:**

The core idea is to use a few pointers (typically `previous`, `current`, and `next`) to traverse the list section to be reversed. Within each step of the traversal, the `next` pointer of the `current` node is redirected to point to the `previous` node, effectively reversing the link. This process is repeated until the entire sublist is reversed.

**Java Example:**

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class ReverseSublist {

    public static Node reverseSublist(Node head, int m, int n) {
        if (head == null || m == n) {
            return head;
        }

        Node dummy = new Node(0);
        dummy.next = head;
        Node prev = dummy;

        for (int i = 0; i < m - 1; i++) {
            prev = prev.next;
        }

        Node start = prev.next;
        Node current = start;
        Node nxt = null;

        for (int i = 0; i < n - m + 1; i++) {
            nxt = current.next;
            current.next = prev;
            prev = current;
            current = nxt;
        }

        start.next = current;
        Node prevStart = dummy.next;
        for (int i = 0; i < m - 2; i++) {
            prevStart = prevStart.next;
        }

        if (m == 1) {
            dummy.next = prev;
        } else {
            prevStart.next = prev;
        }

        return dummy.next;
    }

    public static Node createLinkedList(int[] arr) {
        Node head = null;
        Node tail = null;
        for (int val : arr) {
            if (head == null) {
                head = new Node(val);
                tail = head;
            } else {
                tail.next = new Node(val);
                tail = tail.next;
            }
        }
        return head;
    }

    public static void printLinkedList(Node head) {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("None");
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        Node head = createLinkedList(arr);
        int m = 2;
        int n = 4;

        System.out.println("Original Linked List:");
        printLinkedList(head);

        Node reversedHead = reverseSublist(head, m, n);

        System.out.println("Reversed sublist from " + m + " to " + n + ":");
        printLinkedList(reversedHead);


        arr = new int[]{1, 2, 3, 4, 5};
        head = createLinkedList(arr);
        m = 1;
        n = 5;

        System.out.println("\nOriginal Linked List:");
        printLinkedList(head);

        reversedHead = reverseSublist(head, m, n);

        System.out.println("Reversed sublist from " + m + " to " + n + ":");
        printLinkedList(reversedHead);


        arr = new int[]{1, 2, 3, 4, 5};
        head = createLinkedList(arr);
        m = 1;
        n = 2;

        System.out.println("\nOriginal Linked List:");
        printLinkedList(head);

        reversedHead = reverseSublist(head, m, n);

        System.out.println("Reversed sublist from " + m + " to " + n + ":");
        printLinkedList(reversedHead);
    }
}

```

**When to Use:**

* **Reversing a linked list (fully or partially):**  The most direct application.
* **Problems involving linked list manipulation:** When you need to rearrange the order of nodes within a linked list.
* **When space complexity is critical:** In-place reversal avoids the need for extra memory.

**Key Benefits:**

* **Space efficiency:**  O(1) space complexity.
* **Efficiency:** O(n) time complexity in most cases (where n is the length of the list or sublist).
* **Demonstrates good understanding of pointers:** This pattern showcases proficiency in pointer manipulation, which is often desired in technical interviews.

**LeetCode Problems:**
* Reverse Linked List (LeetCode #206)
* Reverse Linked List II (LeetCode #92)
* Palindrome Linked List (LeetCode #234) (Uses reversal of a portion of the list)
* Reorder List (LeetCode #143)  (Involves list splitting and reversal)


## 6. Top 'K' Elements Pattern

This pattern efficiently identifies the top `k` largest or smallest elements within a dataset, whether it's an array or a stream of data. Heaps are typically the most efficient data structure for this purpose, though sorting can be an alternative in specific cases.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffaf23e53-04ee-4e54-8eca-caa54e1956e7_1456x1106.webp)

**Explanation:**

The key is to maintain a heap of size `k` while iterating through the input data.  If searching for the *largest* elements, use a *min-heap* (where the smallest element among the top `k` is at the root).  Conversely, if searching for the *smallest* elements, use a *max-heap* (largest element at the root).

As you iterate, compare each element with the root of the heap.  If the current element is more "extreme" (larger for largest-k or smaller for smallest-k) than the root, replace the root with the current element and re-heapify. This ensures the heap always holds the top `k` elements encountered so far.


**Java Example (k-th largest):**

```java
import java.util.PriorityQueue;

class TopKElements {

    public static int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>(); // Min-heap for kth largest
        for (int num : nums) {
            minHeap.offer(num);
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }
        return minHeap.peek();
    }

    public static void main(String[] args) {
        int[] nums = {3, 2, 1, 5, 6, 4};
        int k = 2;
        int result = findKthLargest(nums, k); // Output: 5
        System.out.println("The " + k + "-th largest element is: " + result);
    }
}
```

**When to Use:**
* Finding the top/smallest/most frequent `k` elements.
* Working with large datasets where sorting the entire data is inefficient.
* Real-time data streams where you need to maintain the top `k` as data arrives.

**Key Benefits:**

* **Efficiency:** Insert and delete from a heap are O(log k).  Overall time complexity is typically O(n log k), where n is the data size.
* **Space efficiency:**  Heaps use O(k) space.
* **Adaptability:** Works well with streaming data.

**LeetCode Problems:**
* Kth Largest Element in an Array (LeetCode #215)
* Top K Frequent Elements (LeetCode #347)
* Find K Closest Elements (LeetCode #658)
* K Closest Points to Origin (LeetCode #973)
* Find Median from Data Stream (LeetCode #295) (Relates to maintaining a sorted subset)


## 7. Modified Binary Search Pattern

The Modified Binary Search pattern extends the classic binary search algorithm to work on arrays that are sorted but may be rotated or otherwise modified. It retains the logarithmic time complexity that makes binary search so efficient.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb209ba23-9292-4254-b70b-968d6028cc82_1456x706.webp)

**Explanation:**

The core idea is to adapt the binary search logic to account for the specific modifications in the array structure.  In a rotated sorted array, for example, one-half of the array will always be sorted, and the other half may not be. The modified binary search identifies the sorted half, checks if the target lies within that sorted half, and recursively applies the search on the appropriate section.

**Java Example (Finding an element in a rotated sorted array):**

```Java
class ModifiedBinarySearch {
    public int searchRotated(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;

            // Check if left half is sorted
            if (nums[left] <= nums[mid]) {
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else { // Right half is sorted
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1; // Not found
    }
}
```

**When to Use:**

* **Rotated sorted arrays:** The primary use case is finding elements efficiently in arrays that have been rotated.
* **Arrays with a distinct sorted portion:**  Even if not fully rotated, if a significant portion of the array is sorted, a modified binary search can be more efficient than a linear scan.
* **Finding a peak element:** In an array where elements increase up to a peak and then decrease, the modified binary search approach is used to locate the peak.
* **Searching in nearly sorted arrays:**  If an array is mostly sorted with minor deviations, a modified approach might offer advantages.

**Key Benefits:**

* **Efficiency:** Maintains the logarithmic time complexity O(log n) of standard binary search, making it very fast for large datasets.
* **Adaptability:** Extends the application of binary search to non-trivially sorted scenarios.


**LeetCode Problems :**
* Search in Rotated Sorted Array (LeetCode #33)
* Search in Rotated Sorted Array II (LeetCode #81) (Handles duplicates)
* Find Minimum in Rotated Sorted Array (LeetCode #153)
* Find Peak Element (LeetCode #162)


## 8. Backtracking Pattern

Backtracking is an algorithmic technique used to find solutions to problems that can be broken down into a sequence of choices.  It incrementally builds candidates for the solution and abandons ("backtracks") a candidate as soon as it determines that the candidate cannot possibly be completed to a valid solution.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0e6aafdd-9b51-41ef-be18-c9d899c06c3a_1456x1448.webp)

**Explanation:**
1. **Choice:**  The algorithm makes a choice from a set of possible options at each step.
2. **Constraint:** It checks if the choice satisfies the problem's constraints.
3. **Goal:** If the choice is valid and leads to a solution (or partial solution that can potentially lead to a complete solution), the algorithm continues to the next step.
4. **Backtrack:** If the choice violates a constraint or leads to a dead end, the algorithm undoes the last choice (backtracks) and tries a different option.
5. **Exploration:**  This process of making choices, checking constraints, and backtracking is repeated until all possible solution paths have been explored or a valid solution is found.


**Java Example (Generating Permutations):**

```Java
import java.util.ArrayList;
import java.util.List;

class Backtracking {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> currentPermutation = new ArrayList<>();
        boolean[] used = new boolean[nums.length]; // Track used numbers
        backtrack(nums, used, currentPermutation, result);
        return result;
    }

    private void backtrack(int[] nums, boolean[] used, List<Integer> currentPermutation, List<List<Integer>> result) {
        if (currentPermutation.size() == nums.length) {
            result.add(new ArrayList<>(currentPermutation));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (!used[i]) {
                used[i] = true;
                currentPermutation.add(nums[i]);
                backtrack(nums, used, currentPermutation, result);
                currentPermutation.remove(currentPermutation.size() - 1); // Backtrack
                used[i] = false;
            }
        }
    }
}
```

**When to Use:**

* **Combinatorial problems:** Generating permutations, combinations, subsets.
* **Constraint satisfaction problems:**  N-Queens, Sudoku, graph coloring.
* **Search problems:** Finding paths in a maze, exploring game trees.
* **Optimization problems:**  Traveling Salesperson Problem (finding the shortest route), knapsack problem.

**Key Benefits:**

* **Exhaustive search:** Systematically explores all possible solutions, ensuring that the optimal or all valid solutions are found.
* **Flexibility:**  Can handle a wide range of problems by simply modifying the constraint checks and goal conditions.

**LeetCode Problems:**
* Subsets (LeetCode #78)
* Subsets II (LeetCode #90) (Handles duplicates)
* Permutations (LeetCode #46)
* Permutations II (LeetCode #47) (Handles duplicates)
* Combinations (LeetCode #77)
* Combination Sum (LeetCode #39)
* Letter Combinations of a Phone Number (LeetCode #17)
* N-Queens (LeetCode #51)
* Sudoku Solver (LeetCode #37)
* Word Search (LeetCode #79)


## 9. Dynamic Programming (DP) Pattern

Dynamic Programming (DP) is a powerful algorithmic technique used to solve optimization problems by breaking them down into smaller overlapping subproblems and storing the results of these subproblems to avoid redundant computations.  This can drastically improve efficiency, often reducing exponential time complexity to polynomial time.

**Explanation:**

DP relies on two key properties:

1. **Overlapping Subproblems:** The problem can be broken down into smaller subproblems that are reused multiple times.
2. **Optimal Substructure:** An optimal solution to the main problem can be constructed from optimal solutions to its subproblems.

There are two main approaches to DP:

* **Top-Down (Memoization):**  Starts with the original problem and recursively breaks it down into subproblems. The results of solved subproblems are stored in a cache (usually an array or dictionary).  When a subproblem is encountered again, its cached result is retrieved, avoiding recomputation.
* **Bottom-Up (Tabulation):**  Starts by solving the smallest subproblems and iteratively builds up solutions to larger subproblems using the results of the smaller ones. The final solution is obtained by combining the solutions to the largest subproblems.

**DP Sub-Pattern: Fibonacci Numbers**

The Fibonacci sequence is a classic example of DP. Each Fibonacci number is the sum of the two preceding ones, starting from 0 and 1.

**Java Example (Fibonacci - both top-down and bottom-up):**

```java
# Top-Down (Memoization)
import java.util.HashMap;
import java.util.Map;

public class FibonacciMemoization {

    private static Map<Integer, Integer> memo = new HashMap<>();

    public static int fibMemo(int n) {
        if (memo.containsKey(n)) {
            return memo.get(n);
        }
        if (n <= 1) {
            return n;
        }
        int result = fibMemo(n - 1) + fibMemo(n - 2);
        memo.put(n, result);
        return result;
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("Fibonacci number (" + n + ") using memoization: " + fibMemo(n));
    }
}



# Bottom-Up (Tabulation)
public class FibonacciTabulation {

    public static int fibTab(int n) {
        if (n <= 1) {
            return n;
        }
        int[] fibTable = new int[n + 1];
        fibTable[0] = 0;
        fibTable[1] = 1;
        for (int i = 2; i <= n; i++) {
            fibTable[i] = fibTable[i - 1] + fibTable[i - 2];
        }
        return fibTable[n];
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("Fibonacci number (" + n + ") using tabulation: " + fibTab(n));
    }
}
```

**When to Use DP:**

* **Overlapping subproblems:** If you observe that the same subproblems are being solved repeatedly, DP is a good candidate.
* **Optimization problems:** DP is primarily used to find optimal solutions (minimum/maximum values) to problems.
* **Counting problems:**  While less common, DP can also be used to count the number of ways to achieve a certain outcome (e.g., number of ways to reach a particular cell in a grid).

**Key Benefits of DP:**

* **Efficiency:**  Avoids redundant computations by storing and reusing results, often significantly reducing time complexity.
* **Optimization:**  Guarantees finding an optimal solution (given the optimal substructure property).

**LeetCode Problems**

**1D DP:**

* Climbing Stairs (LeetCode #70)
* House Robber (LeetCode #198)
* Maximum Subarray (LeetCode #53)
* Longest Increasing Subsequence (LeetCode #300)

**2D DP:**

* Unique Paths (LeetCode #62)
* Longest Common Subsequence (LeetCode #1143)
* Edit Distance (LeetCode #72)


*Dynamic Programming (DP) Sub-Pattern: 0/1 Knapsack*

The 0/1 Knapsack problem is a classic optimization problem where you have a set of items, each with a weight and a value, and a knapsack with a maximum weight capacity. The goal is to determine the most valuable combination of items that can fit into the knapsack without exceeding its weight limit.  The "0/1" signifies that each item can either be included entirely or excluded; you cannot take a fraction of an item.

**Explanation:**

The problem is solved using dynamic programming because it exhibits both overlapping subproblems and optimal substructure.

* **Overlapping Subproblems:** When deciding whether to include an item, you need to consider the best possible combinations of previous items, leading to the same subproblems being considered multiple times.
* **Optimal Substructure:** The optimal solution for a given knapsack capacity and a set of items can be constructed from optimal solutions to subproblems with smaller capacities and fewer items.


**Java Example (Bottom-up/Tabulation Approach):**

```python
import java.util.HashMap;
import java.util.Map;

public class FibonacciMemoization {

    private static Map<Integer, Integer> memo = new HashMap<>();

    public static int fibMemo(int n) {
        if (memo.containsKey(n)) {
            return memo.get(n);
        }
        if (n <= 1) {
            return n;
        }
        int result = fibMemo(n - 1) + fibMemo(n - 2);
        memo.put(n, result);
        return result;
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("Fibonacci number (" + n + ") using memoization: " + fibMemo(n));
    }
}


public class FibonacciTabulation {

    public static int fibTab(int n) {
        if (n <= 1) {
            return n;
        }
        int[] fibTable = new int[n + 1];
        fibTable[0] = 0;
        fibTable[1] = 1;
        for (int i = 2; i <= n; i++) {
            fibTable[i] = fibTable[i - 1] + fibTable[i - 2];
        }
        return fibTable[n];
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("Fibonacci number (" + n + ") using tabulation: " + fibTab(n));
    }
}

```

**When to Use:**

* **Resource allocation with constraints:** When you have a limited resource (knapsack capacity) and need to select the best combination of items (projects, investments, etc.) that maximize value within that constraint.
* **Selection problems with binary choices:**  Where each item must be either fully selected or not selected at all.


**Key Benefits:**

* **Optimal solution:**  DP guarantees finding the most valuable combination of items.
* **Efficient for moderate input sizes:** The time complexity is polynomial (O(nW) where n is the number of items and W is the capacity), making it efficient for many practical scenarios. However, for very large capacities, it might become computationally expensive (pseudo-polynomial).


**LeetCode Problems:**
* **Partition Equal Subset Sum (LeetCode #416):** Determining if a set can be divided into two subsets with equal sum. (Very closely related to 0/1 Knapsack).
* **Target Sum (LeetCode #494):**  Finding the number of ways to assign + or - signs to numbers to reach a target sum. (Uses a similar DP approach).
* **Coin Change (LeetCode #322):** Finding the fewest number of coins that make up a given amount. (Related to unbounded knapsack).
