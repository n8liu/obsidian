```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        dict = {} # s dictionary
        
        if len(s) != len(t): # check if characters are not the same length
            return False

        for i in s: # add all items to dict from s
            if i in dict:
                dict[i] = dict[i] + 1
            else:
                dict[i] = 1
        
        for i in t: # check t against s dictionary
            if i in dict:
                dict[i] = dict[i] - 1 # remove one from every dictionary until negative
                if dict[i] == -1:
                    return False
            else:
                return False
        return True # if everything passes then true
```