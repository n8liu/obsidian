```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        
        # similar to two sum ii
        sol = []
        nums.sort() # sort the list
        for i in range(len(nums)):
            if nums[i] > 0: # left side is too large, since sum to zero has to have negative numbers
                break
            if i == 0 or nums[i - 1] != nums[i]: # check when i is zero or when the numbers are not overlapping
                self.twosum(nums, i , sol) # run helper method
        return sol
    
    def twosum(self, nums: List[int], i: int, sol: List[List[int]]): # twosum implementation, helper method
        # i is the left bound
        # lo is iterator between i and hi
        # hi is upper bound
        lo = i + 1 #iterator
        hi = len(nums) - 1 # right index

        while lo < hi: # iteratire through all values between lo and hi
            sum = nums[i] + nums[lo] + nums[hi]
            if sum < 0: #if the sum is too low means the lower bound is too small
                lo += 1
            elif sum > 0: # if sum is too high means the upper bound value is too large
                hi -= 1
            else:
                sol.append([nums[i], nums[lo], nums[hi]]) # if valid value add to list
                lo += 1 # iterate again until find all values
                hi -= 1
                while lo < hi and nums[lo] == nums[lo - 1]: # to avoid duplicate results
                    lo += 1
```