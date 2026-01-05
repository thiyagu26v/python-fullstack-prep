---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# 🐍 Top 50 Practical Python Interview Questions: Part 2 (Slightly Advanced)
*Strengthen your skills with new logic problems, edge cases, and foundational OOPS*

---

## **Section 1: Python Basics (Q1-10)**

### **1. Check if a number is an Armstrong Number**
*An Armstrong number of three digits is an integer such that the sum of the cubes of its digits is equal to the number itself.*

**Sample Input:** `153`
**Sample Output:** `True` (1³ + 5³ + 3³ = 1 + 125 + 27 = 153)

#### **Approach 1: Mathematical Logic (Recommended)**
```python
num = 153
sum_val = 0
temp = num
# Find number of digits
n = len(str(num))

while temp > 0:
    digit = temp % 10
    sum_val += digit ** n
    temp //= 10

if num == sum_val:
    print(True)
else:
    print(False)
```

#### **Approach 2: String Comprehension**
```python
num = 153
n = len(str(num))
# Calculate sum using generator expression
print(num == sum(int(digit) ** n for digit in str(num)))
```

---

### **2. Find the GCD (Greatest Common Divisor) of two numbers**

**Sample Input:** `12, 18`
**Sample Output:** `6`

#### **Approach 1: Using Euclidean Algorithm (Recursive)**
```python
def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)

print(gcd(12, 18))
```

#### **Approach 2: Using `math` Module**
```python
import math
print(math.gcd(12, 18))
```

---

### **3. Check if a number is a Perfect Number**
*A perfect number is a positive integer that is equal to the sum of its proper divisors (excluding itself).*

**Sample Input:** `28` (1+2+4+7+14 = 28)
**Sample Output:** `True`

#### **Approach 1: Iterative Check**
```python
num = 28
sum_div = 0
for i in range(1, num):
    if num % i == 0:
        sum_div += i

print(num == sum_div)
```

---

### **4. Calculate the power of a number without using `**` or `pow()`**

**Sample Input:** `base = 2, exp = 3`
**Sample Output:** `8`

#### **Approach 1: Using a Loop**
```python
base, exp = 2, 3
result = 1
for _ in range(exp):
    result *= base
print(result)
```

---

### **5. Count the number of digits in an integer**

**Sample Input:** `12345`
**Sample Output:** `5`

#### **Approach 1: Using `str()` and `len()`**
```python
num = 12345
print(len(str(abs(num)))) # abs handles negative numbers
```

#### **Approach 2: Using `while` loop**
```python
num = 12345
count = 0
temp = abs(num)
if temp == 0: count = 1
while temp > 0:
    temp //= 10
    count += 1
print(count)
```

---

### **6. Find all divisors of a number**

**Sample Input:** `12`
**Sample Output:** `[1, 2, 3, 4, 6, 12]`

#### **Approach 1: Basic Loop**
```python
num = 12
divisors = [i for i in range(1, num + 1) if num % i == 0]
print(divisors)
```

---

### **7. Check if a number is a Palindrome without string conversion**

**Sample Input:** `121`
**Sample Output:** `True`

#### **Approach 1: Reversing the integer mathematically**
```python
num = 121
temp = num
rev = 0
while temp > 0:
    rev = (rev * 10) + (temp % 10)
    temp //= 10

print(num == rev)
```

---

### **8. Print all prime numbers in an interval**

**Sample Input:** `10, 20`
**Sample Output:** `11, 13, 17, 19`

#### **Approach 1: Nested Loops**
```python
start, end = 10, 20
primes = []
for num in range(start, end + 1):
    if num > 1:
        for i in range(2, int(num**0.5) + 1):
            if num % i == 0:
                break
        else:
            primes.append(num)
print(primes)
```

---

### **9. Find the sum of digits of a number**

**Sample Input:** `123`
**Sample Output:** `6`

#### **Approach 1: Mathematical**
```python
num = 123
total = 0
while num > 0:
    total += num % 10
    num //= 10
print(total)
```

---

### **10. Compute the LCM (Least Common Multiple) of two numbers**

**Sample Input:** `12, 18`
**Sample Output:** `36`

#### **Approach 1: Using the formula (LCM * GCD = a * b)**
```python
import math
a, b = 12, 18
lcm = abs(a * b) // math.gcd(a, b)
print(lcm)
```

