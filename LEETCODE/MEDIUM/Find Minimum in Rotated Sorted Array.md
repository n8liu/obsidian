```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        n = len(nums)

        left = 0
        right = n - 1
        min_val = max(nums)
        while left <= right:
            mid = (right+left) // 2
            min_val = min(nums[mid],min_val)
            if nums[mid] > nums[right]:
                left = mid +1
            else:
                right = mid -1
        return min_val
```