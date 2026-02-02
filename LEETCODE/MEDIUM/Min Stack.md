```
class MinStack:

    def __init__(self):
        self.stack = [] # declare stack

    def push(self, val: int) -> None:
        if not self.stack: # if stack is empty, add val because their is no values in list yet
            self.stack.append((val, val)) # current val, current min
            return
        curr_min = self.stack[-1][1] # gets previous, or last item in list
        self.stack.append((val, min(val, curr_min))) # append new value and the minimum between current value and previous value. keep checking previous value total min

    def pop(self) -> None:
        self.stack.pop() # removes top element from stack

    def top(self) -> int:
        return self.stack[-1][0] # gets last item in list, or top of stack value

    def getMin(self) -> int:
        return self.stack[-1][1] # returns minimum which is the second value at the top of the stack


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```