---

## **Section 2: Strings (Q11-18)**

### **11. Check if one string is a rotation of another**
**Sample Input:** `"abcde"`, `"cdeab"`
**Sample Output:** `True`

#### **Approach 1: Concatenation Trick**
```python
s1, s2 = "abcde", "cdeab"
is_rotation = len(s1) == len(s2) and s2 in (s1 + s1)
print(is_rotation)
```

---

### **12. Remove all occurrences of a specific character from a string**

**Sample Input:** `"hello world"`, char = `'l'`
**Sample Output:** `"heo word"`

#### **Approach 1: Using `replace()`**
```python
text = "hello world"
print(text.replace('l', ''))
```

#### **Approach 2: Using Generator Expression**
```python
text = "hello world"
print("".join(c for c in text if c != 'l'))
```

---

### **13. Check if a string is a valid Anagram (Advanced Variation)**
*Ignore case and spaces.*

**Sample Input:** `"Listen"`, `"Silent"`
**Sample Output:** `True`

#### **Approach 1: Sorting**
```python
s1, s2 = "Listen", "Silent"
print(sorted(s1.lower()) == sorted(s2.lower()))
```

---

### **14. Count the number of words in a sentence**

**Sample Input:** `"Python is amazing"`
**Sample Output:** `3`

#### **Approach 1: Using `split()`**
```python
sentence = "Python is amazing"
print(len(sentence.split()))
```

---

### **15. Find the longest word in a sentence**

**Sample Input:** `"I love programming in Python"`
**Sample Output:** `"programming"`

#### **Approach 1: Using `max()` with `key=len`**
```python
sentence = "I love programming in Python"
longest = max(sentence.split(), key=len)
print(longest)
```

---

### **16. Check if a string contains balanced parentheses**
*Simplified: Only checking for `(` and `)`.*

**Sample Input:** `"(())()"`
**Sample Output:** `True`

#### **Approach 1: Using a counter**
```python
s = "(())()"
count = 0
is_balanced = True
for char in s:
    if char == '(': count += 1
    elif char == ')': count -= 1
    if count < 0: 
        is_balanced = False
        break

if count != 0: is_balanced = False
print(is_balanced)
```

---

### **17. Capitalize the first and last letter of each word**

**Sample Input:** `"hello world"`
**Sample Output:** `"HellO WorlD"`

#### **Approach 1: Slicing Mastery**
```python
s = "hello world"
result = " ".join(w[0].upper() + w[1:-1] + w[-1].upper() if len(w) > 1 else w.upper() for w in s.split())
print(result)
```

---

### **18. Find the frequency of each word in a string**

**Sample Input:** `"apple banana apple cherry"`
**Sample Output:** `{'apple': 2, 'banana': 1, 'cherry': 1}`

#### **Approach 1: Using `Counter`**
```python
from collections import Counter
s = "apple banana apple cherry"
print(dict(Counter(s.split())))
```

---

## **Section 3: Lists (Q19-28)**

### **19. Find the missing number in a range from 1 to n**

**Sample Input:** `[1, 2, 4, 5, 6]`, n=6
**Sample Output:** `3`

#### **Approach 1: sum formula**
```python
nums = [1, 2, 4, 5, 6]
n = 6
total_sum = n * (n + 1) // 2
print(total_sum - sum(nums))
```

---

### **20. Move all zeros to the end of a list**

**Sample Input:** `[0, 1, 0, 3, 12]`
**Sample Output:** `[1, 3, 12, 0, 0]`

#### **Approach 1: Filtering and Concatenating**
```python
nums = [0, 1, 0, 3, 12]
non_zeros = [x for x in nums if x != 0]
zeros = [0] * (len(nums) - len(non_zeros))
print(non_zeros + zeros)
```

---

### **21. Find the occurrence of an element in a list without `count()`**

**Sample Input:** `[1, 2, 3, 2, 4, 2]`, target = 2
**Sample Output:** `3`

#### **Approach 1: Simple Loop**
```python
nums = [1, 2, 3, 2, 4, 2]
target = 2
c = 0
for n in nums:
    if n == target: c += 1
print(c)
```

---

### **22. Find the cumulative sum of a list**

