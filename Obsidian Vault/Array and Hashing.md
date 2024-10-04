## [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
### Steps
- save array as set
- go through elements in set
	- if there is an element  - 1 in the set (always looking for the beginning of sub seq)
		- then keep finding consecutive sequences
	- set new max

#### Code
```Python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        hs = set(nums)
        if not nums:
            return 0

        maxSeq = 0

        for el in hs:
            if el - 1 not in hs:
                cur = el
                seq = 1

                while cur + 1 in hs:
                    cur += 1
                    seq += 1
                
                maxSeq = max(seq, maxSeq)


        return maxSeq
        #O(n+n+n)
```



