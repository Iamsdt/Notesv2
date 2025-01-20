## Key Concept
The solution uses a monotonic stack to find the contribution of each element when it acts as both a maximum and minimum in different subarrays. Instead of checking each subarray individually, we calculate how many subarrays each element contributes to as a maximum or minimum.

## Data Structures Used
1. `stack`: Used to maintain indices in monotonic order
2. Four arrays to store boundaries:
   - `next_smaller[]`: Next smaller element's index
   - `prev_smaller[]`: Previous smaller element's index
   - `next_greater[]`: Next greater element's index
   - `prev_greater[]`: Previous greater element's index

## Step-by-Step Breakdown

### 1. Initialization
```python
n = len(nums)
stack = []
next_smaller = [n] * n    # Default to n (out of bounds)
prev_smaller = [-1] * n   # Default to -1 (out of bounds)
```
- We initialize arrays with boundary values:
  - `n` indicates no smaller/greater element exists to the right
  - `-1` indicates no smaller/greater element exists to the left

### 2. Finding Next Smaller Elements
```python
for i in range(n):
    while stack and nums[stack[-1]] > nums[i]:
        next_smaller[stack.pop()] = i
    stack.append(i)
```
Example with nums = [4, 2, 1, 3]:
1. i=0: stack=[0] ([4])
2. i=1: 2<4, so next_smaller[0]=1, stack=[1] ([2])
3. i=2: 1<2, so next_smaller[1]=2, stack=[2] ([1])
4. i=3: 3>1, stack=[2,3] ([1,3])
Result: next_smaller = [1, 2, n, n]

### 3. Finding Previous Smaller Elements
```python
for i in range(n-1, -1, -1):
    while stack and nums[stack[-1]] >= nums[i]:
        prev_smaller[stack.pop()] = i
    stack.append(i)
```
Similar process but scanning from right to left and using >= for strict comparison.

### 4. Finding Next and Previous Greater Elements
```python
next_greater = [n] * n
prev_greater = [-1] * n
```
Similar process as smaller elements but with reversed comparison operators:
- For next_greater: nums[stack[-1]] < nums[i]
- For prev_greater: nums[stack[-1]] <= nums[i]

### 5. Final Calculation
```python
for i in range(n):
    max_contribution = nums[i] * (i - prev_greater[i]) * (next_greater[i] - i)
    min_contribution = nums[i] * (i - prev_smaller[i]) * (next_smaller[i] - i)
    total += max_contribution - min_contribution
```

#### Understanding the Contribution Formula
For element at index i:
1. `(i - prev_greater[i])`: Number of elements to the left that can form subarrays where current element is maximum
2. `(next_greater[i] - i)`: Number of elements to the right that can form subarrays where current element is maximum
3. Multiplying these gives total number of subarrays where current element is maximum
4. Same logic applies for minimum contribution

Example:
For array [3,1,2,4]:
- For element 2:
  - prev_greater = 0 (3 is greater)
  - next_greater = 3 (4 is greater)
  - prev_smaller = 1 (1 is smaller)
  - next_smaller = n (no smaller element ahead)
  - max_contribution = 2 * (2-0) * (3-2) = 4
  - min_contribution = 2 * (2-1) * (4-2) = 8
  - contribution = 4 - 8 = -4

## Time and Space Complexity
- Time Complexity: O(n) - Each element is pushed and popped at most once for each of the four passes
- Space Complexity: O(n) - For the stack and the four arrays storing boundaries

## Key Insights
1. Using monotonic stack helps find next/previous smaller/greater elements efficiently
2. The contribution formula cleverly counts subarrays without generating them
3. The final result is the difference between maximum and minimum contributions
4. Boundary handling with n and -1 simplifies edge cases


## Full Code

```python
class Solution:
    def subArrayRanges(self, nums: List[int]) -> int:
        n = len(nums)
        # Initialize stacks for next smaller and previous smaller elements
        stack = []
        # Arrays to store indices of next and previous smaller elements
        next_smaller = [n] * n
        prev_smaller = [-1] * n
        
        # Find next smaller element
        for i in range(n):
            while stack and nums[stack[-1]] > nums[i]:
                next_smaller[stack.pop()] = i
            stack.append(i)
        
        # Clear stack for reuse
        stack.clear()
        
        # Find previous smaller element
        for i in range(n-1, -1, -1):
            while stack and nums[stack[-1]] >= nums[i]:
                prev_smaller[stack.pop()] = i
            stack.append(i)
        
        # Clear stack for next use
        stack.clear()
        
        # Arrays for next and previous greater elements
        next_greater = [n] * n
        prev_greater = [-1] * n
        
        # Find next greater element
        for i in range(n):
            while stack and nums[stack[-1]] < nums[i]:
                next_greater[stack.pop()] = i
            stack.append(i)
        
        # Clear stack for reuse
        stack.clear()
        
        # Find previous greater element
        for i in range(n-1, -1, -1):
            while stack and nums[stack[-1]] <= nums[i]:
                prev_greater[stack.pop()] = i
            stack.append(i)
        
        total = 0
        
        # Calculate contribution of each element
        for i in range(n):
            # Add contribution when element is maximum
            max_contribution = nums[i] * (i - prev_greater[i]) * (next_greater[i] - i)
            
            # Subtract contribution when element is minimum
            min_contribution = nums[i] * (i - prev_smaller[i]) * (next_smaller[i] - i)
            
            total += max_contribution - min_contribution
        
        return total
```