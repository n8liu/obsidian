```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        s1len, s2len = len(s1), len(s2) # store string length

        if s1len > s2len: # quick base case check
            return False
        
        s1_char = [0] * 26 # freq table
        s2_char = [0] * 26 # freq table of current window

        for i in range(s1len): # populates the array
            s1_char[ord(s1[i]) - ord('a')] += 1 # converts letter to unicode
            s2_char[ord(s2[i]) - ord('a')] += 1

        if s1_char == s2_char: #checks if the first window is a match
            return True

        for i in range(s2len - s1len): # s2len - s2len so no out of bounds, slides s1 window across s2
            s2_char[ord(s2[i]) - ord('a')] -= 1 # removes left most character
            s2_char[ord(s2[i + s1len]) - ord('a')] += 1 # add new character from the right

            if s1_char == s2_char: # check if the current window matches s1 frequency, not checking permutation but checking count of each character
                return True
        
        return False
```