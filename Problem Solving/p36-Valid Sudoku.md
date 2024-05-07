---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:47
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:43
tags:
  - Matrix
  - Medium
  - array
  - hashtable
  - leetcode
---
Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.  
Each column must contain the digits 1-9 without repetition.  
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.  
Note:  

A Sudoku board (partially filled) could be valid but is not necessarily solvable.  
Only the filled cells need to be validated according to the mentioned rules.  

### Solution

column and rows check one by one  
for 3 by 3 blocks  
use 4 pointers