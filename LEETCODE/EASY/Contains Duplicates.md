```
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        dict = {} # create new dictionary
        for i in nums: # loop through all items
            if i in dict: 
                return True
            else:
                dict[i] = 0 # initilize all added numbers to 0
        return False
```
