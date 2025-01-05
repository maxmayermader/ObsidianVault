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

# [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
### Steps
* 2 DP with a 2d grid of 2 given words
* Create sub problems of matching chars
* If chars get diagonal `value + 1` 
* Else get the max between right and bottom values
* return the dp of the start

#### Code
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[0 for j in range(len(text2)+1)] for i in range(len(text1)+1)]

        for i in range(len(text1)-1, -1, -1):
            for j in range(len(text2)-1, -1, -1):
                if text1[i] == text2[j]:
                    dp[i][j] = 1 + dp[i+1][j+1]
                else:
                    dp[i][j] = max(dp[i+1][j], dp[i][j+1])

        return dp[0][0]
```

# [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
### Steps
* Create a dp cache that has index and boolean for index in the dp cache
* Sell move i by 2, Buying move i by 1 
	* base case: i is OOB
	* If val in dp return it
	* If we are buying we can buy or wait and save best result
	* If we are selling we can sell a stock or wait

#### Code
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        dp = {}

        def dfs(i, buying):
            if i >= len(prices):
                return 0

            if (i,buying) in dp:
                return dp[(i,buying)]

            if buying:
                buy = dfs(i+1, not buying) - prices[i]
                cooldown = dfs(i+1, buying)
                dp[(i, buying)] = max(buy, cooldown)
            else:
                sell = dfs(i+2, True) + prices[i]
                cooldown = dfs(i+1, False)
                dp[(i,buying)] = max(sell, cooldown)

            return dp[(i, buying)]

        return dfs(0, True)
```

# [518. Coin Change II](https://leetcode.com/problems/coin-change-ii/)
### Steps
* have a cache which has the which takes in an index and total
* We want to know how many ways to make the total so we add coins and count how many times it equals the total which is done in smaller subprobolems
* If total > amount or no more coins left return 0
* If the amount has been found return 1
* Add the *ways the amount can be reached* by adding current coin and next coin then setting the result in the cache
* return result

#### Code
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = {} #(index, target at that point)

        def bfs(i, t):
            if i >= len(coins) or t > amount: # no more coins or total exceeds amount
                return 0

            if t == amount:
                return 1
            
            if (i, t) in dp:
                return dp[(i,t)]

            dp[(i,t)] = 0  # Initialize before adding combinations
            # Use current coin multiple times or skip to next coin
            dp[(i,t)] = bfs(i, t + coins[i]) + bfs(i + 1, t)

            return dp[(i,t)]

        return bfs(0,0)
```

# [494. Target Sum](https://leetcode.com/problems/target-sum/)
### Steps
* Go through all numbers but at each number you can either add it or subtract it from the total
* Once you have added all numbers return 1 if it equal the target else 0
* Return repeated values
* Add the add the result of both adding and subtracting the next number to the cache
* Use a cached to store index and sum

#### Code
```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        dp = {}
        
        def bfs(i, t):
            if i >= len(nums):
                return 1 if t == target else 0
            
            # if t == target:
            #     return 1

            if (i, t) in dp:
                return dp[(i, t)]

            dp[(i,t)] = bfs(i+1, t+nums[i]) + bfs(i+1, t-nums[i])
            return dp[(i,t)]

        return bfs(0, 0)
                
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

