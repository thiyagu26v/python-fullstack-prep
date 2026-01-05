---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# Python Interview Questions - Level 2 (Intermediate to Advanced)
This document contains 50 intermediate to advanced Python interview questions.
Each question includes:
- Sample Input and Output
- Minimum of two coding approaches
- Detailed line-by-line inline comments

## **Section 1: Advanced OOP & Magic Methods (Q1-10)**

### **1. Difference between `__str__` and `__repr__`**

**Sample Input:** `obj = Person("Alice"); print(str(obj)); print(repr(obj))`
**Sample Output:**
`User: Alice`
`Person(name='Alice')`

#### **Approach 1: Implementing both methods**
```python
class Person:
    def __init__(self, name):  # Constructor method to initialize attributes
        self.name = name  # Assign the passed name to the instance attribute

    def __str__(self):  # Special method called by str() and print()
        return f"User: {self.name}"  # Return a human-readable string representation

    def __repr__(self):  # Special method called by repr() and in debuggers
        return f"Person(name='{self.name}')"  # Return an unambiguous string representation

p = Person("Alice")  # Create a new instance of Person with name "Alice"
print(str(p))   # Explicitly call __str__: Output: User: Alice
print(repr(p))  # Explicitly call __repr__: Output: Person(name='Alice')
```

#### **Approach 2: Standard Library Example (datetime)**
```python
import datetime  # Import the built-in datetime module

now = datetime.datetime.now()  # Get the current local date and time
print(str(now))   # Use __str__ for a readable format: e.g., 2023-10-27...
print(repr(now))  # Use __repr__ for a developer-friendly creation string
```

---

### **2. Difference between `@staticmethod` and `@classmethod`**

**Sample Input:** `MyClass.method()`
**Sample Output:** `Static Method`, `Class Method taking <class '__main__.MyClass'>`

#### **Approach 1: Basic Implementation**
```python
class Demo:
    @staticmethod  # Decorator to define a static method
    def static_method():  # Static methods do not take 'self' or 'cls'
        print("Static Method called")  # Simple print statement

    @classmethod  # Decorator to define a class method
    def class_method(cls):  # Class methods take 'cls' (the class itself) as first arg
        print(f"Class Method called with {cls}")  # Print the class object

Demo.static_method()  # Call using ClassName.method() without instantiation
Demo.class_method()   # Call class method; Python passes 'Demo' as 'cls' automatically
```

#### **Approach 2: Factory Method (Practical Use of Class Method)**
```python
class Person:
    def __init__(self, name, age):  # Standard constructor
        self.name = name  # Set name
        self.age = age  # Set age

    @classmethod  # Define a class method to use as an alternative constructor
    def from_birth_year(cls, name, birth_year):  # Takes class, name, and birth year
        current_year = 2023  # Hardcoded current year for example
        return cls(name, current_year - birth_year)  # Return new instance using cls(name, calculated_age)

p = Person.from_birth_year("Bob", 1990)  # Create Person using the factory method
print(p.age)  # Output: 33 (2023 - 1990)
```

---

### **3. Implement a class that works as a function using `__call__`**

**Sample Input:** `add = Adder(10); print(add(5))`
**Sample Output:** `15`

#### **Approach 1: Basic Functor**
```python
class Adder:
    def __init__(self, n):  # Initialize with a base number
        self.n = n  # Store the base number

    def __call__(self, x):  # The __call__ method allows the instance to be called like a function
        return self.n + x  # Return the sum of stored value and passed argument

add_10 = Adder(10)  # Create an instance 'add_10' initialized with 10
print(add_10(5))    # Call the instance like a function: 10 + 5 = 15
```

#### **Approach 2: Stateful Decorator Class**
```python
class Counter:
    def __init__(self, func):  # Constructor receives the function to decorate
        self.func = func  # Store the function
        self.count = 0  # Initialize a counter state

    def __call__(self, *args, **kwargs):  # Called when the decorated function is invoked
        self.count += 1  # Increment invocation count
        print(f"Call {self.count}")  # Print the current count
        return self.func(*args, **kwargs)  # call the original function and return result

@Counter  # Decorate 'greet' with the Counter class
def greet(name):
    print(f"Hello {name}")  # Function body

greet("Alice")  # First call triggers __call__, increments count to 1
greet("Bob")    # Second call triggers __call__, increments count to 2
# Output:
# Call 1
# Hello Alice
# Call 2
# Hello Bob
```

---

### **4. Implement Singleton Pattern (Ensure only one instance exists)**

**Sample Input:** `s1 = Singleton(); s2 = Singleton(); print(s1 is s2)`
**Sample Output:** `True`

#### **Approach 1: Using `__new__`**
```python
class Singleton:
    _instance = None  # Class-level variable to store the single instance

    def __new__(cls):  # __new__ is called before __init__ to create the object
        if cls._instance is None:  # Check if instance already exists
            cls._instance = super(Singleton, cls).__new__(cls)  # Create it if not
        return cls._instance  # Return the stored single instance

s1 = Singleton()  # Create first reference
s2 = Singleton()  # Create second reference (returns same object)
print(s1 is s2)  # True: both variables point to the exact same memory location
```

#### **Approach 2: Using a Decorator**
```python
def singleton(cls):  # Decorator function taking a class
    instances = {}  # Dictionary to map classes to their single instances
    def get_instance(*args, **kwargs):  # Wrapper function
        if cls not in instances:  # Check if class is already instantiated
            instances[cls] = cls(*args, **kwargs)  # Create and store if new
        return instances[cls]  # Return the stored instance
    return get_instance  # Return the wrapper

@singleton  # Apply decorator to Database class
class Database:
    pass

d1 = Database()  # First request creates instance
d2 = Database()  # Second request returns existing instance
print(d1 is d2)  # True
```

---

### **5. Create a specific Exception class**

**Sample Input:** `raise MyError("Something wrong")`
**Sample Output:** `Caught custom error: Something wrong`

#### **Approach 1: Inheriting from Exception**
```python
class MyCustomError(Exception):  # Define new exception inheriting from base Exception
    pass  # No extra logic needed for basic custom exception

try:
    raise MyCustomError("This is a custom error")  # Raise the custom exception manually
except MyCustomError as e:  # Catch specifically MyCustomError
    print(f"Caught: {e}")  # Print the error message
```

