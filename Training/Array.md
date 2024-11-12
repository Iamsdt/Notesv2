---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - leetcode
---

[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) (amazon)
```python
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


[152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) (amazon)
3,-1, 4 | [-3,-1,-1]

All positive that call Product Increasing
[1, 2, 3, 4]

Negative One:
[-1, -2, -3]

Edge case:
what about zero
then use neutral value

tract min also

```python
class Solution:
    def maxProduct(self, nums: int) -> int:
        res = max(nums)
        cu_min, cu_max = 1, 1

        for n in nums:
            if n == 0:
                cu_min, cu_max = 1, 1
                continue
            
            temp = n*cu_max
            cu_max = max(n*cu_max, n*cu_min, n) #some language doesn's allow [-1, 8]
            cu_min = min(temp, n*cu_min, n) # [-1, -8], we want -8
            res = max(res, cu_max)

        return res
```


1. Two sum
```python
class Solution:

def twoSum(self, nums: List[int], target: int) -> List[int]:

di = {}

for i, v in enumerate(nums):

r = target - v

if r in di:

return [di[r], i]

else:

di[v] = i

  

return [0, 0]
```

1. Two sum 2

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        p, n = 0, len(numbers) -1

        while p < n:
            v = numbers[p]  + numbers[n]
            if v == target:
                return p+1, n+1

            if v < target:
                 p += 1
            else:
                n -= 1
```

121. Best Time to buy and sell stock

```python
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


[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```

[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        match = {'(': ')', '[': ']', '{': '}'}
        for c in s:
            if c in ['(', '[', '{']:
                stack.append(c)
            elif not stack or match[stack.pop()] != c:
                return False
        return not stack
```


