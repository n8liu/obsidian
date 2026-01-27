```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        streak = 0 # keep track of longest streak
        num_set = set(nums) # create a unique element list

        for i in num_set: # loop through all numbers once O(n)
            currnum = i
            currstreak = 1

            while currnum + 1 in num_set: # check if next number is inside the list
                currnum += 1
                currstreak += 1
            
            streak = max(streak, currstreak) # check if current subsequence is the largest
        
        return streak
```