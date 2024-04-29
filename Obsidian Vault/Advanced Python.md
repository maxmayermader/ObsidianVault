#### Contents 
* [[#Modules]]
* [[#Iterators]]
* [[#Generators]]
* [[#Decorators]]
* [[#Exceptions]]
* [[#Command Line Arguments]]
* [[#File IO]]
* [[#Useful Libraries]]

## Modules
```python
if __name__ == '__main__': # Runs main() if file wasn't imported.
    main()
```

```python
import <module_name>
from <module_name> import <function_name>
import <module_name> as m
from <module_name> import <function_name> as m_function
from <module_name> import *
```
## Iterators
```python
<iter> = iter(<collection>)
<iter> = iter(<function>, to_exclusive)     # Sequence of return values until 'to_exclusive'.
<el>   = next(<iter> [, default])           # Raises StopIteration or returns 'default' on end.
```

## Generators
```python
def count(start, step):
    while True:
        yield start
        start += step
```

```python
>>> counter = count(10, 2)
>>> next(counter), next(counter), next(counter)
(10, 12, 14)
```

## Decorators
```python
@decorator_name
def function_that_gets_passed_to_decorator():
    ...
```
## Exceptions
```python
try:
  5/0
except ZeroDivisionError:
  print("No division by zero!")
```

```python
while True:
  try:
    x = int(input('Enter your age: '))
  except ValueError:
    print('Oops!  That was no valid number.  Try again...')
  else: # code that depends on the try block running successfully should be placed in the else block.
    print('Carry on!')
    break
```

## File IO
```python
<file> = open('<path>', mode='r', encoding=None)
```
#### Modes
- **`'r'` - Read (default).**
- **`'w'` - Write (truncate).**
- **`'x'` - Write or fail if the file already exists.**
- **`'a'` - Append.**
- **`'w+'` - Read and write (truncate).**
- **`'r+'` - Read and write from the start.**
- **`'a+'` - Read and write from the end.**
- **`'t'` - Text mode (default).**
- **`'b'` - Binary mode.**

####  File
```python
<file>.seek(0)                      # Moves to the start of the file.
```

```python
<str/bytes> = <file>.readline()     # Returns a line.
<list>      = <file>.readlines()    # Returns a list of lines.
```

```python
<file>.write(<str/bytes>)           # Writes a string or bytes object.
<file>.writelines(<list>)           # Writes a list of strings or bytes objects.
```

#### Read Text from File

```python
def read_file(filename):
    with open(filename, encoding='utf-8') as file:
        return file.readlines() # or read()

for line in read_file(filename):
  print(line)
```

#### Write Text to File
```python
def write_to_file(filename, text):
    with open(filename, 'w', encoding='utf-8') as file:
        file.write(text)
```

#### Append Text to File

```python
def append_to_file(filename, text):
    with open(filename, 'a', encoding='utf-8') as file:
        file.write(text)
```

## Useful Libraries
### Statistics 
```python
from statistics import mean, median, variance, pvariance, pstdev
```

### Random
```python
from random import random, randint, choice, shuffle
random() # random float between 0 and 1
randint(0, 100) # random integer between 0 and 100
random_el = choice([1,2,3,4]) # select a random element from list
shuffle([1,2,3,4]) # shuffles a list
```

### Datetime
- **Module 'datetime' provides 'date' `<D>`, 'time' `<T>`, 'datetime' `<DT>` and 'timedelta' `<TD>` classes. All are immutable and hashable.**
- **Time and datetime can be 'aware' `<a>`, meaning they have defined timezone, or 'naive' `<n>`, meaning they don't.**
- **If object is naive it is presumed to be in system's timezone.**

```python
from datetime import date, time, datetime, timedelta
from dateutil.tz import UTC, tzlocal, gettz
```

## Command Line Arguments
