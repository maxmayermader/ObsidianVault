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