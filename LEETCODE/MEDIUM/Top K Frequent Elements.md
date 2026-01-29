```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # dict = {} # create dictionary

        # for i in nums: #add all items to dictionary
        #     if i in dict:
        #         dict[i] = dict[i] + 1
        #     else:
        #         dict[i] = 1
        
        # #need to sort numbers by biggest to least count
        # print(sorted(dict.items(), key=lambda item: item[1]))
        # DNF
```

O(n log k) by using a MinHeap ← heapq library
```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:

        #use min heap O(n log k) <- use for sort biggest to smallest get fast

        dict = {}
        minheap = []
        
        # # for i in nums: # better looking way
        # #     dict[i] = dict.get(i, 0) + 1

        for i in nums: #add all items to dict
            if i in dict:
                dict[i] = dict[i] + 1
            else:
                dict[i] = 1
        
        for i, j in dict.items(): # iterate through all tuples in dict
            heapq.heappush(minheap, (j, i)) # add all items to the heap, heapq minheap by default
            if len(minheap) > k: 
                heapq.heappop(minheap) # after adding an item, check new minheap if items change, if changed remove smallest item
        return [i for j, i in minheap] # print out list of items
```

Use python library Counter which creates a list of frequencies “{(1, 3), (2, 2), (3, 1)}” which would be faster than above method

```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # dict = {} # create dictionary

        # for i in nums: #add all items to dictionary
        #     if i in dict:
        #         dict[i] = dict[i] + 1
        #     else:
        #         dict[i] = 1
        
        # #need to sort numbers by biggest to least count
        # print(sorted(dict.items(), key=lambda item: item[1])) 

        #use min heap O(n log k) <- use for sort biggest to smallest get fast

        dict = Counter(nums)
        minheap = []
        
        # # for i in nums: # better looking way
        # #     dict[i] = dict.get(i, 0) + 1
        
        # for i in nums: #add all items to dict
        #     if i in dict:
        #         dict[i] = dict[i] + 1
        #     else:
        #         dict[i] = 1
        
        for i, j in dict.items(): # iterate through all tuples in dict
            heapq.heappush(minheap, (j, i)) # add all items to the heap, heapq minheap by default
            if len(minheap) > k: 
                heapq.heappop(minheap) # after adding an item, check new minheap if items change, if changed remove smallest item
        return [i for j, i in minheap] # print out list of items
```