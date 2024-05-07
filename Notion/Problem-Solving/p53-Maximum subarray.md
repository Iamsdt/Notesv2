---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:53
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:44
tags:
  - DP
  - DivideAndConquer
  - Medium
  - array
  - leetcode
---
# Max Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

## Short

add with previous value, if value is negative then reset to zero and compare max with current value

### Long

track max results and current results (start with zero)  
add new number with current res, if the results is negative then rest to zero  
and compare max res and current res  
answer max res  

```Python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        max_res = nums[0]

        current = 0

        for i in nums:
            if current < 0:
                current = 0

            current += i
            max_res =  max(max_res, current)


        return max_res
```