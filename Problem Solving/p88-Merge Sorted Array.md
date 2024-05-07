---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:52
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:35
tags:
  - Sorting
  - TwoPointer
  - easy
  - leetcode
---
### Problem

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

### Sort Solution

if num1 greater then nums2 then add nums1 last, or do opposite  
and if anything left in num2 add the things first in nums1  

### Solution

start from end of nums 1  
if num1 is greater than num2 then save nums1 on last index and reduce num1 pointer else update with num2  

and the end, check num2 pointer is anything left then add these things in first on nums1

```Plain
from typing import List


class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        last = m + n -1
        while m > 0 and n > 0:
            if nums1[m-1] > nums2[n-1]:
                nums1[last] = nums1[m-1]
                m -= 1
            else:
                nums1[last] =nums2[n-1]
                n -= 1

            last -= 1

        while n > 0:
            nums1[last] = nums2[n-1]
            n -= 1
            last -=1


        return nums1
```