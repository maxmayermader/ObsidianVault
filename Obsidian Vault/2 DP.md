# [62. Unique Paths](https://leetcode.com/problems/unique-paths/)
### Steps
• Bottom-Up Approach: The solution starts from the bottom-right cell (m-1, n-1) and works its way up and left, calculating the number of possible paths for each cell.
• Dictionary Storage: Uses a dictionary to store coordinates and their corresponding path counts, where the key is a tuple (row, column) and the value is the number of unique paths to reach that cell.
• Direction Handling: Implements movement in two directions (left and up) using the directions array`[[0, -1], [-1, 0]]`, which represents possible moves from any given cell.
• Path Accumulation: For each cell, it checks its neighboring cells (based on allowed directions) and accumulates the number of possible paths. If a neighboring cell exists, it adds the current cell's path count to that neighbor's count.
• Base Case: Initializes the target cell (bottom-right) with a value of 1, as there is exactly one way to reach the destination from itself, and builds up the solution from there.

#### Code
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = {(m-1, n-1) : 1} # (r, c) : move count
        directions = [[0, -1], [-1, 0]]

        for r in range(m-1, -1, -1):
            for c in range(n-1, -1, -1):
                for dr, dc in directions:
                    newr, newc = r + dr, c + dc
                    if newr >= 0 and newc >= 0:
                        if (newr, newc) in dp:
                            dp[(newr, newc)] +=  dp.get((r,c), 0)
                        else:
                            dp[(newr, newc)] =  dp.get((r,c), 0)

        return dp[(0,0)]
```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

