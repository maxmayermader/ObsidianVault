# [704. Binary Search](https://leetcode.com/problems/binary-search/)
### Steps
- array is sorted so we can do divided and conquer
- if target > middle
	- look at right half
- else
	- look at left half
- do this until you find target or l == r

#### Code
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)-1
        while l <= r:
            m = l + ((r-l)//2)
            if nums[m] == target:
                return m
            if nums[m] < target:
                l = m + 1
                m = (r+l) // 2
            else:
                r = m - 1
                m = (r+l) // 2
        return -1
```

# [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)
### Steps
- search rows first by seeing if target could be in row
	- then do binary search on rows until you find target row
- then do normal binary search on row

#### Code
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rl, rr = 0, len(matrix) - 1
        rm = 0
        while rl <= rr:
            rm = rl + ((rr-rl )// 2)
            if matrix[rm][0] <= target <= matrix[rm][-1]:
                break
            if matrix[rm][0] > target:
                rr = rm - 1
            else:
                rl = rm + 1

        l, r = 0, len(matrix[rm])-1
        while l <= r:
            m = l + ((r-l)//2)
            if matrix[rm][m] == target:
                return True
            if matrix[rm][m] > target:
                r = m - 1
            else:
                l = m + 1

        return False
```

# [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
### Steps
- We want to find **K** bananas to eat per hour
- **K** can be 1 to max banana pile
- So do binary search and find minimum **K** to eat
- get total time to eat all the bananas
- if total time > time
	- took too long so move left
- else
	- move right
- adjust res

#### Code
```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        maxBanana = 1
        minBanana = 1
        for banana in piles:
            maxBanana = max(maxBanana, banana)
        res = 0
        while minBanana <= maxBanana:
            k = (maxBanana + minBanana)// 2

            time = 0
            for pile in piles:
                time += math.ceil(float(pile)/k)
            if time <= h:
                res = k
                maxBanana = k -1
            else:
                minBanana = k + 1
        return res
```

#
### Steps
- In a rotated sorted array (e.g., [4,5,6,1,2,3]), one half of the array will always be "normally sorted" while the other contains the rotation point (and minimum element)
- By comparing nums[mid] with nums[end], we can determine which half contains the minimum:
    - If nums[mid] > nums[end], the minimum must be in the right half (since a normally sorted array shouldn't have a larger number before a smaller one)
    - If nums[mid] ≤ nums[end], the minimum must be in the left half (including mid itself)
- We keep track of the minimum value seen so far (curr_min) while narrowing down the search space, ensuring we don't miss the minimum even if we pass over it during our binary search

#### Code
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        l, r = 0, len(nums)-1
        minNum = float('inf')
        while l <= r:
            m = (l + r) // 2
            minNum = min(minNum, nums[m])
            if nums[m] > nums[r]:
                l = m + 1
            else:
                r = m - 1
        return min(minNum, nums[0])
```

# [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
### Steps
- Check if the left <= mid (checking left)
	- If mid < target or left > target, move to the right (Mid could be bigger than left but left shouldn't be bigger than the target if it is sorted properly)
- Else (checking right portion because array has been rotated)
	- if mid > target or right < target, then move pointer left (mid should be smaller than right but shouldn't be smaller than the target)

#### Code
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)-1
        while l <= r:
            m = (r+l)//2
            if nums[m] == target:
                return m
            if nums[l] <= nums[m]:
                if nums[l] > target or nums[m] < target:
                    l = m + 1
                else:
                    r = m - 1
            else:
                if nums[r] < target or nums[m] > target:
                    r = m - 1
                else:
                    l = m + 1
```

# [981. Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)
### Steps
- store time and values in **HM**
- use binary search to get time
	- key may be empty
	- timestamp_prev <= timestamp
		- gets previous value even if you don't find target

#### Code
```python
class TimeMap:

    def __init__(self):
        self.hm = {}


    def set(self, key: str, value: str, timestamp: int) -> None:
        if key in self.hm:
            self.hm[key].append((timestamp, value))
        else:
            self.hm[key] = [(timestamp, value)]

    def get(self, key: str, timestamp: int) -> str:
        arr = self.hm.get(key,[])
        res = ""
        l,r = 0, len(arr)-1
        while l <= r:
            m = (l+r) //2
            if arr[m][0] <= timestamp:
                res = arr[m][1]
                l = m + 1
            else:
                r = m - 1
        return res
        


# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)
```
