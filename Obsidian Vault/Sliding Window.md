#### [[Templates]]

## [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

### Steps
- Create a window using a deque
- Keep track of indexes in the q
- you want to keep the biggest elements at the front the q
	- You can add if it is smaller than rightmost position
	- if it is bigger pop right most and add new el
- once you have completed the window pop left el and add to res
- then pop left element and repeat steps until window is at the end of arr

#### Code
```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        output = []
        q = collections.deque()  # Deque to store indices of potential maximum elements
        l = r = 0  # Left and right pointers of the sliding window
        
        # Iterate through the array
        while r < len(nums):
            # Remove smaller elements from the back of the deque
            # This maintains the deque in decreasing order of element values
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)  # Add current index to the deque
            
            # Remove the leftmost element if it's outside the current window
            if l > q[0]:
                q.popleft()
            
            # If we have a full window, add the maximum to the output
            if (r + 1) >= k:
                output.append(nums[q[0]])  # The front of the deque always has the maximum
                l += 1  # Move the left pointer of the window
            
            r += 1  # Move the right pointer of the window
        
        return output
```

# [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
### Steps
* Use a hashmap to store fruits in 
* We add fruits on right to the basket
	* if the basket is bigger than capacity
		* subtract the count from the right
		* if the left basket is empty remove it
		* move left pointer
	* increment right

#### Code
```python
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        baskets = {}
        l = 0
        for r in range(len(fruits)):
            baskets[fruits[r]] = 1 + baskets.get(fruits[r], 0)
            if len(baskets) > 2:
                baskets[fruits[l]] -= 1
                if baskets[fruits[l]] == 0:
                    del baskets[fruits[l]]  
                l += 1

        return r - l + 1
```

