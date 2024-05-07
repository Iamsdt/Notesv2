---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:53
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:32
tags:
  - array
  - easy
  - hashtable
  - leetcode
---
## Problem: TwoSum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

## Solution:

substract from targets with current value and check that present in dict, if there then that dict value and current index is the answer, or save the value as dict key and index as dict value

```Plain
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        di = {}
        for i, v in enumerate(nums):
            r = target - v
            if r in di:
                return [di[r], i]
            else:
                di[v]=i


        return [0, 0]

```