```
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        cars = sorted(zip(position, speed)) # pairs cars with speed using zip, then sort cars in ascending order by creating tuples
        times = [float(target - p) / s for p, s in cars] # for each car, calculates target
        ans = 0 # number of car fleets
        while len(times) > 1:
            lead = times.pop() # removes and gets time of car
            if lead < times[-1]: # if car arrives before the next car, cannot form a fleet
                ans += 1
            else:
                times[-1] = lead # sametime or later, than car behind merges into one fleet
        return ans + bool(times)
```