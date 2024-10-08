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


# [55. Jump Game](https://leetcode.com/problems/jump-game/)
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


# [846. Hand of Straights](https://leetcode.com/problems/hand-of-straights/)
### Steps
- Create a hm of the hand count
- Heapify the keys from HM
- go through pq
	- get top of the heap
		- loop for group size
			- if the next consequtive value is not in the loop return False
			- if the count of val is 0 and it's not the top of the heap return False
			- if the count of val is 0 then pop it from the heap

#### Code
```python
class Solution:
    def isNStraightHand(self, hand: List[int], groupSize: int) -> bool:
        if len(hand) % groupSize != 0:
            return False

        hm = collections.Counter(hand)
        pq = []
        for key in hm:
            heapq.heappush(pq, key)
        print(pq)

        while pq:
            top = pq[0]
            for val in range(top, groupSize+top):
                if val not in hm:
                    return False
                hm[val] -= 1
                if hm[val] == 0:
                    if val != pq[0]:
                        return False
                    heapq.heappop(pq)

        return True
```


# [1899. Merge Triplets to Form Target Triplet](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/)
### Steps
- store indices of target values in the triplets in a set
	- go through triplets 
		- add indices if the values are in the triplets
- if set == True, then return true

#### Code
```python
class Solution:
    def mergeTriplets(self, triplets: List[List[int]], target: List[int]) -> bool:
        good = set()

        for t in triplets:
            if t[0] > target[0] or t[1] > target[1] or t[2] > target[2]:
                continue
            for i, v in enumerate(t):
                if v == target[i]:
                    good.add(i)

        return len(good) == 3
```

# [763. Partition Labels](https://leetcode.com/problems/partition-labels/)
### Steps
- Use a *HM* for characters and the index of their last appearance
- loop through input string keeping track of partition size
	- set the end to the maximum end of visited chars
	- once you reach end append size to res, reset size and end


#### Code
```python
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        hm = {}
        for i, c in enumerate(s):
            hm[c] = i

        res = []
        end = 0
        size = 0
        for i in range(len(s)):
            end = max(end, hm[s[i]])
            size+=1

            if i == end:
                res.append(size)
                size = 0

        return res
```


# [678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)
### Steps
- keep track of the max num of left and right parenthesis
- loop through string
	- if there is an opening parentheses increment both left and right max
	- if there is a closing decrement both left and right parentheses
	- If you have a wild card increase max and decrement min
	- if max parentheses is < 0 return False (you have more closing parentheses than possible openings)
	- reset left to 0 if, min < 0 

#### Code
```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        leftMin, rightMax = 0,0

        for c in s:
            if c == '(':
                leftMin += 1
                rightMax += 1
            elif c == ')':
                leftMin -= 1
                rightMax -= 1
            else:
                leftMin -= 1
                rightMax += 1
            if rightMax < 0:
                return False
            if leftMin < 0:
                leftMin = 0
            
        return leftMin == 0
```
