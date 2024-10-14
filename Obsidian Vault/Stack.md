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