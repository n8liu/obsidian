```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        # thinking: keep track of previous multiplcations
        #           current thinking implementation is n^2

        # breaking the problem down, we want all values multiplied to the left and right of current number

        # initilize array with values because unable to access array with no values
        combine = [0] * len(nums) # answer array of combining the left and right side

        combine[0] = 1
        for i in range(1, len(nums)):
            combine[i] = nums[i - 1] * combine[i - 1] #combine all values of left side into the array first
        
        right = 1
        for i in reversed(range(len(nums))): # all values on the right side multiply into the combined array
            combine[i] = combine[i] * right
            right *= nums[i]
        
        return combine
```