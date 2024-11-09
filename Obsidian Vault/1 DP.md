#### [[Templates]]

# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
### Steps
- subproblem find (n-1) and (n-2), sum = n;

#### Code
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        first = 1
        second = 2
        for i in range(3, n + 1):
            third = first + second
            first = second
            second = third
        return second
```

# [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)
### Steps
- We want to work backwards and set each i$^{th}$ pos to the min cost to reach the end

#### code
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        cost.append(0)

        for i in range(len(cost)-3, -1, -1):
            cost[i] = min(cost[i]+cost[i+1], cost[i]+cost[i+2])

        return min(cost[0], cost[1])
```


# [198. House Robber](https://leetcode.com/problems/house-robber/)
### Steps
* The problem uses dynamic programming with only two variables to track the maximum money that can be stolen up to the previous and current houses respectively
- For each house, we have two options:
    - Rob the current house and add it to the money from two houses back (n + rob1)
    - Skip the current house and keep the money from the previous house (rob2)
- The code slides a "window" of two variables through the array, where:
    - rob1 represents max money if we ended two houses back
    - rob2 represents max money if we ended at previous house
    - temp stores the current best choice between the two options
- The pattern at each step is:
    1. Calculate best choice for current house (temp)
    2. Slide rob2 into rob1
    3. Make temp the new rob2

#### Code
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        rob1, rob2 = 0, 0

        for n in nums:
            temp = max(n + rob1, rob2)
            rob1 = rob2
            rob2 = temp
        return rob2
```

# [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)
### Steps
* Use house robber I, but run it twice
	* once skipping beginning and once skipping end, return max of the 2

#### Code
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]

        def helper(arr):
            rob1, rob2 = 0, 0

            for num in arr:
                temp = max(num + rob1, rob2)
                rob1 = rob2
                rob2 = temp
            return rob2

        return max(helper(nums[1:]), helper(nums[:-1]))
```

# [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)
### Steps
* 2D matrix
	* row starting index
	* col: ending index
* set $[row][col]$ to True if it is a palindrome
* Creates a 2D DP table where dp\[i]\[j] represents if substring from index i to j is a palindrome, initialized with False
* Iterates through the string from right to left (i) and for each i, checks all possible endings (j) from i to end
	* A substring is marked as palindrome (dp\[i]\[j] = True) when:
		* Characters at both ends match (s\[i] == s\[j]) AND
		* Either substring length is ≤ 3 (j - i <= 2) OR inner substring is palindrome (dp\[i + 1]\[j - 1])
	* If true, increment result


#### Code
```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        n, res = len(s), 0
        dp = [[0] * n for _ in range(n)]

        for i in range(n - 1, -1, -1):
            for j in range(i, n):
                if s[i] == s[j] and (j - i <= 2 or dp[i + 1][j - 1]):
                    dp[i][j] = 1
                    res += 1

        return res
```

# [91. Decode Ways](https://leetcode.com/problems/decode-ways/)
### Steps
* Have a dp cache
* Top Bottom search
	* if i has already been visited just return it
	* if char at i is 0, return 0
	* 2 ways to get count
		* i + 1 == 0 or i + 1 == 2
		* if i is not at the end of the string and (char at i  and char at i + 1 is between 10 - 26)
		* save and return count

#### Code
```python
class Solution:
    def numDecodings(self, s: str) -> int:
        dp = {len(s):1}

        def dfs(i):
            if i in dp:
                return dp[i]
            if s[i] == '0':
                return 0

            res = dfs(i+1)
            if i + 1 < len(s) and 
            (s[i] == '1'  or (s[i] == '2' and s[i+1] in "0123456")):
                res += dfs(i+2)
            dp[i] = res
            return res

        return dfs(0)

```

# [322. Coin Change](https://leetcode.com/problems/coin-change/)
### Steps
* Use Top-Bottom
* dp{amount : min}
* dfs of amount
	* if amount == 0
		* return 0
	* if amount in dp
		* return dp\[amount]
	* set currMin to max
	* for all coins 
		* if amount - coins >= 0
			* get new min
	* cache new amount
	* return curr min

#### Code
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = {}

        def dfs(amount):
            if amount == 0:
                return 0
            if amount in dp:
                return dp[amount]

            currMin = float('inf')
            for coin in coins:
                if amount - coin >= 0:
                    currMin = min(currMin, 1 + dfs(amount - coin ))
            dp[amount] = currMin
            return currMin 

        res = dfs(amount) 
        return res if res != float('inf') else -1
```

# [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
### Steps
* set result to max num
* Set curMin and curMax to 1
* loop through nums
	* if num is 0:
		* Set curMin and curMax to 1 and continue
	* set new currentMax, which is max of
		*  num or currMax \* n  or currMin \* n
	* set new currentMin, which is min of
		*  num or currMax \* n  or currMin \* n
	* set new result max
* return result max

#### Code
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        res = max(nums)
        curMin, curMax = 1, 1

        for n in nums:
            if n == 0:
                curMin, curMax = 1, 1
                continue
            temp = curMax * n
            curMax = max(n, temp, curMin*n)
            curMin = min(n, temp, curMin*n)
            res = max(res, curMax)

        return res       
```

# [139. Word Break](https://leetcode.com/problems/word-break/)
### Steps
* Initialize an array `dp` with the same length as `s` and all values initially set to `false`.
- Iterate `i` over the indices of `s`. At each `i`:
    - Iterate over each `word` in `wordDict`:
        - Check if `i == word.length - 1` or `dp[i - word.length] = true`.
        - If so, and the substring of `s` ending at `i` with the same length as `word` matches, set `dp[i] = true` and `break`.
- Return `dp[s.length - 1]`.

#### Code
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * (len(s) + 1)
        dp[len(s)] = True

        for i in range(len(s) - 1, -1, -1):
            for w in wordDict:
                if (i + len(w)) <= len(s) and s[i : i + len(w)] == w:
                    dp[i] = dp[i + len(w)]
                if dp[i]:
                    break

        return dp[0]
```

# 
### Steps
* Initialize a dp array of same length as input, filled with 1s
    - Each position represents the LIS length ending at that index
    - Base case is 1 since each number alone forms an LIS of length 1
- Iterate through array from right to left
    - For each position i, look at all numbers to its right
    - If current number is smaller than right number (nums[i] < nums[r])
        - Update the maximum subsequence length possible
    - Add the maximum found length to dp[i]
    - Track global maximum in res variable

#### Code
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)
        res = 0

        for i in range(len(nums)-1, -1, -1):
            r = i + 1
            currMax = 0
            while r < len(nums):
                if nums[i] < nums[r]:
                    currMax = max(currMax, dp[r])
                r+=1
            dp[i] += currMax
            res = max(res, dp[i])

        return res
```

# 
### Steps
* 

#### Code
```python

```