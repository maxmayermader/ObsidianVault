## [252. Meeting Rooms](https://leetcode.com/problems/meeting-rooms/)

### Steps
- Imagine length of time as line
- sort the intervals
- if the end is in the next interval then false 
	- (end > begin)

#### Code
```python
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        intervals.sort()
        # print(intervals)
        for i in range(len(intervals)-1):
            if intervals[i][1] > intervals[i+1][0]:
                return False

        return True 
```

## [57. Insert Interval](https://leetcode.com/problems/insert-interval/)

### Steps
- - Iterate through the existing intervals
- If new interval ends before current interval starts:
    - Insert new interval
    - Add remaining intervals
    - Return result
- If new interval starts after current interval ends:
    - Add current interval to result
- If there's overlap:
    - Merge intervals by updating new interval's start/end
- After loop, add final new interval to result
- Return result list

#### Code
```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        res = []

        for i in range(len(intervals)):
            if newInterval[1] < intervals[i][0]:
                res.append(newInterval)
                return res + intervals[i:]
            elif newInterval[0] > intervals[i][1]:
                res.append(intervals[i])
            else:
                newInterval = [min(newInterval[0], intervals[i][0]), max(newInterval[1], intervals[i][1])]

        res.append(newInterval)
        return res
```

## [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)
### Steps
- Sort the arry by first value
- keep track of start and ending values
- if an end is greater than the next merge the two intervals
- if next is greater than end
	- append start and end to the array and get the new start and end

#### Code
```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        res = []
        start = intervals[0][0]
        end = intervals[0][1]
        for i in range(1, len(intervals)):
            if end >= intervals[i][0]:
                end = max(end, intervals[i][1])
            else:
                res.append([start, end])
                start = intervals[i][0]
                end = intervals[i][1]
        res.append([start, end])

        return res
        ```

## [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

### Steps
- Sort the array by start
- go through intervals
- if interval start is >= prevEnd then we don't worry
- if the prevEnd is greater than the start
	- incremnt res
	- get min the of the the ends
	----    ---
		----

#### Code
```Python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort()
        prevEnd = intervals[0][1]
        res = 0
        for start, end in intervals[1:]:
            if start >= prevEnd:
                prevEnd = end
            else:
                res += 1
                prevEnd = min(prevEnd, end)

        return res
```

## [253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)
### Steps
* (*You want to find the most overlapping meetings*)
* You have 2 arrays of start and end times
* Sort times in 1 array
* go through times
	* if start then increment count
	* if end then decrement count
	* set max count to res

#### Code
```python
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        time = []
        for start, end in intervals:
            time.append((start, 1))
            time.append((end, -1))
        
        time.sort()
        
        count = 0
        max_count = 0
        for t in time:
            count += t[1]
            max_count = max(max_count, count)
        return max_count
```