#### **Approach 2: Custom Exception with Attributes**
```python
class ValidationError(Exception):  # Inherit from Exception
    def __init__(self, message, code):  # Accept custom arguments
        super().__init__(message)  # Initialize base Exception with message
        self.code = code  # Store the custom error code

try:
    raise ValidationError("Invalid Input", 400)  # Raise with message and code
except ValidationError as e:  # Catch the custom exception
    print(f"Error: {e}, Code: {e.code}")  # Access message (via e) and custom .code attribute
```

---

### **6. Use `__slots__` to reduce memory usage**

**Sample Input:** `obj.x`
**Sample Output:** `1` (Access works, but dynamic attributes prevented if not in slots on strict usage)

#### **Approach 1: With `__slots__`**
```python
class Point:
    __slots__ = ['x', 'y']  # Explicitly define allowed attributes. Prevents creation of __dict__
    
    def __init__(self, x, y):
        self.x = x  # Assign x
        self.y = y  # Assign y

p = Point(1, 2)  # Create instance
print(p.x)  # Access valid attribute
# p.z = 3  # This would raise AttributeError because 'z' is not listed in __slots__
```

#### **Approach 2: Comparison (Standard Class)**
```python
class PointStandard:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        # Standard classes have an internal __dict__ consuming more memory per instance

p = PointStandard(1, 2)  # Create instance
p.z = 3  # Allowed: dynamic attribute creation is standard in Python
print(p.z)  # Output: 3
```

---

### **7. Implement Operator Overloading (e.g., `+` for custom objects)**

**Sample Input:** `v1 + v2`
**Sample Output:** `Vector(3, 3)` (if v1=(1,1), v2=(2,2))

#### **Approach 1: Overloading `__add__`**
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):  # Special Magic Method for '+' operator
        return Vector(self.x + other.x, self.y + other.y)  # Return new Vector with sum of coords

    def __repr__(self):  # For readable output
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)  # Vector 1
v2 = Vector(3, 4)  # Vector 2
print(v1 + v2)  # Calls v1.__add__(v2). Output: Vector(4, 6)
```

#### **Approach 2: Overloading `__eq__` (Equality)**
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __eq__(self, other):  # Special Magic Method for '==' operator
        return self.x == other.x and self.y == other.y  # Compare values instead of memory IDs

v1 = Vector(1, 1)
v2 = Vector(1, 1)
print(v1 == v2)  # True because of __eq__. (Default behavior would return False)
```

---

### **8. Implement a Context Manager using `__enter__` and `__exit__`**

**Sample Input:** `with MyManager() as m: print("Inside")`
**Sample Output:** `Enter`, `Inside`, `Exit`

#### **Approach 1: Class-based Context Manager**
```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename  # Store filename
        self.mode = mode  # Store mode

    def __enter__(self):  # Magic method called at the start of 'with' block
        self.file = open(self.filename, self.mode)  # Open resource
        return self.file  # Return resource to be bound to 'as var'

    def __exit__(self, exc_type, exc_val, exc_tb):  # Called when exiting 'with' block
        if self.file:
            self.file.close()  # Clean up resource (close file) even if error occurred

# Usage (creates file if not exists)
# with FileManager('test.txt', 'w') as f:
#     f.write('Hello')
```

#### **Approach 2: Using `contextlib.contextmanager` Decorator**
```python
from contextlib import contextmanager

@contextmanager  # Decorator to convert generator into context manager
def file_manager(filename, mode):
    f = open(filename, mode)  # Setup phase: Open resource
    try:
        yield f  # Pass control to the 'with' block body
    finally:
        f.close()  # Teardown phase: Ensure closure (always executes)

# with file_manager('test.txt', 'w') as f:
#     f.write('Hello')
```

---

### **9. Use Property Decorators for Getter/Setter Logic**

**Sample Input:** `obj.age = -5`
**Sample Output:** `ValueError: Age cannot be negative`

#### **Approach 1: Using `@property` and `@name.setter`**
```python
class Person:
    def __init__(self, age):
        self._age = age  # Use underscore to denote 'protected/internal' attribute

    @property  # Define the getter method
    def age(self):
        return self._age  # Return the internal value

    @age.setter  # Define the setter method for validation
    def age(self, value):
        if value < 0:  # Validation logic
            raise ValueError("Age cannot be negative")  # Reject invalid data
        self._age = value  # Set valid data

p = Person(20)
p.age = 25  # Calls the setter method
print(p.age)  # Calls the getter method
# p.age = -5  # Raises ValueError thanks to setter logic
```

#### **Approach 2: Using `property()` function (Old style but valid)**
```python
class Person:
    def __init__(self, age):
        self._age = age

    def get_age(self):  # Explicit getter
        return self._age

    def set_age(self, value):  # Explicit setter
        if value < 0:
            raise ValueError("Invalid")
        self._age = value

    age = property(get_age, set_age)  # Bind getter and setter to 'age' attribute manually

p = Person(10)
p.age = 15
print(p.age)
```

---

### **10. Demonstrate Multiple Inheritance and MRO**

**Sample Input:** `D().show()`
**Sample Output:** `D show`, `B show`, `A show` (Depends on hierarchy)

#### **Approach 1: Diamond Problem Structure**
```python
class A:
    def show(self):
        print("A show")

class B(A):  # Inherits from A
    def show(self):
        print("B show")
        super().show()  # Call next class in MRO (A)

class C(A):  # Inherits from A
    def show(self):
        print("C show")
        super().show()  # Call next class in MRO (A if C is used alone)

class D(B, C):  # Inherits from B, then C
    def show(self):
        print("D show")
        super().show()  # Call next class in MRO (B)

d = D()
d.show()
# Output order demonstrates MRO: D -> B -> C -> A
# print(D.mro())  # View Method Resolution Order: [D, B, C, A, object]
```

#### **Approach 2: Using Specific Parent Call**
```python
class A:
    def msg(self):
        print("Message from A")

class B:
    def msg(self):
        print("Message from B")

class C(A, B):  # Multiple inheritance
    def msg(self):
        A.msg(self)  # Explicitly call A's method
        B.msg(self)  # Explicitly call B's method (bypassing MRO ambiguity manual selection)

c = C()
c.msg()
```


