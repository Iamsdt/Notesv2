---
Created by: Shudipto Trafder
Created time: 2023-10-18T19:55
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:24
tags:
  - algo
---
take the first element from the list  
and make count 1  
then iterate through from second element  
if it is the same then increase the count else reduce the count  
if the count is zero then update the candidate  

```Plain
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