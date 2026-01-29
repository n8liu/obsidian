```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        buyprice = prices[0] # check buy price
        profit = 0

        for p in prices:
            if buyprice > p: # checks if buyprice is is too big, want the smaller number
                buyprice = p
            
            profit = max(profit, p - buyprice) # checks if the current max profit is still bigger or the new current price minus the buy price is bigger
        return profit
```