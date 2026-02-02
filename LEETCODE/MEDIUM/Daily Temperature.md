```
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        answer = [0] * len(temperatures) # create list of len(temps)
        stack = []

        for currday, currtemp in enumerate(temperatures): # enumerate is similar to range(len(s))[i] to get the values but iterate over index
            while stack and temperatures[stack[-1]] < currtemp: # add to stack, adn check i
                prevday = stack.pop()
                answer[prevday] = currday - prevday # used to create track of temperatures and days counted
            stack.append(currday) # add 

        return answer
```