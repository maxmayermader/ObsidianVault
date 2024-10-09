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

