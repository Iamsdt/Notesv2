---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:35
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:33
tags:
  - DivideAndConquer
  - Sorting
  - array
  - easy
  - hashtable
  - leetcode
---
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

### Solution

Boyer–Moore Majority vote algorithm  
take the first element from the list  
and make count 1  
then itter through from second element  
if it is same then increase count else reduce count  
if count is zero then update the candidate  

```Plain
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        di = Counter(nums)

        item = 0
        value = 0

        for i in di.keys():
            m = max(item, di[i])
            if item <= m:
                value = i

        return value

    # Boyer–Moore Majority vote algorithm
    def maxElement(self, nums: List[int]) -> int:
        candidate = nums[0]
        count = 1

        for i in range(1, len(nums)):
            if nums[i] == candidate:
                count += 1
            else:
                count -= 1

            if count == 0:
                candidate = nums[i]
                count = 1

        return candidate
```