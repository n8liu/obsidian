```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dict = {} # created a dictionary

        for i in strs: # iterate through all items in the list
            key = "".join(sorted(i)) # sort the strings alphabetically by using sort, but sort uses a seperation of characters. so, use join on to make one word
            if key in dict: # check if a dictionary contains grouping of sorted words
                dict[key] = dict[key] + [i] # add if exist
            else:
                dict[key] = [i] # add if new
        
        return list(dict.values()) ## return list of all items
```

## key takeaways
- **find commonalities** the strings then group them together