---

## **Section 2: Decorators, Generators & Advanced Functions (Q11-20)**

### **11. Create a decorator that accepts arguments**

**Sample Input:** `@repeat(3) def say(): print("Hi")`
**Sample Output:** `Hi` (printed 3 times)

#### **Approach 1: Three-level Nested Function**
```python
def repeat(num_times):  # Outermost function accepts arguments for the decorator
    def decorator_repeat(func):  # Middle function accepts the function to be decorated
        def wrapper(*args, **kwargs):  # Innermost function accepts arguments for the decorated function
            for _ in range(num_times):  # Loop 'num_times' (captured from closure)
                func(*args, **kwargs)  # Call the original function
        return wrapper  # Return the wrapper function
    return decorator_repeat  # Return the decorator function

@repeat(3)  # Apply decorator with argument '3'
def say_hello():
    print("Hello")  # Function body

say_hello()  # Call the decorated function
```

#### **Approach 2: Using a Class as Decorator**
```python
class Repeat:
    def __init__(self, num_times):  # Constructor accepts decorator arguments
        self.num_times = num_times  # Store the argument

    def __call__(self, func):  # Called when decorating the function
        def wrapper(*args, **kwargs):  # Wrapper for the function execution
            for _ in range(self.num_times):  # Loop using stored argument
                func(*args, **kwargs)  # Call original function
        return wrapper  # Return the wrapper

@Repeat(3)  # Instantiate class with '3' and use as decorator
def greet():
    print("Hi")  # Function body

greet()  # Call decorated function
```

---

### **12. Implement a Memoization Decorator (Caching results)**

**Sample Input:** `fib(50)` (Calculated instantly using cache)
**Sample Output:** `12586269025`

#### **Approach 1: Manual Dictionary Cache**
```python
def memoize(func):  # Decorator function
    cache = {}  # Dictionary to store results (Closure)
    def wrapper(n):  # Wrapper accepting argument 'n'
        if n not in cache:  # Check if result is already cached
            cache[n] = func(n)  # Calculate and store if not present
        return cache[n]  # Return the cached result
    return wrapper  # Return the wrapper

@memoize  # Apply memoization
def fib(n):
    if n <= 1: return n  # Base case
    return fib(n-1) + fib(n-2)  # Recursive call (now optimized)

print(fib(50))  # Calculate Fibonacci of 50 efficiently
```

#### **Approach 2: Using `functools.lru_cache`**
```python
from functools import lru_cache  # Import built-in memoization tool

@lru_cache(maxsize=None)  # Decorator to cache results (unlimited size)
def fib(n):
    if n <= 1: return n  # Base case
    return fib(n-1) + fib(n-2)  # Recursive call

print(fib(50))  # Calculate using optimized built-in cache
```

---

### **13. Chain multiple decorators on a single function**

**Sample Input:** `@bold @italic`
**Sample Output:** `<b><i>text</i></b>`

#### **Approach 1: Stacking Decorators**
```python
def make_bold(func):  # Decorator for bold tag
    def wrapper():
        return f"<b>{func()}</b>"  # Wrap result in <b>
    return wrapper

def make_italic(func):  # Decorator for italic tag
    def wrapper():
        return f"<i>{func()}</i>"  # Wrap result in <i>
    return wrapper

@make_bold  # Applied second (Outer)
@make_italic  # Applied first (Inner)
def say():
    return "text"

print(say())
# Order of execution: make_bold(make_italic(say))
# Output: <b><i>text</i></b>
```

#### **Approach 2: Manual Application**
```python
def say_plain():
    return "text"  # Basic function

# Manually applying decorators showing the specialized syntax logic
# Inner: make_italic(say_plain)
# Outer: make_bold(...)
decorated_func = make_bold(make_italic(say_plain))
print(decorated_func())  # Execute the composed function chain
```

---

### **14. Create a custom Iterator (using `__iter__` and `__next__`)**

**Sample Input:** `Counter(3)`
**Sample Output:** `1, 2, 3`

#### **Approach 1: Custom Class Implementation**
```python
class CountUp:
    def __init__(self, low, high):  # Initialize range
        self.current = low  # Start value
        self.high = high  # End value

    def __iter__(self):
        return self  # Iterator object must return itself

    def __next__(self):  # Logic to get the next item
        if self.current > self.high:  # Check termination condition
            raise StopIteration  # Signal end of iteration to the loop
        else:
            self.current += 1  # Increment state
            return self.current - 1  # Return current value (before increment)

for num in CountUp(1, 3):  # Use in a for-loop
    print(num)
```

#### **Approach 2: Using a Generator Function (Simpler)**
```python
def count_up(low, high):
    current = low  # Initialize
    while current <= high:  # Loop condition
        yield current  # Pause execution and return value to caller
        current += 1  # Resume here next time and increment

for num in count_up(1, 3):  # Iterate over generated values
    print(num)
```

---

### **15. Implement a generator that yields infinite Fibonacci numbers**

**Sample Input:** `first 5 numbers`
**Sample Output:** `0, 1, 1, 2, 3`

#### **Approach 1: While True Loop**
```python
def fib_generator():
    a, b = 0, 1  # Initialize first two numbers
    while True:  # Infinite loop
        yield a  # Yield current number
        a, b = b, a + b  # Update values for next iteration

gen = fib_generator()  # Create generator object
for _ in range(5):  # Loop 5 times
    print(next(gen))  # Manually get next value
```

#### **Approach 2: Using `itertools.islice` to consume**
```python
import itertools  # Import itertools for slicing generators

def fib_gen():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# islice allows slicing an infinite iterator safely
# list() consumes the slice and prints it
print(list(itertools.islice(fib_gen(), 5)))
```

---

### **16. Use `yield from` to delegate to a sub-generator**

**Sample Input:** `list(delegator())`
**Sample Output:** `['A', 'B', 1, 2]`

#### **Approach 1: Standard Loop Delegation**
```python
def sub_gen():
    yield 1
    yield 2

def delegator():
    yield 'A'
    yield 'B'
    for item in sub_gen():  # Manually iterate sub-generator
        yield item  # Re-yield each item

print(list(delegator()))  # ['A', 'B', 1, 2]
```

