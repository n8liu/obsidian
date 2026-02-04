```
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        # the largest area is the combination of multiple histograms given height is shorter histogram
        stack = [-1] # minimum stack item
        max_area = 0 # keeps track of max
        for i in range(len(heights)):
            while stack[-1] != -1 and heights[stack[-1]] >= heights[i]: # valid bars in stack and curr bar is shorter/equal to top bar of stack
                curr_height = heights[stack.pop()] # pop index from stack
                curr_width = i - stack[-1] - 1
                max_area = max(max_area, curr_height * curr_width) # update max area
            stack.append(i)
        
        while stack[-1] != -1:
            curr_height = heights[stack.pop()]
            curr_width = len(heights) - stack[-1] - 1
            max_area = max(max_area, curr_height * curr_width)
        return max_area
```