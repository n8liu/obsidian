```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # two-pointer O(n) time and O(1) space
        i = 0 # left pointer
        j = len(s) - 1 # right pointer

        while i < j: # while the left and right dont reach each other
            while i < j and not s[i].isalnum(): # check left until reaches number/letter
                i+= 1
            while i < j and not s[j].isalnum(): #check right until reaches number/letter
                j -= 1

            if s[i].lower() != s[j].lower(): # checks the left and right have the same number/letter
                return False # if not return false

            i += 1 # if match then move one pointer inwards
            j -= 1
        
        return True # return true if all matched
```