#### **Approach 2: `yield from` Syntax**
```python
def sub_gen():
    yield 1
    yield 2

def delegator():
    yield 'A'
    yield 'B'
    yield from sub_gen()  # Automatically yields all values from sub_gen transparently

print(list(delegator()))  # ['A', 'B', 1, 2]
```

---

### **17. Demonstrate Closures (Function retaining environment)**

**Sample Input:** `multiply_by_5 = multiplier(5); multiply_by_5(10)`
**Sample Output:** `50`

#### **Approach 1: Nested Function**
```python
def multiplier(n):  # Outer function accepting 'n'
    def multiply(x):  # Inner function accepting 'x'
        return x * n  # Uses 'n' from outer scope (Closure)
    return multiply  # Returns the inner function

times5 = multiplier(5)  # Create closure with n=5
print(times5(10))  # Call inner function: 10 * 5 = 50
print(times5(2))   # Call inner function: 2 * 5 = 10
```

#### **Approach 2: Using `lambda` inside**
```python
def multiplier(n):
    return lambda x: x * n  # Returns an anonymous function capturing n

times3 = multiplier(3)  # Create closure with n=3
print(times3(10))  # 10 * 3 = 30
```

---

### **18. Use `functools.partial` to fix arguments**

**Sample Input:** `power_of_2(4)`
**Sample Output:** `16` (where original is `pow(base, exp)`)

#### **Approach 1: Using Wrapper Function**
```python
def power(base, exponent):
    return base ** exponent  # General power function

def square(base):  # specialized wrapper
    return power(base, 2)  # Fix exponent to 2

print(square(5))  # 25
```

#### **Approach 2: Using `partial`**
```python
from functools import partial  # Import tool

def power(base, exponent):
    return base ** exponent

# Create new function 'square' with exponent argument pre-filled as 2
square = partial(power, exponent=2)
print(square(5))  # 5^2 = 25
```

---

### **19. Implement a Coroutine that receives data using `send()`**

**Sample Input:** `grep 'copy'`
**Sample Output:** `Line found: copy this`

#### **Approach 1: Basic Coroutine**
```python
def grep(pattern):
    print(f"Looking for {pattern}")
    while True:
        line = (yield)  # Pause and wait to receive data via .send()
        if pattern in line:  # Check condition
            print(f"Line found: {line}")

search = grep('python')  # Initialize generator
next(search)  # Prime the coroutine (advance to first yield)
search.send("I love java")  # Send data: No match
search.send("I love python")  # Send data: Match -> prints "Line found..."
```

#### **Approach 2: Auto-Priming Decorator**
```python
def coroutine(func):  # Decorator to handle priming
    def start(*args, **kwargs):
        g = func(*args, **kwargs)  # Create generator
        next(g)  # Prime it automatically
        return g  # Return ready-to-use generator
    return start

@coroutine
def receiver():
    try:
        while True:
            data = (yield)  # Wait for data
            print(f"Received: {data}")
    except GeneratorExit:  # Handle close() call
        print("Done")

r = receiver()  # Created and primed automatically
r.send("Hello")  # Use immediately
r.close()  # Close coroutine
```

---

### **20. Monkey Patching (Modifying class/module at runtime)**

**Sample Input:** `obj.func()` -> Modified behavior
**Sample Output:** `Patched!`

#### **Approach 1: Patching a Class Method**
```python
class MyClass:
    def greet(self):
        print("Original Hello")

def new_greet(self):  # Define new function to replace the old one
    print("Patched Hello")

MyClass.greet = new_greet  # Replace method on the class dynamically
obj = MyClass()
obj.greet()  # Calls new_greet: Output: Patched Hello
```

#### **Approach 2: Patching using `unittest.mock` (Safe)**
```python
from unittest.mock import patch

class ProductionClass:
    def method(self):
        return "Real Value"

# Temporarily replace 'method' with a mock that returns a fixed value
# This is cleaner and safer than manual patching as it reverts automatically
with patch.object(ProductionClass, 'method', return_value="Mocked Value"):
    obj = ProductionClass()
    print(obj.method())  # Output: Mocked Value

print(ProductionClass().method())  # Output: Real Value (Restored)
```

---


---

## **Section 3: Python Data Handling & Collections (Q21-30)**

### **21. Deep Copy vs Shallow Copy**

**Sample Input:** `l1 = [[1], [2]]; l2 = copy.copy(l1); l1[0][0] = 99`
**Sample Output:** `l2[0][0]` is `99` (Shallow), `l2[0][0]` is `1` (Deep)

#### **Approach 1: Using `copy` module (Shallow Copy)**
```python
import copy  # Import the copy module for shallow and deep copying

list1 = [[1, 2], [3, 4]]  # Create a nested list
list2 = copy.copy(list1)  # Shallow copy: creates a new outer list, but inner items are shared references

list1[0][0] = 99  # Modify a nested item in the original list
print(list1)  # [[99, 2], [3, 4]] -> Original is modified
print(list2)  # [[99, 2], [3, 4]] -> Shallow copy reflects changes to nested objects
```

#### **Approach 2: Using `copy.deepcopy` (Deep Copy)**
```python
import copy  # Import the copy module

list1 = [[1, 2], [3, 4]]  # Create a nested list
list2 = copy.deepcopy(list1)  # Deep copy: recursively copies all objects, creating completely independent copies

list1[0][0] = 99  # Modify a nested item in the original list
print(list1)  # [[99, 2], [3, 4]] -> Original reflects the change
print(list2)  # [[1, 2], [3, 4]] -> Deep copy remains unchanged as it has its own copy of inner lists
```

---

### **22. The Mutable Default Argument Gotcha**

**Sample Input:** `func(); func()`
**Sample Output:** `[1]`, `[1, 1]` (Unexpected accumulation)

#### **Approach 1: The "Buggy" Way**
```python
def add_item(item, list_arr=[]):  # The default list is created only once when the function is DEFINED
    list_arr.append(item)  # Modifies the same list object across different function calls
    return list_arr

print(add_item(1))  # [1] -> First call adds to the empty default list
print(add_item(1))  # [1, 1] -> Second call adds to the SAME list object persistent in memory
```

