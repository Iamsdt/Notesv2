---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - leetcode
---


Fibonacci number is amongst the most common problem. There isn't much to this problem since it can be solved easily by directly applying what's given in the problem statement 

_**Solution - I (Recursion)**_

Using the basic definition of Fibonacci numbers - `F(n) = F(n - 1) + F(n - 2)` and `F(0) = 0, F(1) = 1`

```python
def fib(int n): 
	if(n <= 1) // base condition
		return n;
	return fib(n - 1) + fib(n - 2);
	// or 1-liner:
	// return n <= 1  ? n : fib(n - 1) + fib(n - 2);
```

_**Time Complexity :**_ **`O(2^N)`**. It can be calculated from the recurrence relation `T(N) = T(N-1) + T(N-2)`. This is the most naive approach to calculate fibonacci number and recursion tree grows exponentially. There's a lot of repeated work that happens here.  
_**Space Complexity :**_ **`ON)`**, required for recursive call stack.


_**Solution - II (Top-Down Recursive Approach - Dynamic Programming)**_

```python
int memo[31] = {0};

int fib(int n) {
	if(n <= 1)
		return n;
	if(memo[n])
		return memo[n];
	return memo[n] = fib(n - 1) + fib(n - 2);
	// or 1-liner:
	// return memo[n] = memo[n] ? memo[n] : n <= 1 ? n : fib(n - 1) + fib(n - 2);
}
```
