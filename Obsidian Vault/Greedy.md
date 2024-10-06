# [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
### Steps
- We want to loop through the array
- We only want the maximum subarray
	- if we find a subarray that is > 0
		- Set the subarray sum to 0
	- continue adding values to subarray and tracking max

#### Code
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        maxSub = nums[0]
        curSub = 0

        for n in nums:
            if curSub < 0:
                curSub = 0
            curSub += n
            maxSub = max(maxSub, curSub)

        return maxSub
```


## [55. Jump Game](https://leetcode.com/problems/jump-game/)
### Steps
- Can the goal reach the start
- start at the goal and work you way back
- if index can reach the goal then set new goal to index
- if goal is 0 (start) return True else False

#### Code
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        goal = len(nums)-1
        for i in range(goal, -1, -1):
            if i + nums[i] >= goal:
                goal = i

        return goal == 0
```


# [45. Jump Game II](https://leetcode.com/problems/jump-game-ii/)
### Steps
- It maintains a window [l, r] representing the range of indices that can be reached in the current jump.
- In each iteration, it finds the farthest index that can be reached from the current window.
- The window is then updated, and the jump count is incremented.
- The process continues until the right boundary of the window reaches or exceeds the last index.

#### Code
```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        res = 0
        l = r = 0
        while r < len(nums)-1:
            maxJump = 0
            for i in range(l, r+1):
                maxJump = max(maxJump, i + nums[i])

            l = r + 1
            r = maxJump
            res += 1

        return res
```



# [134. Gas Station](https://leetcode.com/problems/gas-station/)
### Steps
- -First, check if a solution is possible by comparing total gas to total cost
- We want to loop through all the stations once
- We're looking for the starting station that allows a complete circuit
    - Keep a running total of gas surplus/deficit
    - If the running total becomes negative at any point:
        - Reset the running total to 0
        - Update the potential starting station to the next one
- The last updated starting station is our answer

#### Code
```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        if sum(gas) < sum(cost):
            return -1

        res = 0
        total = 0
        for i in range(len(gas)):
            total += gas[i] - cost[i]
            if total < 0:
                total = 0
                res = i+1

        return res
```



# y