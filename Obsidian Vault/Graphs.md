#### [[Templates]]

# [2684. Maximum Number of Moves in a Grid](https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/)
### Steps
* Use BFS 
* Count moves and return the maximum

#### Code
```python
class Solution:
    def maxMoves(self, grid):
        numRows, numCols = len(grid), len(grid[0])
        dirs = [-1, 0, 1]   # The three possible directions for the next column
        q = deque()
        visited = set()
        
        # Enqueue the cells in the first column
        for row in range(numRows):
            visited.add((row, 0))
            q.append((row, 0, 0))
            
        maxMoves = 0
        
        while q:
            queueSize = len(q)
            currRow, currCol, moveCount = q.popleft()
            maxMoves = max(maxMoves, moveCount)
            
            for direction in dirs:
                # Next cell after the move
                newRow, newCol = currRow + direction, currCol + 1
                
                # Check if next move is valid and unvisited
                if (0 <= newRow < numRows and 
                    0 <= newCol < numCols and 
                    (newRow, newCol) not in visited and 
                    grid[currRow][currCol] < grid[newRow][newCol]):
                    
                    visited.add((newRow, newCol))
                    q.append((newRow, newCol, moveCount + 1))
                        
        return maxMoves
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