---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - leetcode
---


### 1. Maximum Sum Subarray of Size K
Variation with Minimum Sum, max avg, min avg

Given an array of positive integers and a positive number`k`, find the maximum sum of any contiguous subarray of size `k`.
```
Input: [3, 5, 2, 1, 7], k=2
Output: 8
```

The subarray `[1, 7]` is the sum of the maximum sum.

```python
def getMaxSum(arr, k):
    maxSum = 0
    windowSum = 0
    start = 0
    
    for i in range(len(arr)):
        windowSum += arr[i]
        
        if ((i - start + 1) == k):
            maxSum = max(maxSum, windowSum)
            windowSum -= arr[start]
            start += 1
    
    return maxSum
```



### 2. Difference Between the Maximum and Minimum Average of all K-Length Continuous Subarrays

```
Input: arr[3, 8, 9, 15], K = 2
Output: 6.5
```

All subarrays of length 2 are `{3, 8}`, `{8, 9}`, `{9, 15}` and their averages are `(3+8)/2 = 5.5, (8+9)/2 = 8.5`, and `(9+15)/2 = 12.0` respectively.

Therefore, the difference between the `maximum(=12.0)` and `minimum(=5.5)` is `12.0 -5.5 = 6.5`.

#### Solution

```python
def getMinMaxDiff(arr, k):
    n = len(arr)
    
    if k > n:
        return -1
    
    min_avg = float('inf')
    max_avg = float('-inf')
    
    window_sum = sum(arr[:k])
    
    for i in range(k, n):
        current_avg = window_sum / k
        min_avg = min(min_avg, current_avg)
        max_avg = max(max_avg, current_avg)
        window_sum -= arr[i - k]
        window_sum += arr[i]
    
    last_avg = window_sum / k
    min_avg = min(min_avg, last_avg)
    max_avg = max(max_avg, last_avg)
    
    difference = max_avg - min_avg
    
    return difference

# Test case
arr = [3, 8, 9, 15]
k = 2
result = getMinMaxDiff(arr, k)
print(result)  # Output: 6.5
```


### 3. Find Duplicates Within a Range ‘K’ in an Array

```
​Input: nums = [5, 6, 8, 2, 4, 6, 9]
k = 2
Ouput: False​
```

#### Solution

```
def getDuplicates(nums, k):
    d = {}
    count = 0
    for i in range(len(nums)):
        if nums[i] in d and i - d[nums[i]] <= k:
            return True
        else:
            d[nums[i]] = i
    
    return False
```


###  4. Number of Subarrays of Size K and Average Greater than or Equal to Threshold

Given an array of integers `arr` and two integers `k` and threshold.

Return the number of subarrays of size `k` and average greater than or equal to a threshold.

```
Input: arr = [2,2,2,2,5,5,5,8], k = 3, threshold = 4
Output: 3
Explanation: Sub-arrays [2,5,5],[5,5,5] and [5,5,8] have averages 4, 5 and 6 respectively. All other sub-arrays of size 3 have averages less than 4 (the threshold).
```

#### **Solution**

```
class Solution(object):
    def numOfSubarrays(self, arr, k, threshold):
        """
        :type arr: List[int]
        :type k: int
        :type threshold: int
        :rtype: int
        """
        start = 0
        windowSum = 0
        count = 0
        
        for windowEnd in range(len(arr)):
            windowSum += arr[windowEnd] 
            if windowEnd >= k - 1:
                if (windowSum/k) >= threshold:
                    count+=1
                windowSum -=arr[start]
                start += 1
                
        return count
```



### 5. Length of the Longest Substring That Doesn’t Contain Any Vowels

```
Input: s = "codeforintelligents"
Output: 3
Explanation: 'nts' is the longest substring that doesn't contain any vowels.
```

#### Solution

```
def getLongestSubstring(s):
    vowels = ['a', 'e', 'i', 'o', 'u']
    result = ""
    maxResult = ""
    for i in range(len(s)):
        if s[i] not in vowels:
            result += s[i]
            if len(result) > len(maxResult):
                maxResult = result
        else:
            result = ""
    
    return len(maxResult)
```

### 6. Maximum Number of Vowels in a Substring

Given a string s.
Return the maximum number of vowel letters in any sub string of s.
Vowel letters in English are (a, e, i, o, u).

```
Input: s = "abciiidef"
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.
```

#### **Solution**
```
def getLongestSubstring(s):
    vowels = ['a', 'e', 'i', 'o', 'u']
    result = ""
    maxResult = ""
    for i in range(len(s)):
        if s[i] in vowels:
            result += s[i]
            if len(result) > len(maxResult):
                maxResult = result
        else:
            result = ""
    
    return len(maxResult)
```

