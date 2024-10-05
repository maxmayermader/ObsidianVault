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

## [1851. Minimum Interval to Include Each Query](https://leetcode.com/problems/minimum-interval-to-include-each-query/)
### Steps
- Sort intervals
- Use hm for result so that indexes match result
- Use a heap to keep track of interval sizes and the end of the interval as well
- Loop through sorted queries
	- add all intervals to the pq that contain the query
	- pop all intervals that do not include the query
	- add the top interval from the heap to the res hm
- return maped result to query from res hm

#### Code
```python
class Solution:
    def minInterval(self, intervals: List[List[int]], queries: List[int]) -> List[int]:
        intervals.sort()
        res = {}
        i = 0
        pq = []

        for q in sorted(queries):
            while i < len(intervals) and q >= intervals[i][0]:
                heapq.heappush(pq, ((intervals[i][1]-intervals[i][0]+1), intervals[i][1]))
                i+=1
            
            while pq and q > pq[0][1]:
                heapq.heappop(pq)

            res[q] = pq[0][0] if pq else -1

        return [res[q] for q in queries]
```