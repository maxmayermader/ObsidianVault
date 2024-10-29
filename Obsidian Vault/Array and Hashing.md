#### [[Templates]]

# [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
### Steps
* Use *HM*, if you find a value in the *HM*, then there is a duplicate

#### Code 
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        # return len(nums) != len(set(nums))  One line sol
        hm = {}
        for num in nums:
            if num in hm:
                return True
            hm[num] = 1 + hm.get(num,0)

        return False
```

# [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
### Steps
- Use *HM* to store each chars and counts. If *HM* are not the same then False

#### Code
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        hm1, hm2 = {}, {}

        for i in range(len(s)):
            hm1[s[i]] = 1 + hm1.get(s[i], 0)
            hm2[t[i]] = 1 + hm2.get(t[i], 0)
        return hm1 == hm2
```

# [1. Two Sum](https://leetcode.com/problems/two-sum/)
### Steps
- Use *HM* store the target - sum. If you a value that's in the *HM* return true.

#### Code
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hm = {}
        for i in range(len(nums)):
            if nums[i] in hm:
                return [hm[nums[i]], i]
            else:
                hm[target-nums[i]] = i
```

# [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)
### Steps
- Use a *HM* and store the count of each a-z char as key and create a list of words that have the same key. Return values.

#### Code
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list)
        for s in strs:
            count = [0]*26
            for c in s:
                count[ord(c) - ord('a')] += 1
            res[tuple(count)].append(s)

        return res.values()
```

# [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
### Steps
- Create a *HM* to count the freq of each el
- Create a nested list where the indices correspond the freq of each el
- Traverse the nested list in reverse order adding each el to res until res == k

#### Code
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        freq = [[] for i in range(len(nums) + 1)]

        for n in nums:
            count[n] = 1 + count.get(n, 0)
        for n, c in count.items():
            freq[c].append(n)

        res = []
        for i in range(len(freq) - 1, 0, -1):
            res += freq[i]
            if len(res) == k:
                return res
```

# [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
### Steps
- First pass: Iterate forward, calculating prefix products. Each element stores the product of all numbers before it.
- Second pass: Iterate backward, maintaining a running postfix product. Multiply each element by the postfix to get the final result.

#### Code
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1] * (len(nums))

        for i in range(1, len(nums)):
            res[i] = res[i-1] * nums[i-1]
        postfix = 1
        for i in range(len(nums) - 1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]
        return res
```



# [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)
### Steps
- Use *HM* with *Hash Set* to store values in rows, cols and 3x3 squares ensuring that the same value is not already present in the row, col or square

#### Code
```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = defaultdict(set)
        cols = defaultdict(set)
        diags = defaultdict(set)
        
        for i in range(len(board)):
            for j in range(len(board)):
                if board[i][j] != '.':
                    if (board[i][j] in rows[i] or
                        board[i][j] in cols[j] or
                        board[i][j] in diags[(i//3, j//3)]):
                        return False

                    rows[i].add(board[i][j])
                    cols[j].add(board[i][j])
                    diags[((i//3), (j//3))].add(board[i][j])

        return True    
```




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


        return maxSeq #O(n+n+n)
```

## [271. Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/)
### Steps
- Encode:
    - Convert each string to "length:string" format
    - Concatenate all these formatted strings
- Decode:
    - Iterate through the encoded string
    - For each section, extract the length, then the corresponding string
    - Add each extracted string to the result list
- Key idea: Use string length as a prefix to eliminate need for delimiters

#### Code
```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        return "".join(f'{len(s)}:{s}' for s in strs)

    def decode(self, s: str) -> List[str]:
        result, i = [], 0
        while i < len(s):
            j = s.find(':', i)
            length = int(s[i:j])
            result.append(s[j+1:j+1+length])
            i = j + 1 + length
        return result
```

#   [2501. Longest Square Streak in an Array](https://leetcode.com/problems/longest-square-streak-in-an-array/)
### Steps
* Use a **set** to store all the numbers from the array 
* Loop through the array and treat each number as the starting point of a streak. 
	* Searching for the square of the previous number in the sequence  
	* The longest streak we find by counting how many times the inner loop runs gives us the desired result.

#### Code
```python
class Solution:
    def longestSquareStreak(self, nums: List[int]) -> int:
        hs = set(nums)
        res = 0
        streak = 0
        for n in hs:
            streak = 0
            v = n
            while v in hs:
                streak += 1
                if v**2 > 10**5:
                    break
                v*=v

            res = max(res, streak)

        return res if res > 1 else -1
```