#### **Approach 2: The "Safe" Way (None Check)**
```python
def add_item_safe(item, list_arr=None):  # Use None as the default value (immutable)
    if list_arr is None:  # Check if a list was provided or if we should use the default
        list_arr = []  # Create a NEW list object inside the function call
    list_arr.append(item)  # Append to the newly created or provided list
    return list_arr

print(add_item_safe(1))  # [1] -> New list created
print(add_item_safe(1))  # [1] -> New list created again, no accumulation
```

---

### **23. Packing and Unpacking Arguments (`*args`, `**kwargs`)**

**Sample Input:** `func(1, 2, a=3)`
**Sample Output:** `Args: (1, 2), Kwargs: {'a': 3}`

#### **Approach 1: Function Definition**
```python
def func(*args, **kwargs):  # *args collects positional args into a tuple, **kwargs collects keyword args into a dict
    print(f"Args: {args}")    # Print the tuple of positional arguments
    print(f"Kwargs: {kwargs}") # Print the dictionary of keyword arguments

func(1, 2, a=3, b=4)  # Call with mixed argument types
```

#### **Approach 2: Function Call (Exploding)**
```python
def add(a, b, c):  # Function expecting exactly three arguments
    print(a + b + c)  # Print their sum

nums = [1, 2, 3]  # A list of values
add(*nums)  # The * operator unpacks the list into positional arguments a, b, and c

d = {'a': 1, 'b': 2, 'c': 3}  # A dictionary with keys matching parameter names
add(**d)    # The ** operator unpacks dictionary keys/values into named keyword arguments
```

---

### **24. Sorting with Custom Keys (Lambda)**

**Sample Input:** `data = [{'name': 'B', 'age': 30}, {'name': 'A', 'age': 40}]`
**Sample Output:** Sorted by name: A, B

#### **Approach 1: Using `lambda`**
```python
data = [{'name': 'Bob', 'age': 30}, {'name': 'Alice', 'age': 25}]  # List of dictionaries

# The 'key' argument takes a function; lambda extract the 'name' field for comparison
sorted_data = sorted(data, key=lambda x: x['name'])
print(sorted_data)  # Display the list sorted alphabetically by name
```

#### **Approach 2: Using `operator.itemgetter` (More efficient)**
```python
from operator import itemgetter  # itemgetter is faster than lambda for attribute access

data = [{'name': 'Bob', 'age': 30}, {'name': 'Alice', 'age': 25}]  # List of dictionaries
# Sort specifically by the 'age' key using itemgetter
sorted_data = sorted(data, key=itemgetter('age'))  
print(sorted_data)  # Display the list sorted numerically by age
```

---

### **25. Parallel Iteration with `zip`**

**Sample Input:** `names=['A', 'B'], ages=[20, 30]`
**Sample Output:** `('A', 20), ('B', 30)`

#### **Approach 1: Standard `zip`**
```python
names = ["Alice", "Bob"]  # First list
ages = [25, 30]           # Second list

for name, age in zip(names, ages):  # zip pairs elements by index until the shortest list ends
    print(f"{name} is {age}")  # Unpack and print each pair
```

#### **Approach 2: `zip_longest` (Handle uneven lists)**
```python
from itertools import zip_longest  # Import for handling lists of different lengths

names = ["Alice", "Bob"]  # Longer list
ages = [25]               # Shorter list

# zip_longest pairs items but uses a 'fillvalue' if one iterator finishes early
for name, age in zip_longest(names, ages, fillvalue=0):
    print(f"{name} is {age}")  # Bob will be paired with '0'
```

---

### **26. Use `map`, `filter`, and `reduce`**

**Sample Input:** `nums = [1, 2, 3, 4]`
**Sample Output:** `Sum of squares of evens: 20`

#### **Approach 1: Functional Style**
```python
from functools import reduce  # Import reduce for cumulative operations

nums = [1, 2, 3, 4]  # Input list

# 1. Filter: Keep only even numbers (2, 4)
evens = filter(lambda x: x % 2 == 0, nums)
# 2. Map: Square those even numbers (4, 16)
squared = map(lambda x: x**2, evens)
# 3. Reduce: Sum the squared numbers cumulative fashion (4 + 16 = 20)
result = reduce(lambda x, y: x + y, squared)

print(result)  # Output: 20
```

#### **Approach 2: List Comprehension (Pythonic Equivalent)**
```python
nums = [1, 2, 3, 4]  # Input list
# Combine filtering and mapping in a single readable line, then sum the result
result = sum([x**2 for x in nums if x % 2 == 0])
print(result)  # Output: 20
```

---

### **27. Using `any()` and `all()` for Validation**

**Sample Input:** `[True, True, False]`
**Sample Output:** `any: True, all: False`

#### **Approach 1: Checking Constraints**
```python
ages = [25, 30, 18, 40]  # List of numbers
# any() returns True if AT LEAST ONE element in the generator matches the condition
has_adult = any(age >= 18 for age in ages)  
# all() returns True only if EVERY element in the generator matches the condition
all_adults = all(age >= 18 for age in ages) 

print(f"Has Adult: {has_adult}")  # True
print(f"All Adults: {all_adults}") # True
```

#### **Approach 2: Empty Iterables Behavior**
```python
# Interview tip: empty iterable logic
print(all([]))  # True (Vacuously true because NO element violates the condition)
print(any([]))  # False (Because there is no element to satisfy any condition)
```

---

### **28. Dynamic Attributes (`getattr`, `setattr`)**

**Sample Input:** `obj, "name"`
**Sample Output:** Alice

#### **Approach 1: Dynamic Access**
```python
class Person:  # Basic placeholder class
    pass

p = Person()  # Create instance
setattr(p, 'name', 'Alice')  # Set the 'name' attribute dynamically using a string key
print(getattr(p, 'name'))    # Access the 'name' attribute dynamically using a string key
```

#### **Approach 2: Handling Missing Attributes**
```python
p = Person()  # Create empty instance
# getattr accepts an optional 3rd argument as a default value if the attribute is missing
name = getattr(p, 'age', 18) 
print(name)  # Output: 18 (default used because 'age' isn't set)
```

---

### **29. `defaultdict` for Grouping**

**Sample Input:** `pairs = [('a', 1), ('a', 2), ('b', 3)]`
**Sample Output:** `{'a': [1, 2], 'b': [3]}`

