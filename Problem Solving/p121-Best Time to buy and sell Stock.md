---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:47
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:44
tags:
  - DP
  - array
  - easy
  - leetcode
---
### Problems

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

### Solution

asume first value is invest, now iterate throught second index, if you find the vlaue less than invert update it or calculate profile and keep max one

```Plain
from typing import List


class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        invest = prices[0]
        for i in range(1, len(prices)):
            if prices[i] < invest:
                invest = prices[i]
            else:
                profit = max(prices[i] - invest, profit)

        return profit

```