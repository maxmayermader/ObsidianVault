#### [[Templates]]

# [15. 3Sum](https://leetcode.com/problems/3sum/)
### Steps
- Sort the input array in ascending order.
- Iterate through the array with index i, using each element as a potential first number of the triplet.
- For each i, use two pointers (l and r) to scan the remaining subarray for complementary pairs.
- Move l right if the sum is too small, move r left if the sum is too large.
- When a valid triplet is found, add it to the result and skip duplicates for l and r.
- Use early termination: break the outer loop if nums[i] > 0, as sorted positives can't sum to zero.

#### Code
```python title:3sum
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []

        for i, e in enumerate(nums):
            if e > 0:
                break
            if i > 0 and e == nums[i-1]:
                continue

            l = i+1
            r = len(nums)-1

            while l < r:
                total = nums[i] + nums[l] + nums[r]
                if total == 0:
                    res.append([nums[i], nums[l], nums[r]])
                    while l < r and nums[l] == nums[l+1]:
                        l += 1
                    while l < r and nums[r] == nums[r-1]:
                        r -= 1
                    l += 1
                    r -= 1
                elif total < 0:
                    l += 1
                else:
                    r -= 1
        return res
```

# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
### Steps
- Have a left & right pointer
- Keep track of maxWater which is the area of the minHeight of two pointers and their distance.

#### Code
```python title:ContainerWithMostWater
class Solution:
    def maxArea(self, height: List[int]) -> int:
        maxRain = 0
        l = 0
        r = len(height) - 1

        while l < r:
            minHeight = min(height[l], height[r])
            maxRain = max(maxRain, minHeight*(r-l))

            if height[l] < height[r]:
                l += 1
            else:
                r -= 1

        return maxRain
```

