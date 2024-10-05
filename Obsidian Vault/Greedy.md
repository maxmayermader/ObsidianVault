## [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
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

