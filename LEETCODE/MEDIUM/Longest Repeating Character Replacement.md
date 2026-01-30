```
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        start = 0 # starting pointer of window
        freq_map = {} # frequency of characters of window
        max_freq = 0 # high freq of any character
        longest = 0 # longest window saved

        # we add plus one to start/end because word length starts at one

        for end in range(len(s)): # move right pointer (end)
            freq_map[s[end]] = freq_map.get(s[end], 0) + 1 # add character to freq_map set to zero or plus one
            max_freq = max(max_freq, freq_map[s[end]])
# update max_freq with max
            valid = (end + 1 - start - max_freq <= k) # check if make sure not to edit too many characters
            if not valid:
                freq_map[s[start]] -= 1 # remove one character
                start += 1 # increase beg by one
            
            longest = end + 1 - start # update longest

        return longest
```