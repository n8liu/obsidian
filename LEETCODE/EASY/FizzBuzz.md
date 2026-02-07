```
class Solution:
    def fizzBuzz(self, n: int) -> List[str]:
        arr = []
        for i in range(1, n + 1):
            # case 1: divisible by both
            if i % 15 == 0:
                arr.append("FizzBuzz")
            # case 2: divisible by 3
            elif i % 3 == 0:
                arr.append("Fizz")
            # case 3: divisible by 3
            elif i % 5 == 0:
                arr.append("Buzz")
            # case 4: none
            else:
                arr.append(str(i))
        return arr
```