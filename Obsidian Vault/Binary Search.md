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