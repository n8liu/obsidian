```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dict = {}
        
        for i in range(len(nums)): # iterate through all numbers 0 to end
            complement = target - nums[i] # 9 - number in list (9 - 2 = 7)
            if complement in dict: # check if the complement is a number in the original list
                return [dict[complement], i] # [if previous number is the complement, index is the second number found]
            dict[nums[i]] = i # if not in orignal list, add number to dictionary with key as the number and the value as the index
```


remember this one