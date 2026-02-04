```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0 # left bound
        right = len(nums) - 1 # right bound
        
        while left <= right:
            mid = (left + right) // 2 # middle index
            
            # Case 1, return the middle index.
            if nums[mid] == target:
                return mid
            # Case 2, discard the smaller half.
            elif nums[mid] < target:
                left = mid + 1                 
            # Case 3, discard the larger half.         
            else:
                right = mid - 1
        
        # If we finish the search without finding target, return -1.
        return -1
```