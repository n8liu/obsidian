```
class Solution:
    def isValid(self, s: str) -> bool:
        # current implementation, add every string if open bracket, if close bracket check if most recent bracket is open bracket match
        # missing, need a map to match
        
        stack = [] # creates stack
        mapping = {")": "(", "}": "{", "]": "["} # create mapping to match brackets

        for i in s: # loop through string
            if i in mapping: # check if valid mapping char
                top = stack.pop() if stack else "" # pop unless empty then return nothing
                if mapping[i] != top: # if no match return false
                    return False
            else:
                stack.append(i) # add to stack since its not an open bracket
        
        return not stack # returns true or false if stack is empty
        # return false if stack is empty, but we want true when all values are popped
```