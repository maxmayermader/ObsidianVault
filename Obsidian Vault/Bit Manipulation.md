# [136. Single Number](https://leetcode.com/problems/single-number/)
### Steps
* - If we take XOR of zero and some bit, it will return that bit
    - a⊕0=a
- If we take XOR of two same bits, it will return 0
    - a⊕a=0
- a⊕b⊕a=(a⊕a)⊕b=0⊕b=b

#### Code
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0
        for num in nums:
            res = num ^ res
        return res
```

# [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)
### Steps
* while n
	* Set most significant bit to 0
	* increment count
* return count

#### Code
```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0
        while n:
            n &= n - 1
            res += 1
        return res
```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

# 
### Steps
* 

#### Code
```python

```

