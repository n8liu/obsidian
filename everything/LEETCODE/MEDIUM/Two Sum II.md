```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # current implementation: similar as previous two sum with a dictionary
        # new implementation: uses the fact that the array is sorted
        # use two pointer: one left and one right
        #               if left + right is greater than targer then move index right down one
        #               if left + right is less than target then move index left up one
        # O(n) time bc traverse list once and O(1) space

        left = 0 # left index
        right = len(numbers) - 1 # right index

        while left < right:
            sum = numbers[left] + numbers[right]

            if sum == target:
                return [left + 1, right + 1] # index added 1
            elif sum < target:
                left += 1
            else:
                right -= 1
        
        return [] # case n/a
```