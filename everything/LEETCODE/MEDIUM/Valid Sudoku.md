```
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = [set() for _ in range(9)] # store values for each row, column, and boxes
        cols = [set() for _ in range(9)]
        boxes = [set() for _ in range(9)] # <- all hashsets

        for r in range(9): # most or all 2d array questions can only be solved in O(n^2)
            for c in range(9):
                val = board[r][c]
                if val == ".": # check if value is empty
                    continue

                if val in rows[r]: # check if already in a row set
                    return False
                rows[r].add(val)

                if val in cols[c]: # check if already in a col set
                    return False
                cols[c].add(val)

                box = (r // 3) * 3 + c // 3 # check if current number is valid inside the box
                if val in boxes[box]:
                    return False
                boxes[box].add(val)

        return True
```