**Sample Input:** `[1, 2, 3, 4]`
**Sample Output:** `[1, 3, 6, 10]`

#### **Approach 1: Iterative**
```python
nums = [1, 2, 3, 4]
res = []
total = 0
for n in nums:
    total += n
    res.append(total)
print(res)
```

---

### **23. Find the median of a list**

**Sample Input:** `[3, 1, 2, 4, 5]`
**Sample Output:** `3`

#### **Approach 1: Sorting and Indexing**
```python
nums = [3, 1, 2, 4, 5]
nums.sort()
n = len(nums)
if n % 2 != 0:
    median = nums[n // 2]
else:
    median = (nums[n // 2 - 1] + nums[n // 2]) / 2
print(median)
```

---

### **24. Partition a list into even and odd numbers**

**Sample Input:** `[1, 2, 3, 4, 5, 6]`
**Sample Output:** `Evens: [2, 4, 6], Odds: [1, 3, 5]`

#### **Approach 1: List Comprehension**
```python
nums = [1, 2, 3, 4, 5, 6]
evens = [x for x in nums if x % 2 == 0]
odds = [x for x in nums if x % 2 != 0]
print(f"Evens: {evens}, Odds: {odds}")
```

---

### **25. Sort a list based on the length of elements**

**Sample Input:** `["apple", "go", "banana", "kiwi"]`
**Sample Output:** `["go", "kiwi", "apple", "banana"]`

#### **Approach 1: Using `sort(key=len)`**
```python
fruits = ["apple", "go", "banana", "kiwi"]
fruits.sort(key=len)
print(fruits)
```

---

### **26. Find the difference between two lists (Elements in A but not in B)**

**Sample Input:** `[1, 2, 3]`, `[2, 4]`
**Sample Output:** `[1, 3]`

#### **Approach 1: Set difference**
```python
a = [1, 2, 3]
b = [2, 4]
print(list(set(a) - set(b)))
```

---

### **27. Generate a list of squares of even numbers using List Comprehension**

**Sample Input:** `range(1, 11)`
**Sample Output:** `[4, 16, 36, 64, 100]`

```python
res = [x**2 for x in range(1, 11) if x % 2 == 0]
print(res)
```

---

### **28. Check if a list is sorted**

**Sample Input:** `[1, 2, 3, 5, 4]`
**Sample Output:** `False`

#### **Approach 1: Comparing with sorted version**
```python
nums = [1, 2, 3, 5, 4]
print(nums == sorted(nums))
```

---

## **Section 4: Dictionaries (Q29-35)**

### **29. Find common keys in two dictionaries**

**Sample Input:** `{'a': 1, 'b': 2}`, `{'b': 3, 'c': 4}`
**Sample Output:** `['b']`

#### **Approach 1: Set Intersection on keys**
```python
d1 = {'a': 1, 'b': 2}
d2 = {'b': 3, 'c': 4}
print(list(d1.keys() & d2.keys()))
```

---

### **30. Combine two dictionaries by summing values for common keys**

**Sample Input:** `d1 = {'a': 100, 'b': 200}`, `d2 = {'a': 50, 'c': 30}`
**Sample Output:** `{'a': 150, 'b': 200, 'c': 30}`

#### **Approach 1: Iterating and Updating**
```python
d1 = {'a': 100, 'b': 200}
d2 = {'a': 50, 'c': 30}
res = d1.copy()
for k, v in d2.items():
    res[k] = res.get(k, 0) + v
print(res)
```

---

### **31. Convert two lists into a dictionary**

**Sample Input:** `keys = ['name', 'age']`, `values = ['Alice', 25]`
**Sample Output:** `{'name': 'Alice', 'age': 25}`

#### **Approach 1: Using `zip()`**
```python
keys = ['name', 'age']
vals = ['Alice', 25]
print(dict(zip(keys, vals)))
```

---

### **32. Sort a list of dictionaries by a specific key**

**Sample Input:** `[{'name': 'B', 'score': 90}, {'name': 'A', 'score': 100}]`
**Sample Output:** `[{'name': 'A', 'score': 100}, {'name': 'B', 'score': 90}]`

#### **Approach 1: Using `sorted()` with lambda**
```python
data = [{'name': 'B', 'score': 90}, {'name': 'A', 'score': 100}]
print(sorted(data, key=lambda x: x['name']))
```