#### **Approach 1: Standard Dict (`setdefault`)**
```python
data = [('a', 1), ('a', 2), ('b', 3)]  # List of key-value tuples
d = {}  # Regular dictionary
for k, v in data:
    # setdefault ensures the key exists (initializing with [] if not) before appending
    d.setdefault(k, []).append(v)  
print(d)  # Output contains lists as values
```

#### **Approach 2: `collections.defaultdict` (Cleaner)**
```python
from collections import defaultdict  # Specialized dictionary subclass

data = [('a', 1), ('a', 2), ('b', 3)]  # Input data
d = defaultdict(list)  # Specify 'list' as the factory function for missing keys
for k, v in data:
    d[k].append(v)  # No need for initialization checks; it handles it automatically
print(dict(d))  # Convert back to regular dict for clean printing
```

---

### **30. `else` clause in Loops (`for ... else`)**

**Sample Input:** Search loop completes without break
**Sample Output:** `else` block executes

#### **Approach 1: Standard Flag Variable**
```python
found = False  # Initialize a flag
for i in [1, 2, 3]:  # Iterate through a list
    if i == 5:  # Check condition
        found = True  # Set flag if found
        break  # Exit loop
if not found:  # Manual check after the loop finishes
    print("Not found (Flag)")  # Print if never triggered
```

#### **Approach 2: Pythonic `else` block**
```python
for i in [1, 2, 3]:  # Loop through items
    if i == 5:  # Search condition
        print("Found")
        break  # The 'else' block will be SKIPPED if break is executed
else:
    # This block executes ONLY if the loop finishes naturally (WITHOUT hitting a 'break')
    print("Not found (Else)")
```

---

## **Section 4: Functional Python & Built-in Modules (Q31-40)**

### **31. `is` vs `==` (Identity vs Equality)**

**Sample Input:** `a = [1]; b = [1]; print(a == b, a is b)`
**Sample Output:** `True False` (Equality True, Identity False via different memory addresses)

#### **Approach 1: Equality Check (`==`)**
```python
list1 = [1, 2, 3]  # Create a list
list2 = [1, 2, 3]  # Create another list with the same values

# The '==' operator checks for value equality (Do these objects contain the same data?)
if list1 == list2:
    print("Values are identical")  # This will print
```

#### **Approach 2: Identity Check (`is`)**
```python
list1 = [1, 2, 3]  # Create a list
list2 = list1      # Create a new reference pointing to the SAME object in memory
list3 = [1, 2, 3]  # Create a new list object with the same content

# The 'is' operator checks for identity (Do these references point to the exact same memory address?)
print(list1 is list2)  # True: list2 is just an alias for list1
print(list1 is list3)  # False: content is the same, but they are different objects in memory
```

---

### **32. Using `namedtuple` and `dataclasses`**

**Sample Input:** `p = Point(1, 2); print(p.x)`
**Sample Output:** `1`

#### **Approach 1: `collections.namedtuple` (Immutable)**
```python
from collections import namedtuple  # Import factory function for tuples with fields

# Create a tuple-like class 'Point' with fields 'x' and 'y'
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)  # Instantiate
print(p.x, p.y)    # Access by field name (cleaner than indexing like p[0])
# p.x = 30  # Error: namedtuples are immutable (tuple heritage)
```

#### **Approach 2: `dataclasses` (Modern, Mutable by default)**
```python
from dataclasses import dataclass  # decorator to automate class boilerplate

@dataclass  # Automatically generates __init__, __repr__, and __eq__
class Point:
    x: int  # Type hints are required for dataclass fields
    y: int

p = Point(10, 20)  # Instantiate using generated constructor
p.x = 30  # Allowed: dataclasses are mutable by default
print(p)  # Auto-generated repr: Point(x=30, y=20)
```

---

### **33. Context Manager: `contextlib.suppress`**

**Sample Input:** Delete non-existent file
**Sample Output:** No Error (Silently ignored)

#### **Approach 1: Try/Except Block**
```python
import os  # module for operating system interactions

try:
    os.remove("non_existent_file.txt")  # Attempt to delete
except FileNotFoundError:  # Catch specifically if the file doesn't exist
    pass  # Silently ignore the error as intended
print("Done")
```

#### **Approach 2: `contextlib.suppress` (Cleaner)**
```python
import os
from contextlib import suppress  # utility to gracefully handle specific exceptions

# with suppress(Exception) will catch and ignore the named exception within its block
with suppress(FileNotFoundError):
    os.remove("non_existent_file.txt")  # Even if this fails, execution continues normally
print("Done")
```

---

### **34. Infinite Iterators (`cycle`, `repeat`)**

**Sample Input:** `cycle('AB')`
**Sample Output:** `A, B, A, B...`

#### **Approach 1: `itertools.cycle`**
```python
import itertools  # Standard library for advanced iteration
import time       # For potential delays

counter = 0  # To prevent actual infinite loop in this example
for char in itertools.cycle("AB"):  # cycle() loops 'A' then 'B' forever
    print(char, end=" ")
    counter += 1
    if counter >= 6: break  # Safety break after 6 iterations
# Output: A B A B A B
```

#### **Approach 2: `itertools.repeat`**
```python
import itertools

# repeat(obj, times) yields the object a fixed or infinite number of times
for item in itertools.repeat("Hello", 3):
    print(item)  # Prints "Hello" exactly 3 times
```

---

### **35. Preserving Metadata in Decorators (`functools.wraps`)**

**Sample Input:** `func.__name__` on decorated function
**Sample Output:** `func` (Correct), not `wrapper`

#### **Approach 1: Without `wraps` (Metadata lost)**
```python
def my_decorator(func):  # Standard decorator pattern
    def wrapper():
        """Wrapper Docstring"""  # This docstring will replace the original
        func()
    return wrapper

@my_decorator
def greet():
    """Greet Docstring"""
    pass

print(greet.__name__)  # 'wrapper' -> The original function's name is GONE
print(greet.__doc__)   # 'Wrapper Docstring' -> Documentation is lost too
```

