```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        # two-pointer: start at left and right then calculate the total area to see if its max
        left = 0 # left index
        right = len(height) - 1 # right index

        maxarea = 0 # biggest area

        while left < right: # until both pointers reach eachother
            width = right - left # width is the distance between indexes
            maxarea = max(maxarea, min(height[left], height[right]) * width)
            # maxarea is the max of the current area times the minimum height * width to find which is larger 
            if height[left] <= height[right]: # move the pointer of the shorter height since the area does not decrease but could increase
                left += 1
            else:
                right -= 1
        
        return maxarea
```
