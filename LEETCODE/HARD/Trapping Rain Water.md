```
class Solution:
    def trap(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1 # index
        ans = 0 # total water
        leftmax, rightmax = 0, 0

        while left < right: #until pointer touch
            if height[left] < height[right]: # height of left wall is less than height of right wall
                leftmax = max(leftmax, height[left]) # save the bigger wall to the left side max
                ans += leftmax - height[left]
                # left max is the biggest wall of the right so no water overflows minus the height of the left
                print(ans)
                left += 1
            else: # case two
                rightmax = max(rightmax, height[right])
                ans += rightmax - height[right]
                right -= 1
        return ans
```