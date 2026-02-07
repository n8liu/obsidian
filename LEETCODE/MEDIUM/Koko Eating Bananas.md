```
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        def calculate_hours(k):
            hours = 0

            for pile in piles:
                hours += ceil(pile / k)
            
            return hours

        left = 1
        right = max(piles)
        ans = max(piles)
        while left <= right:
            mid = (right+left) // 2

            if calculate_hours(mid) > h:
                left = mid + 1
            else:
                ans = mid
                right = mid -1
        return ans
```