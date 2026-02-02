```
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        # stack numbers but when hit operator, operate on both previous numbers then combine into one variable until end
        operators = { # lambda functions
            "+": lambda a, b: a + b,
            "-": lambda a, b: a - b,
            "/": lambda a, b: int(a / b), # only in python
            "*": lambda a, b: a * b,
        }

        stack = []
        for i in tokens:
            if i in operators: # if operator do math on previous 2 numbers
                num2 = stack.pop()
                num1 = stack.pop()
                op = operators[i] # since numbers are popped, add back to stack
                stack.append(op(num1, num2))
            else:
                stack.append(int(i)) # list of strings, add numbers to stack
        return stack.pop() # pop last number to return
```