#### **Approach 2: With `functools.wraps` (Metadata preserved)**
```python
from functools import wraps  # essential tool for writing robust decorators

def my_decorator(func):
    @wraps(func)  # This decorator copies __name__, __doc__, etc. from 'func' to 'wrapper'
    def wrapper():
        func()
    return wrapper

@my_decorator
def greet():
    """Greet Docstring"""
    pass

print(greet.__name__)  # 'greet' -> name is preserved!
print(greet.__doc__)   # 'Greet Docstring' -> Documentation is preserved!
```

---

### **36. Making a Class Iterable (`__getitem__`, `__len__`)**

**Sample Input:** `obj[0]`
**Sample Output:** Returns item at index 0

#### **Approach 1: Using `__getitem__` (Sequence Protocol)**
```python
class MySequence:
    def __init__(self, data):
        self.data = data  # Store a list internaly

    def __getitem__(self, index):  # Enables the obj[index] syntax
        return self.data[index]  # Delegation to the internal list

obj = MySequence([1, 2, 3])
print(obj[0])  # Access by index works
for item in obj:  # Iteration works automatically because Python tries index 0, 1, 2...
    print(item, end=" ")
```

#### **Approach 2: Implementing `__iter__`**
```python
class MyIterable:
    def __init__(self, data):
        self.data = data

    def __iter__(self):  # The formal way to make an object iterable
        return iter(self.data)  # simply return an iterator for the internal data

obj = MyIterable([1, 2, 3])
for item in obj:  # This calls __iter__() and loops through the results
    print(item, end=" ")
```

---

### **37. Inspecting Scope (`globals`, `locals`)**

**Sample Input:** `print(locals())`
**Sample Output:** Dictionary of local variables

#### **Approach 1: `locals()` inside function**
```python
def func():
    x = 10  # Local variable
    y = 20  # Local variable
    # locals() returns a dictionary of all variables currently in the local scope
    print(locals())  # {'x': 10, 'y': 20}

func()
```

#### **Approach 2: `globals()` module level**
```python
x = 100  # Global variable
def func():
    # globals() returns a dictionary of all variables in the module-level scope
    # This allows dynamic access to global variables
    print(globals()['x'])  

func()
```

---

### **38. Frequency Counting with `collections.Counter`**

**Sample Input:** `['a', 'b', 'a', 'c']`
**Sample Output:** `{'a': 2, 'b': 1, 'c': 1}`

#### **Approach 1: Manual Dictionary**
```python
data = ['a', 'b', 'a', 'c']
count = {}  # Empty dict for frequency tracking
for item in data:
    # get(item, 0) provides the current count or 0 if it's the first time seeing it
    count[item] = count.get(item, 0) + 1
print(count)
```

#### **Approach 2: `collections.Counter`**
```python
from collections import Counter  # high-performance counter subclass of dict

data = ['a', 'b', 'a', 'c']
counts = Counter(data)  # Automatically count frequencies of all items in the iterable
print(counts)  # Counter({'a': 2, 'b': 1, 'c': 1})
print(counts.most_common(1))  # Utility method to find the top 'n' most frequent items
```

---

### **39. Advanced JSON Serialization (Custom Objects)**

**Sample Input:** `json.dumps(obj)`
**Sample Output:** `{"name": "Alice"}`

#### **Approach 1: Using `default` parameter**
```python
import json  # Library for handling JSON data

class Person:
    def __init__(self, name):
        self.name = name

def encode_person(obj):  # Custom logic to convert object to a JSON-serializable type (like dict)
    if isinstance(obj, Person):  # Check if object is of our custom class
        return {'name': obj.name}  # Return a dictionary representation
    raise TypeError("Not serializable")

p = Person("Alice")
# Pass the converter function to the 'default' argument
print(json.dumps(p, default=encode_person)) 
```

#### **Approach 2: Subclassing `JSONEncoder`**
```python
import json

class PersonEncoder(json.JSONEncoder):  # Inherit from standard encoder
    def default(self, obj):  # Override the default method
        if isinstance(obj, Person):
            return {'name': obj.name}  # Custom formatting
        return super().default(obj)  # Fallback to standard behavior for other types

p = Person("Bob")
# Specify the custom class in 'cls' argument
print(json.dumps(p, cls=PersonEncoder))
```

---

### **40. Modern String Formatting (`f-strings` features)**

**Sample Input:** `val=10`
**Sample Output:** `val=10` (Self-documenting f-string)

#### **Approach 1: Standard F-string**
```python
name = "Alice"
age = 30
# Embed variables directly inside curly braces for clarity and performance
print(f"{name} is {age} years old")
```

#### **Approach 2: Self-documenting (Python 3.8+)**
```python
x = 10
y = 25
print(f"{x=}, {y=}")  # Output: x=10, y=25
print(f"{x+y=}")      # Output: x+y=35 (Calculations)
```


---

## **Section 5: Modern Python & Best Practices (Q41-50)**

### **41. Basic Asynchronous Function (`async`/`await`)**

**Sample Input:** `await say_hi()`
**Sample Output:** `Hello... (pause 1s) ...World`

#### **Approach 1: Simple Async/Await**
```python
import asyncio  # Import the asyncio library for concurrent programming

async def say_hello():  # 'async' keyword defines a coroutine function
    print("Hello")
    await asyncio.sleep(1)  # 'await' yields control back to the event loop during the 1s delay
    print("World")

# To run a coroutine, you must use an event loop
asyncio.run(say_hello())  
```

#### **Approach 2: Returning values from Async**
```python
import asyncio

async def get_data():
    await asyncio.sleep(0.5)  # Simulate I/O latency
    return {"data": 100}  # Coroutines can return values just like normal functions

async def main():
    result = await get_data()  # Execution waits here until get_data() completes
    print(result)

asyncio.run(main())
```

---

### **42. Running Tasks Concurrently (`asyncio.gather`)**

**Sample Input:** `Task A (1s), Task B (1s)`
**Sample Output:** `Finished in approx 1s` (Total, not 2s)

#### **Approach 1: Using `gather`**
```python
import asyncio
import time

async def task(name, delay):
    await asyncio.sleep(delay)  # Non-blocking sleep
    print(f"Task {name} done")

async def main():
    start = time.perf_counter()  # Start high-resolution timer
    # asyncio.gather runs multiple coroutines concurrently and waits for all to finish
    await asyncio.gather(
        task("A", 1),
        task("B", 1)
    )
    print(f"Time: {time.perf_counter() - start:.2f}s")  # Should be ~1.00s

asyncio.run(main())
```

