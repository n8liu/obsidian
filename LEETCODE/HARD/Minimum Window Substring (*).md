```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if not t or not s: # early exit for empty inputs
            return ""
        
        dict_t = Counter(t)
        required = len(dict_t) # number of distinct characters in t
        filtered_s = [] # filter all criteria is that the character should be present in t.
        for i, char in enumerate(s): #filter relevant characters, skip chars not in t which reduces pointer operations
            if char in dict_t:
                filtered_s.append((i, char))
        
        l, r = 0, 0 # traverse pointer characters
        formed = 0 # tracks how many distinct chars meet required count
        window_counts = {}

        ans = (float("inf"), None, None) # (length, start, end)

        while r < len(filtered_s):
            character = filtered_s[r][1]
            window_counts[character] = window_counts.get(character, 0) + 1
            if window_counts[character] == dict_t[character]:
                formed += 1
            
            while l <= r and formed == required:
                character = filtered_s[l][1]

                end = filtered_s[r][0]
                start = filtered_s[l][0]
                if end - start + 1 < ans[0]:
                    ans = (end - start + 1, start, end)

                window_counts[character] -= 1
                if window_counts[character] < dict_t[character]:
                    formed -= 1
                l += 1
            r += 1
        return "" if ans[0] == float("inf") else s[ans[1] : ans[2] + 1]
```