# [155. Min Stack](https://leetcode.com/problems/min-stack/)
### Steps
- Normal stack but you keep track of the previous minimum element in the stack with a stack

#### Code
```python 
class MinStack:
    def __init__(self):
        self.s = []

    def push(self, val: int) -> None:
        if not self.s:
            self.s.append((val,val))
            return
        self.s.append((val, min(val, self.s[-1][1])))

    def pop(self) -> None:
        return self.s.pop()[0]

    def top(self) -> int:
        return self.s[-1][0]

    def getMin(self) -> int:
        return self.s[-1][1]
```

# [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
### Steps
- Use a stack. append numbers and pop 2 numbers when there is an operator and append the result

#### Code
```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        s = []

        def operation(op):
            b = s.pop()
            a = s.pop()
            if op == '*':
                return a * b
            elif op == '/':
                return int(a / b)  # Or use: a // b
            elif op == '+':
                return a + b
            else:
                return a - b

        for t in tokens:
            if t in {'+', '-', '*', '/'}:
                s.append(operation(t))
            else:
                s.append(int(t))

        return s[0]
```

# [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
### Steps
- backtracking with a stack
- Add opening parentheses if open < n
- Add closing if closing < open
- valid if open == closing == n
- pop characters added after visiting

#### Code
```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []
        stack = []

        def backtrack(openN, closeN):
            if openN == closeN == n:
                res.append(''.join(stack))
                return

            if openN < n:
                stack.append('(')
                backtrack(openN+1, closeN)
                stack.pop()
            if closeN < openN:
                stack.append(')')
                backtrack(openN, closeN+1)
                stack.pop()
            
        backtrack(0,0)
        return res
```

# [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)
### Steps
- Add temperatures, indices to a stack 
- Keep popping when you find a temperature greater than the top of the stack
	-  Set the popped index to the difference between current and popped indices  

#### Code
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = []
        res = [0]*len(temperatures)

        for i, temp in enumerate(temperatures):
            while stack and stack[-1][0] < temp:
                t, index = stack.pop()
                res[index] = i - index
            stack.append((temp,i))

        return res
```

# 