#### **Approach 2: Creating Tasks (`create_task`)**
```python
async def main():
    # create_task schedules the coroutine to run on the event loop immediately
    t1 = asyncio.create_task(task("A", 1))
    t2 = asyncio.create_task(task("B", 1))
    
    # You can do other work here while T1 and T2 run in the background
    
    await t1  # Wait for T1 to finish
    await t2  # Wait for T2 to finish
```

---

### **43. Type Hinting (Generics and Optional)**

**Sample Input:** `func(10)`
**Sample Output:** `10` (With IDE/Linter support for types)

#### **Approach 1: Basic Hints & Optional**
```python
from typing import Optional, List  # Import type hint utilities

# 'Optional[int]' means the argument can be an integer OR None
def greet(name: Optional[str] = None) -> str:
    if name:
        return f"Hello {name}"
    return "Hello Stranger"

# 'List[int]' specifies that the argument must be a list containing only integers
def process_items(items: List[int]) -> int:
    return sum(items)
```

#### **Approach 2: Union and Any (Python 3.10+ syntax)**
```python
# New pipes syntax '|' replaces Union for cleaner code
def process(data: int | str) -> None:
    print(data)

# 'Any' is used when a variable can truly be of any type
from typing import Any
def log(obj: Any):
    print(f"Logging: {obj}")
```

---

### **44. Managing Environment Variables (`os.getenv`)**

**Sample Input:** Env var `DB_URL`
**Sample Output:** `localhost:5432`

#### **Approach 1: Using `os.environ`**
```python
import os  # module for operating system dependent functionality

# dictionary-like access to environment variables
# Note: Raises KeyError if 'SECRET_KEY' is not set
key = os.environ['SECRET_KEY'] 
```

#### **Approach 2: Safe access with `os.getenv`**
```python
import os

# getenv returns None (or a default) if the variable is missing, preventing crashes
db_url = os.getenv('DB_URL', 'localhost:5432')  # Provide a fallback value
print(f"Connecting to {db_url}")
```

---

### **45. Using `logging` instead of `print`**

**Sample Input:** `logging.info("Start")`
**Sample Output:** `INFO:root:Start` (With timestamp/level)

#### **Approach 1: Basic Configuration**
```python
import logging  # built-in logging facility

# Configure logger: set level and output format
logging.basicConfig(level=logging.INFO, format='%(levelname)s: %(message)s')

logging.debug("Debug info (hidden)")  # Won't show because level is INFO
logging.info("System Started")         # Standard info message
logging.error("An error occurred")     # High-priority error message
```

#### **Approach 2: Logging to a File**
```python
import logging

# Direct output to 'app.log' instead of the console
logging.basicConfig(filename='app.log', level=logging.WARNING)
logging.warning("This goes to the file")
```

---

### **46. The `if __name__ == "__main__":` Guard**

**Sample Input:** `python script.py` vs `import script`
**Sample Output:** Executes only when run directly

#### **Approach 1: Standard usage**
```python
def main():
    print("Executing core logic")

# This block ensures code doesn't run automatically when the file is imported elsewhere
if __name__ == "__main__":
    main()  # Only runs if script.py is executed directly via CLI
```

#### **Approach 2: Why it's used**
```python
# script_a.py
print("Always runs on import")
if __name__ == "__main__":
    print("Only runs when script_a is the MAIN entry point")
```

---

### **47. Unit Testing Basics (`unittest`)**

**Sample Input:** `test_add(5, 5)`
**Sample Output:** `OK`

#### **Approach 1: `unittest` Module**
```python
import unittest  # Built-in testing framework

def add(a, b):
    return a + b

class TestMath(unittest.TestCase):  # Inherit from TestCase
    def test_add(self):  # Method name must start with 'test'
        self.assertEqual(add(2, 3), 5)  # Assert that the result matches expected
        self.assertNotEqual(add(2, 3), 6)

if __name__ == '__main__':
    unittest.main()  # Run the test suite
```

#### **Approach 2: `pytest` style (Simple Asserts)**
```python
# No class needed, uses standard 'assert' keyword
def test_multiply():
    assert 2 * 3 == 6  # Simple boolean check
```

---

### **48. Virtual Environments (Concept)**

**Sample Input:** `python -m venv venv`
**Sample Output:** A local isolated Python environment

#### **Approach 1: Creation & Activation (Windows)**
```powershell
# Commands run in terminal, not in Python script
python -m venv myenv       # Create a new environment folder 'myenv'
.\myenv\Scripts\activate   # Activate the environment (paths change)
```

#### **Approach 2: Why isolate?**
```text
# Project A requires Django 3.2
# Project B requires Django 4.0
# Virtual environments allow both to exist on one machine without conflict.
```

---

### **49. Command Line Arguments (`argparse`)**

**Sample Input:** `python script.py --name Alice`
**Sample Output:** `Hello Alice`

#### **Approach 1: Using `sys.argv` (Simple)**
```python
import sys  # System-specific parameters

# sys.argv[0] is the script name. args start from index 1.
if len(sys.argv) > 1:
    print(f"Argument received: {sys.argv[1]}")
```

#### **Approach 2: Using `argparse` (Robust)**
```python
import argparse  # Highly recommended for production CLI tools

parser = argparse.ArgumentParser(description="A greeting script")
# Define an expected argument '--name'
parser.add_argument('--name', type=str, help='Your name', required=True)

args = parser.parse_args()  # Automatically parses sys.argv
print(f"Hello {args.name}")
```

---

### **50. Dependency Management (`pip`)**

**Sample Input:** `pip install requests`
**Sample Output:** Package installed and ready to import

#### **Approach 1: Requirements file**
```text
# requirements.txt
# This file lists all external dependencies for a project
requests==2.28.1  # Specific version for stability
pandas>=1.4.0      # Minimum version requirement
```

#### **Approach 2: Commands**
```bash
# Command to install all dependencies listed in a requirements file
pip install -r requirements.txt  

# Command to generate a requirements file based on currently installed packages
pip freeze > requirements.txt    
```

---


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
