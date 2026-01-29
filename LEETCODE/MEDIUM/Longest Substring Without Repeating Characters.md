```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        # sliding window, if duplicate appears in window drop left until no duplicates
        # using hashset, so checking character is done in O(1) time
        ans = 0

        char = {} # hashset

        i = 0
        for j in range(len(s)): #loop through index of characters
            # j = 0 1 2 3 4
            if s[j] in char: # if character exists or basically a duplicate
                i = max(char[s[j]], i) # move the window left pointer right until no duplicate
            
            ans = max(ans, j - i + 1) # checks if the current length window is bigger than old
            char[s[j]] = j + 1 # add/update character to set plus character index, the reason for this is so i can update instantly to last previous seen of the character
        return ans
```
