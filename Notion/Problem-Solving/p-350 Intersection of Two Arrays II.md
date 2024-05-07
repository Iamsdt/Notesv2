---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:52
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:45
tags:
  - BS
  - Sorting
  - TwoPointer
  - array
  - easy
  - hashtable
  - leetcode
---
Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

### Solution

put things into dict, check the key present in both dict  
take minimum and then appen the value as number of times  

```Plain
from typing import List
from collections import Counter


class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        di1 = Counter(nums1)
        di2 = Counter(nums2)
        res = []
        for i in di1.keys():
            if i in di2:
                v = min(di1[i], di2[i])
                res.extend([i]*v)

        return res

```