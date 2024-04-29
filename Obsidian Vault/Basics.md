### Contents
* [[#Comparison Operators]]
* [[#Logical Operators]]
* [[#Loops]]
* [[#Range]]
* [[#Heap]]
* [[#Enumerate]]
* [[#Counter]]
* [[#Named Tuple]]
* [[#OrderedDict]]
* [[#Class]]
* [[#Linked List]]
* [[#Trees]]

Back to [[Python Documentation]]

## Comparison Operators
```python
==                   # equal values
!=                   # not equal
>                    # left operand is greater than right operand
<                    # left operand is less than right operand
>=                   # left operand is greater than or equal to right operand
<=                   # left operand is less than or equal to right operand
<element> is <element> # check if two operands refer to same object in memory
```

## Logical Operators
```python
1 < 2 and 4 > 1 # True
1 > 3 or 4 > 1  # True
1 is not 4      # True
not True        # False
1 not in [2,3,4]# True

if <condition that evaluates to boolean>:
  # perform action1
elif <condition that evaluates to boolean>:
  # perform action2
else:
  # perform action3
```

## Loops
```python
my_list = [1,2,3]
my_tuple = (1,2,3)
my_list2 = [(1,2), (3,4), (5,6)]
my_dict = {'a': 1, 'b': 2. 'c': 3}

for num in my_list:
    print(num) # 1, 2, 3

for num in my_tuple:
    print(num) # 1, 2, 3

for num in my_list2:
    print(num) # (1,2), (3,4), (5,6)

for num in '123':
    print(num) # 1, 2, 3

for k,v in my_dict.items(): # Dictionary Unpacking
    print(k) # 'a', 'b', 'c'
    print(v) # 1, 2, 3

while <condition that evaluates to boolean>:
  # action
  if <condition that evaluates to boolean>:
    break # break out of while loop
  if <condition that evaluates to boolean>:
    continue # continue to the next line in the block
```

```python
# waiting until user quits
msg = ''
while msg != 'quit':
    msg = input("What should I do?")
    print(msg)
```

## Range
```python
range(10)          # range(0, 10) --> 0 to 9
range(1,10)        # range(1, 10)
list(range(0,10,2))# [0, 2, 4, 6, 8]
```

## Enumerate
```python
for i, el in enumerate('helloo'):
  print(f'{i}, {el}')
# 0, h
# 1, e
# 2, l
# 3, l
# 4, o
# 5, o
```

## Counter
```python
from collections import Counter
colors = ['red', 'blue', 'yellow', 'blue', 'red', 'blue']
counter = Counter(colors)# Counter({'blue': 3, 'red': 2, 'yellow': 1})
counter.most_common()[0] # ('blue', 3)
```

## Named Tuple
```python
from collections import namedtuple
Point = namedtuple('Point', 'x y')
p = Point(1, y=2)# Point(x=1, y=2)
p[0]             # 1
p.x              # 1
getattr(p, 'y')  # 2
p._fields        # Or: Point._fields #('x', 'y')
```

```python
from collections import namedtuple
Person = namedtuple('Person', 'name height')
person = Person('Jean-Luc', 187)
f'{person.height}'           # '187'
'{p.height}'.format(p=person)# '187'
```

## OrderedDict
```python
from collections import OrderedDict
# Store each person's languages, keeping # track of who responded first. 
programmers = OrderedDict()
programmers['Tim'] = ['python', 'javascript']
programmers['Sarah'] = ['C++']
programmers['Bia'] = ['Ruby', 'Python', 'Go']

for name, langs in programmers.items():
    print(name + '-->')
    for lang in langs:
      print('\t' + lang)
```

## Class
```python
class <name>:
    age = 80 # Class Object Attribute
    def __init__(self, a):
        self.a = a # Object Attribute

    @classmethod
    def get_class_name(cls):
        return cls.__name__
```
### Inheritance 
class Employee(Person): def **init**(self, name, age, staff_num): super().**init**(name, age) self.staff_num = staff_num
````text
h2 id="multiple-inheritance">Multiple Inheritance</h2>
```python
class A: pass
class B: pass
class C(A, B): pass
````

**MRO determines the order in which parent classes are traversed when searching for a method:**

```python
>>> C.mro()
[<class 'C'>, <class 'A'>, <class 'B'>, <class 'object'>]
```

## Heap
```python
import heapq # (minHeap by Default)

nums = [5, 7, 9, 1, 3]

heapq.heapify(nums) # converts list into heap. Can be converted back to list by list(nums).
heapq.heappush(nums,element) # Push an element into the heap
heapq.heappop(nums) # Pop an element from the heap
#heappush(heap, ele) :- This function is used to insert the element mentioned in its arguments into heap. The order is adjusted, so as heap structure is maintained.
#heappop(heap) :- This function is used to remove and return the smallest element from heap. The order is adjusted, so as heap structure is maintained.

# Other Methods Available in the Library
# Used to return the k largest elements from the iterable specified 
# The key is a function with that accepts single element from iterable,
# and the returned value from that function is then used to rank that element in the heap
heapq.nlargest(k, iterable, key = fun)
heapq.nsmallest(k, iterable, key = fun)
```
## Linked List
## Trees



Back to top [[#Contents]]