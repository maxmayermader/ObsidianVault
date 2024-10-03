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