---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:40
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:40
tags:
  - Queue
  - Stack
  - easy
  - leetcode
---
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

void push(int x) Pushes element x to the back of the queue.  
int pop() Removes the element from the front of the queue and returns it.  
int peek() Returns the element at the front of the queue.  
boolean empty() Returns true if the queue is empty, false otherwise.  
Notes:  

You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.  
Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.  

### Solution

take head this is going to use in peek  
push -> save everything into s1  
pop -> is s2 is empty then add from s1 and then pop from s2  
peek -> if s2 not empty then return last element or return head  
empty -> check everything ok  

```Plain
class MyQueue:

    def __init__(self):
        self.s1 = []
        self.s2 = []
        self.head = []

    def push(self, x: int) -> None:
        if not self.s1:
            self.head = x
        self.s1.append(x)

    def pop(self) -> int:
        if not self.s2:
            while self.s1:
                self.s2.append(self.s1.pop())

        return self.s2.pop()

    def peek(self) -> int:
        if self.s2:
            return self.s2[-1]

        return self.head

    def empty(self) -> bool:
        return not self.s1 and not self.s2

```