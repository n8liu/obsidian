```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        dq = deque() # stores indices of elements in decreasing order
        res = [] # stores maximum for each window

        for i in range(k): # first window, maintain decreasing order
            while dq and nums[i] >= nums[dq[-1]]:
                dq.pop()
            dq.append(i)
        
        res.append(nums[dq[0]]) # max in first window

        for i in range(k, len(nums)): # sliding window
            if dq and dq[0] == i - k:
                dq.popleft()
            while dq and nums[i] >= nums[dq[-1]]: # remove the leftmost index
                dq.pop()
            
            dq.append(i) # same logic as initial window, but remove elements from back
            res.append(nums[dq[0]])
        return res
```