---

### **33. Filter a dictionary based on values**
**Scenario:** Keep items where value > 50.

**Sample Input:** `{'a': 10, 'b': 60, 'c': 55}`
**Sample Output:** `{'b': 60, 'c': 55}`

#### **Approach 1: Dictionary Comprehension**
```python
d = {'a': 10, 'b': 60, 'c': 55}
res = {k: v for k, v in d.items() if v > 50}
print(res)
```

---

### **34. Check if a value exists in a dictionary**

**Sample Input:** `{'a': 1}`, value = `1`
**Sample Output:** `True`

#### **Approach 1: Using `values()` and `in`**
```python
d = {'a': 1}
print(1 in d.values())
```

---

### **35. Get a list of keys sorted by their values**

**Sample Input:** `{'a': 3, 'b': 1, 'c': 2}`
**Sample Output:** `['b', 'c', 'a']`

#### **Approach 1: Using `sorted()` with `key=dict.get`**
```python
d = {'a': 3, 'b': 1, 'c': 2}
print(sorted(d, key=d.get))
```

---

## **Section 5: Functions & scoping (Q36-42)**

### **36. Write a function that checks if a number is in a given range**

```python
def in_range(n, start, end):
    return start <= n <= end

print(in_range(5, 1, 10))
```

---

### **37. Nested Function: Write a function that returns another function**

```python
def multiplier(factor):
    def multiply(n):
        return n * factor
    return multiply

double = multiplier(2)
print(double(5)) # 10
```

---

### **38. Use `global` keyword to modify a variable outside the function**

```python
x = 10
def update():
    global x
    x = 20

update()
print(x) # 20
```

---

### **39. Recursive function to find the sum of a list**

```python
def recursive_sum(lst):
    if not lst: return 0
    return lst[0] + recursive_sum(lst[1:])

print(recursive_sum([1, 2, 3]))
```

---

### **40. Function with variable number of keyword arguments (`**kwargs`)**

```python
def describe_pet(name, **details):
    print(f"Pet: {name}")
    for k, v in details.items():
        print(f"- {k}: {v}")

describe_pet("Rex", breed="Labrador", age=3)
```

---

### **41. Write a Lambda function that multiplies two numbers**

```python
mult = lambda a, b: a * b
print(mult(5, 4))
```

---

### **42. Use `map()` to convert a list of strings to integers**

```python
s_nums = ["1", "2", "3"]
i_nums = list(map(int, s_nums))
print(i_nums)
```

---

## **Section 6: File Handling (Q43-46)**

### **43. Append a line to an existing file**

```python
with open("test.txt", "a") as f:
    f.write("\nNew line added.")
```

---

### **44. Search for a specific word in a file and print the line number**

```python
search_word = "Python"
try:
    with open("test.txt", "r") as f:
        for i, line in enumerate(f, 1):
            if search_word in line:
                print(f"Found at line {i}")
except FileNotFoundError:
    print("File not found")
```

---

### **45. Count the frequency of each word in a file**

```python
from collections import Counter
try:
    with open("test.txt", "r") as f:
        content = f.read().split()
        print(Counter(content))
except FileNotFoundError:
    pass
```

---

### **46. Read only the first N lines of a file**

```python
N = 5
with open("test.txt", "r") as f:
    for _ in range(N):
        line = f.readline()
        if not line: break
        print(line.strip())
```

---

## **Section 7: OOP Mastery (Q47-50)**

### **47. Simple Inheritance with Method Overriding**

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

d = Dog()
d.speak()
```

---

### **48. Encapsulation: Using Private variables and Getters/Setters**

```python
class Student:
    def __init__(self, name):
        self.__name = name # Private

    def get_name(self):
        return self.__name

    def set_name(self, name):
        self.__name = name

s = Student("Alice")
print(s.get_name())
```

---

### **49. Polymorphism: Different classes with the same method name**

```python
class Cat:
    def sound(self): return "Meow"
class Dog:
    def sound(self): return "Bark"

for animal in [Cat(), Dog()]:
    print(animal.sound())
```

---

### **50. Abstract Class using `abc` module (Basics)**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): pass

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side**2

sq = Square(4)
print(sq.area())
```

---


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
