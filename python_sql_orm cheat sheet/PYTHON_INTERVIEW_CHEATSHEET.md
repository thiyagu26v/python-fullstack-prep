---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# 🐍 PYTHON INTERVIEW CHEAT SHEET
## Complete Reference for Coding Rounds

---

## 📋 TABLE OF CONTENTS
1. [Python Keywords](#python-keywords)
2. [Built-in Functions](#built-in-functions)
3. [String Methods](#string-methods)
4. [List Methods](#list-methods)
5. [Dictionary Methods](#dictionary-methods)
6. [Set Methods](#set-methods)
7. [Tuple Methods](#tuple-methods)
8. [File Methods](#file-methods)
9. [Common Interview Patterns](#common-interview-patterns)

---

## 🔑 PYTHON KEYWORDS

### Control Flow Keywords

| Keyword | Purpose | Example |
|---------|---------|---------|
| `if` | Conditional execution | `if x > 5: print("Greater")` |
| `elif` | Additional condition | `elif x == 5: print("Equal")` |
| `else` | Default condition | `else: print("Less")` |
| `for` | Loop over iterable | `for i in range(5): print(i)` |
| `while` | Loop while condition true | `while x < 10: x += 1` |
| `break` | Exit loop early | `if x == 5: break` |
| `continue` | Skip to next iteration | `if x % 2 == 0: continue` |
| `pass` | Placeholder/no operation | `if True: pass` |

### Function & Class Keywords

| Keyword | Purpose | Example |
|---------|---------|---------|
| `def` | Define function | `def add(a, b): return a + b` |
| `return` | Return value from function | `return result` |
| `lambda` | Anonymous function | `square = lambda x: x**2` |
| `class` | Define class | `class Dog: pass` |
| `yield` | Generator function | `def gen(): yield 1` |

### Exception Handling Keywords

| Keyword | Purpose | Example |
|---------|---------|---------|
| `try` | Start exception block | `try: x = 1/0` |
| `except` | Handle exception | `except ZeroDivisionError: pass` |
| `finally` | Always execute | `finally: file.close()` |
| `raise` | Raise exception | `raise ValueError("Invalid")` |
| `assert` | Debug assertion | `assert x > 0, "Must be positive"` |

### Import Keywords

| Keyword | Purpose | Example |
|---------|---------|---------|
| `import` | Import module | `import math` |
| `from` | Import from module | `from math import sqrt` |
| `as` | Alias import | `import numpy as np` |

### Logical Keywords

| Keyword | Purpose | Example |
|---------|---------|---------|
| `and` | Logical AND | `if x > 0 and x < 10:` |
| `or` | Logical OR | `if x == 0 or x == 1:` |
| `not` | Logical NOT | `if not is_valid:` |
| `is` | Identity check | `if x is None:` |
| `in` | Membership test | `if 'a' in word:` |

### Variable Keywords

| Keyword | Purpose | Example |
|---------|---------|---------|
| `True` | Boolean true | `is_valid = True` |
| `False` | Boolean false | `is_valid = False` |
| `None` | Null value | `result = None` |
| `global` | Global variable | `global counter` |
| `nonlocal` | Enclosing scope variable | `nonlocal x` |

### Other Keywords

| Keyword | Purpose | Example |
|---------|---------|---------|
| `with` | Context manager | `with open('f.txt') as f:` |
| `async` | Async function | `async def fetch():` |
| `await` | Wait for async | `result = await fetch()` |
| `del` | Delete object | `del my_list[0]` |

---

## 🛠️ BUILT-IN FUNCTIONS

### Type Conversion Functions

```python
# int() - Convert to integer
int("123")          # 123
int(3.14)           # 3
int("1010", 2)      # 10 (binary to decimal)

# float() - Convert to float
float("3.14")       # 3.14
float(5)            # 5.0

# str() - Convert to string
str(123)            # "123"
str([1,2,3])        # "[1, 2, 3]"

# bool() - Convert to boolean
bool(0)             # False
bool(1)             # True
bool([])            # False
bool([1])           # True

# list() - Convert to list
list("abc")         # ['a', 'b', 'c']
list((1,2,3))       # [1, 2, 3]

# tuple() - Convert to tuple
tuple([1,2,3])      # (1, 2, 3)

# set() - Convert to set
set([1,2,2,3])      # {1, 2, 3}

# dict() - Create dictionary
dict(a=1, b=2)      # {'a': 1, 'b': 2}

# frozenset() - Immutable set
frozenset([1,2,3])  # frozenset({1, 2, 3})

# bytes() - Convert to bytes
bytes("hello", 'utf-8')  # b'hello'

# bytearray() - Mutable bytes
bytearray([65, 66])      # bytearray(b'AB')

# complex() - Complex number
complex(1, 2)       # (1+2j)

# ord() - Character to ASCII
ord('A')            # 65

# chr() - ASCII to character
chr(65)             # 'A'

# hex() - Convert to hexadecimal
hex(255)            # '0xff'

# oct() - Convert to octal
oct(8)              # '0o10'

# bin() - Convert to binary
bin(10)             # '0b1010'
```

### Mathematical Functions

```python
# abs() - Absolute value
abs(-5)             # 5
abs(-3.14)          # 3.14

# pow() - Power
pow(2, 3)           # 8
pow(2, 3, 5)        # 3 (2^3 % 5)

# round() - Round number
round(3.7)          # 4
round(3.14159, 2)   # 3.14

# sum() - Sum of iterable
sum([1,2,3,4])      # 10
sum([1,2,3], 10)    # 16 (with start value)

# max() - Maximum value
max([1,5,3])        # 5
max(1, 5, 3)        # 5
max("apple", "zebra")  # "zebra"

# min() - Minimum value
min([1,5,3])        # 1
min(1, 5, 3)        # 1

# divmod() - Division and modulo
divmod(17, 5)       # (3, 2)
```

### Sequence Functions

```python
# len() - Length of object
len([1,2,3])        # 3
len("hello")        # 5

# range() - Generate range
range(5)            # range(0, 5) -> 0,1,2,3,4
range(2, 8)         # 2,3,4,5,6,7
range(0, 10, 2)     # 0,2,4,6,8

# enumerate() - Add counter to iterable
for i, val in enumerate(['a','b','c']):
    print(i, val)   # 0 a, 1 b, 2 c

enumerate(['a','b'], start=1)  # (1,'a'), (2,'b')

# zip() - Combine iterables
list(zip([1,2], ['a','b']))  # [(1,'a'), (2,'b')]

# reversed() - Reverse iterator
list(reversed([1,2,3]))      # [3, 2, 1]

# sorted() - Sort iterable
sorted([3,1,2])              # [1, 2, 3]
sorted([3,1,2], reverse=True) # [3, 2, 1]
sorted(['apple','Zebra'], key=str.lower)  # ['apple','Zebra']

# filter() - Filter elements
list(filter(lambda x: x > 2, [1,2,3,4]))  # [3, 4]

# map() - Apply function
list(map(lambda x: x*2, [1,2,3]))  # [2, 4, 6]

# all() - All elements true
all([True, True, True])   # True
all([True, False])        # False
all([1, 2, 3])            # True

# any() - Any element true
any([False, False, True]) # True
any([0, 0, 0])            # False

# slice() - Create slice object
s = slice(1, 5, 2)
[1,2,3,4,5,6][s]          # [2, 4]
```

### Object & Attribute Functions

```python
# type() - Get type
type(123)           # <class 'int'>
type([])            # <class 'list'>

# isinstance() - Check instance
isinstance(5, int)           # True
isinstance('hi', (int,str))  # True

# issubclass() - Check subclass
issubclass(bool, int)        # True

# id() - Object identity
id(x)               # Memory address

# hash() - Hash value
hash("hello")       # Hash value
hash((1,2,3))       # Tuples are hashable

# dir() - List attributes
dir([])             # All list methods

# vars() - Object's __dict__
vars(obj)           # Object attributes

# getattr() - Get attribute
getattr(obj, 'name', 'default')

# setattr() - Set attribute
setattr(obj, 'name', 'value')

# hasattr() - Check attribute
hasattr(obj, 'name')         # True/False

# delattr() - Delete attribute
delattr(obj, 'name')

# callable() - Check if callable
callable(print)              # True
callable(5)                  # False

# property() - Create property
property(fget, fset, fdel, doc)
```

### Input/Output Functions

```python
# print() - Print to console
print("Hello")
print("a", "b", sep="-")     # a-b
print("test", end="")        # No newline

# input() - Get user input
name = input("Enter name: ")

# open() - Open file
f = open('file.txt', 'r')
f = open('file.txt', 'w')
f = open('file.txt', 'a')
f = open('file.txt', 'rb')   # Binary read

# format() - Format value
format(0.5, '%')             # '50.000000%'
format(255, 'x')             # 'ff' (hex)
```

### Iteration Functions

```python
# iter() - Create iterator
it = iter([1,2,3])

# next() - Get next item
next(it)            # 1
next(it)            # 2
next(it, 'default') # 3, then 'default'
```

### Compilation & Execution Functions

```python
# eval() - Evaluate expression
eval("2 + 3")       # 5
eval("len([1,2,3])") # 3

# exec() - Execute code
exec("x = 5")

# compile() - Compile source
code = compile("print('hi')", "", "exec")
exec(code)

# globals() - Global namespace
globals()           # Dict of global vars

# locals() - Local namespace
locals()            # Dict of local vars
```

### Class & Object Functions

```python
# object() - Base object
obj = object()

# super() - Parent class
super().__init__()

# classmethod() - Class method decorator
@classmethod
def method(cls):
    pass

# staticmethod() - Static method decorator
@staticmethod
def method():
    pass

# repr() - String representation
repr([1,2,3])       # '[1, 2, 3]'

# ascii() - ASCII representation
ascii('ñ')          # "'\\xf1'"

# memoryview() - Memory view
memoryview(b'abc')
```

### Other Useful Functions

```python
# help() - Get help
help(len)

# __import__() - Import module
math = __import__('math')
```

---

## 📝 STRING METHODS

```python
s = "Hello World"

# Case Conversion
s.upper()           # "HELLO WORLD"
s.lower()           # "hello world"
s.capitalize()      # "Hello world"
s.title()           # "Hello World"
s.swapcase()        # "hELLO wORLD"
s.casefold()        # "hello world" (aggressive lowercase)

# Searching & Checking
s.find('o')         # 4 (first occurrence)
s.find('x')         # -1 (not found)
s.rfind('o')        # 7 (last occurrence)
s.index('o')        # 4 (raises ValueError if not found)
s.count('l')        # 3
s.startswith('He')  # True
s.endswith('ld')    # True

# Validation
s.isalpha()         # False (has space)
s.isdigit()         # False
s.isalnum()         # False
s.isspace()         # False
s.isupper()         # False
s.islower()         # False
s.istitle()         # True
s.isascii()         # True
s.isdecimal()       # False
s.isnumeric()       # False
s.isidentifier()    # False
s.isprintable()     # True

# Splitting & Joining
s.split()           # ['Hello', 'World']
s.split('o')        # ['Hell', ' W', 'rld']
s.rsplit('o', 1)    # ['Hello W', 'rld'] (right split)
s.splitlines()      # Split by line breaks
'-'.join(['a','b']) # 'a-b'

# Trimming
s.strip()           # Remove leading/trailing whitespace
s.lstrip()          # Remove leading whitespace
s.rstrip()          # Remove trailing whitespace
s.strip('Hd')       # Remove specified characters

# Replacing
s.replace('World', 'Python')    # "Hello Python"
s.replace('l', 'L', 2)          # Replace first 2 occurrences

# Padding & Alignment
s.center(20)        # "    Hello World     "
s.center(20, '-')   # "----Hello World-----"
s.ljust(20)         # "Hello World         "
s.rjust(20)         # "         Hello World"
s.zfill(20)         # "000000000Hello World"

# Partitioning
s.partition(' ')    # ('Hello', ' ', 'World')
s.rpartition(' ')   # ('Hello', ' ', 'World')

# Encoding
s.encode('utf-8')   # b'Hello World'

# Formatting
"Hello {}".format("World")           # "Hello World"
"x={x}, y={y}".format(x=1, y=2)      # "x=1, y=2"
f"2 + 2 = {2+2}"                     # "2 + 2 = 4" (f-string)

# Translation
trans = str.maketrans('aeiou', '12345')
"hello".translate(trans)             # "h2ll4"

# Expanding Tabs
"a\tb".expandtabs(4)                 # "a   b"
```

---

## 📚 LIST METHODS

```python
lst = [1, 2, 3]

# Adding Elements
lst.append(4)           # [1, 2, 3, 4]
lst.extend([5, 6])      # [1, 2, 3, 4, 5, 6]
lst.insert(0, 0)        # [0, 1, 2, 3, 4, 5, 6]

# Removing Elements
lst.remove(0)           # [1, 2, 3, 4, 5, 6] (removes first occurrence)
lst.pop()               # 6 (returns and removes last)
lst.pop(0)              # 1 (returns and removes at index)
lst.clear()             # []

# Searching
lst = [1, 2, 3, 2, 1]
lst.index(2)            # 1 (first occurrence)
lst.index(2, 2)         # 3 (search from index 2)
lst.count(1)            # 2

# Sorting & Reversing
lst.sort()              # Sort in place
lst.sort(reverse=True)  # Sort descending
lst.sort(key=lambda x: -x)  # Custom sort
lst.reverse()           # Reverse in place

# Copying
lst2 = lst.copy()       # Shallow copy
```

### List Comprehensions (Important for Interviews!)

```python
# Basic comprehension
[x**2 for x in range(5)]                    # [0, 1, 4, 9, 16]

# With condition
[x for x in range(10) if x % 2 == 0]        # [0, 2, 4, 6, 8]

# Nested comprehension
[[i*j for j in range(3)] for i in range(3)] # [[0,0,0], [0,1,2], [0,2,4]]

# Multiple conditions
[x for x in range(20) if x % 2 == 0 if x % 3 == 0]  # [0, 6, 12, 18]

# With else
[x if x > 5 else 0 for x in range(10)]      # [0,0,0,0,0,0,6,7,8,9]
```

---

## 📖 DICTIONARY METHODS

```python
d = {'a': 1, 'b': 2}

# Accessing Elements
d.get('a')              # 1
d.get('c', 0)           # 0 (default value)
d['a']                  # 1 (raises KeyError if not found)

# Adding/Updating
d.update({'c': 3})      # {'a': 1, 'b': 2, 'c': 3}
d.update(d=4, e=5)      # Can use keyword args
d.setdefault('f', 6)    # Get value, set if not exists

# Removing
d.pop('a')              # 1 (returns and removes)
d.pop('x', None)        # None (with default)
d.popitem()             # ('e', 5) (removes last item in 3.7+)
d.clear()               # {}

# Views
d = {'a': 1, 'b': 2, 'c': 3}
d.keys()                # dict_keys(['a', 'b', 'c'])
d.values()              # dict_values([1, 2, 3])
d.items()               # dict_items([('a',1), ('b',2), ('c',3)])

# Copying
d2 = d.copy()           # Shallow copy

# Merging (Python 3.9+)
d1 = {'a': 1}
d2 = {'b': 2}
d3 = d1 | d2            # {'a': 1, 'b': 2}

# From keys
dict.fromkeys(['a','b'], 0)  # {'a': 0, 'b': 0}
```

### Dictionary Comprehensions

```python
# Basic comprehension
{x: x**2 for x in range(5)}              # {0:0, 1:1, 2:4, 3:9, 4:16}

# With condition
{x: x**2 for x in range(10) if x % 2 == 0}

# From two lists
keys = ['a', 'b', 'c']
values = [1, 2, 3]
{k: v for k, v in zip(keys, values)}     # {'a':1, 'b':2, 'c':3}

# Swap keys and values
{v: k for k, v in {'a': 1, 'b': 2}.items()}  # {1:'a', 2:'b'}
```

---

## 🎯 SET METHODS

```python
s = {1, 2, 3}

# Adding Elements
s.add(4)                # {1, 2, 3, 4}
s.update([5, 6])        # {1, 2, 3, 4, 5, 6}
s.update([7], {8})      # Can add multiple iterables

# Removing Elements
s.remove(1)             # KeyError if not found
s.discard(1)            # No error if not found
s.pop()                 # Remove and return arbitrary element
s.clear()               # set()

# Set Operations
s1 = {1, 2, 3}
s2 = {3, 4, 5}

# Union
s1.union(s2)            # {1, 2, 3, 4, 5}
s1 | s2                 # Same as union

# Intersection
s1.intersection(s2)     # {3}
s1 & s2                 # Same as intersection

# Difference
s1.difference(s2)       # {1, 2}
s1 - s2                 # Same as difference

# Symmetric Difference
s1.symmetric_difference(s2)  # {1, 2, 4, 5}
s1 ^ s2                 # Same as symmetric difference

# Update Methods
s1.intersection_update(s2)      # s1 = s1 & s2
s1.difference_update(s2)        # s1 = s1 - s2
s1.symmetric_difference_update(s2)  # s1 = s1 ^ s2

# Checking
s1.issubset(s2)         # s1 <= s2
s1.issuperset(s2)       # s1 >= s2
s1.isdisjoint(s2)       # No common elements

# Copying
s2 = s1.copy()          # Shallow copy
```

### Set Comprehensions

```python
# Basic comprehension
{x**2 for x in range(5)}                # {0, 1, 4, 9, 16}

# With condition
{x for x in range(10) if x % 2 == 0}    # {0, 2, 4, 6, 8}
```

---

## 📦 TUPLE METHODS

```python
t = (1, 2, 3, 2, 1)

# Count occurrences
t.count(1)              # 2

# Find index
t.index(2)              # 1 (first occurrence)
t.index(2, 2)           # 3 (search from index 2)

# Tuples are immutable - no add/remove methods!
# Convert to list to modify, then back to tuple
```

### Tuple Unpacking (Important!)

```python
# Basic unpacking
a, b, c = (1, 2, 3)

# With *
a, *b, c = (1, 2, 3, 4, 5)  # a=1, b=[2,3,4], c=5

# Swap values
a, b = b, a

# Enumerate unpacking
for i, val in enumerate(['a', 'b', 'c']):
    print(i, val)
```

---

## 📄 FILE METHODS

```python
f = open('file.txt', 'r')

# Reading
f.read()                # Read entire file
f.read(10)              # Read 10 characters
f.readline()            # Read one line
f.readlines()           # Read all lines as list

# Writing
f = open('file.txt', 'w')
f.write("Hello")        # Write string
f.writelines(['a\n', 'b\n'])  # Write list of strings

# Position
f.tell()                # Current position
f.seek(0)               # Move to beginning
f.seek(10, 0)           # Move to position 10 from start

# Closing
f.close()

# Better: Use context manager
with open('file.txt', 'r') as f:
    content = f.read()
# File automatically closed

# File Modes
# 'r'  - Read (default)
# 'w'  - Write (overwrites)
# 'a'  - Append
# 'x'  - Exclusive creation
# 'b'  - Binary mode
# 't'  - Text mode (default)
# '+'  - Update (read and write)

# Other methods
f.flush()               # Flush buffer
f.fileno()              # File descriptor
f.isatty()              # Is terminal device
f.readable()            # Is readable
f.writable()            # Is writable
f.seekable()            # Is seekable
```
## 💡 USEFUL BUILT-IN MODULES FOR INTERVIEWS

### collections

```python
from collections import Counter, defaultdict, deque, OrderedDict, namedtuple

# Counter - Count elements
Counter(['a', 'b', 'a', 'c'])  # Counter({'a': 2, 'b': 1, 'c': 1})

# defaultdict - Default values
dd = defaultdict(int)
dd['key'] += 1  # No KeyError

# deque - Double-ended queue
dq = deque([1, 2, 3])
dq.appendleft(0)    # deque([0, 1, 2, 3])
dq.popleft()        # 0

# namedtuple - Named tuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
print(p.x, p.y)
```

### itertools

```python
from itertools import permutations, combinations, product, chain

# Permutations
list(permutations([1,2,3], 2))  # [(1,2), (1,3), (2,1), (2,3), (3,1), (3,2)]

# Combinations
list(combinations([1,2,3], 2))  # [(1,2), (1,3), (2,3)]

# Product (Cartesian product)
list(product([1,2], ['a','b']))  # [(1,'a'), (1,'b'), (2,'a'), (2,'b')]

# Chain (Flatten)
list(chain([1,2], [3,4]))       # [1, 2, 3, 4]
```

### heapq (Priority Queue)

```python
import heapq

# Min heap
heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)
heapq.heappop(heap)  # 1

# Heapify
nums = [3, 1, 4, 1, 5]
heapq.heapify(nums)  # [1, 1, 4, 3, 5]

# N largest/smallest
heapq.nlargest(3, [1,2,3,4,5])   # [5, 4, 3]
heapq.nsmallest(3, [1,2,3,4,5])  # [1, 2, 3]
```

### math

```python
import math

math.ceil(3.2)      # 4
math.floor(3.8)     # 3
math.sqrt(16)       # 4.0
math.factorial(5)   # 120
math.gcd(12, 8)     # 4
math.lcm(12, 8)     # 24 (Python 3.9+)
math.pow(2, 3)      # 8.0
math.log(8, 2)      # 3.0
math.pi             # 3.141592653589793
math.e              # 2.718281828459045
```

### re (Regular Expressions)

```python
import re

# Match
re.match(r'\d+', '123abc')      # Match from start

# Search
re.search(r'\d+', 'abc123')     # Search anywhere

# Find all
re.findall(r'\d+', 'a1b2c3')    # ['1', '2', '3']

# Replace
re.sub(r'\d+', 'X', 'a1b2c3')   # 'aXbXcX'

# Split
re.split(r'\s+', 'a  b   c')    # ['a', 'b', 'c']
```

---

## 🚀 TIME & SPACE COMPLEXITY QUICK REFERENCE

### Common Time Complexities

| Complexity | Name | Example |
|------------|------|---------|
| O(1) | Constant | Array access, hash lookup |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search, single loop |
| O(n log n) | Log-linear | Merge sort, heap sort |
| O(n²) | Quadratic | Nested loops, bubble sort |
| O(2ⁿ) | Exponential | Recursive fibonacci |
| O(n!) | Factorial | Permutations |

### When to Use What Data Structure

| Use Case | Data Structure |
|----------|---------------|
| Fast lookup by key | Dictionary / Hash Map |
| Unique elements | Set |
| Ordered unique elements | Sorted list or OrderedDict |
| LIFO (Last In First Out) | List as Stack |
| FIFO (First In First Out) | deque as Queue |
| Priority Queue | heapq |
| Fast insertion/deletion at both ends | deque |
| Immutable sequence | Tuple |
| Frequency counting | Counter |

---

## ✅ INTERVIEW TIPS

1. **Always clarify the problem** before coding
2. **Think out loud** - explain your thought process
3. **Start with brute force**, then optimize
4. **Test with edge cases**: empty input, single element, duplicates
5. **Analyze time and space complexity** after solving
6. **Use meaningful variable names**
7. **Consider using built-in functions** when appropriate
8. **Practice common patterns**: two pointers, sliding window, hash maps, etc.

---

**Good luck with your Python interviews! 🎯**


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
