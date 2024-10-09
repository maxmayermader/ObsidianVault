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

