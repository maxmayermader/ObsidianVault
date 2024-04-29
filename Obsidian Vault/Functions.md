#### Contents
* [[#Lambda]]
* [[#Comprehensions]]
* [[#Map,Filter,Reduce]]
* [[#Ternary]]
* [[#Any,All]]
* [[#Closures]]
* [[#Scope]]
Back to [[Python Documentation]]
## Lambda
```python
# lambda: <return_value>
# lambda <argument1>, <argument2>: <return_value>
```

```python
# Factorial
from functools import reduce
n = 3
factorial = reduce(lambda x, y: x*y, range(1, n+1))
print(factorial) #6
```

```python
# Fibonacci
fib = lambda n : n if n <= 1 else fib(n-1) + fib(n-2)
result = fib(10)
print(result) #55
```

## Comprehensions
```python
<list> = [i+1 for i in range(10)]         # [1, 2, ..., 10]
<set>  = {i for i in range(10) if i > 5}  # {6, 7, 8, 9}
<iter> = (i+5 for i in range(10))         # (5, 6, ..., 14)
<dict> = {i: i*2 for i in range(10)}      # {0: 0, 1: 2, ..., 9: 18}
```

```python
output = [i+j for i in range(3) for j in range(3)] # [0, 1, 2, 1, 2, 3, 2, 3, 4]

# Is the same as:
output = []
for i in range(3):
  for j in range(3):
    output.append(i+j)
```

## Map,Filter,Reduce
```python
from functools import reduce
list(map(lambda x: x + 1, range(10)))            # [1, 2, 3, 4, 5, 6, 7, 8, 9,10]
list(filter(lambda x: x > 5, range(10)))         # (6, 7, 8, 9)
reduce(lambda acc, x: acc + x, range(10))        # 45
```

## Ternary
```python
# <expression_if_true> if <condition> else <expression_if_false>

[a if a else 'zero' for a in [0, 1, 0, 3]] # ['zero', 1, 'zero', 3]
```
## Any,All
```python
any([False, True, False])# True if at least one item in collection is truthy, False if empty.
all([True,1,3,True])     # True if all items in collection are true
```
## Closures
```python
def get_multiplier(a):
    def out(b):
        return a * b
    return out
```

```python
>>> multiply_by_3 = get_multiplier(3)
>>> multiply_by_3(10)
30
```
## Scope
```python
ef get_counter():
    i = 0
    def out():
        nonlocal i
        i += 1
        return i
    return out
```

```python
>>> counter = get_counter()
>>> counter(), counter(), counter()
(1, 2, 3)
```