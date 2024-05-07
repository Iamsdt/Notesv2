---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:46
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:42
tags:
  - Stack
  - String
  - easy
  - leetcode
---
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.  
Open brackets must be closed in the correct order.  

### Solution:

create dict, where key is open brackets and value close brackets  
check current bracket is opening then put into stack  
else check if not in stack or pop from stack and match with current value or not  

```Plain
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