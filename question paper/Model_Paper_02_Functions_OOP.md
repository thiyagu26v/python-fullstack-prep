# Python Coding Round - Model Paper 02
## Topic: Functions & Object-Oriented Programming
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Price Calculator (5 Marks)
Write a function that calculates total price with optional tax and discount percentages.

**Input:**
```
calculate_price(100, tax=10, discount=5)
```

**Output:**
```
105.0
```

---

## Question 2: Args Summary (5 Marks)
Write a function that accepts *args and **kwargs and returns a summary dictionary.

**Input:**
```
summarize(1, 2, 3, name="John", age=25)
```

**Output:**
```
{"args_count": 3, "args_sum": 6, "kwargs": {"name": "John", "age": 25}}
```

---

## Question 3: Temperature Converter (5 Marks)
Using lambda and map, convert list of temperatures from Celsius to Fahrenheit.

**Input:**
```
[0, 20, 37, 100]
```

**Output:**
```
[32.0, 68.0, 98.6, 212.0]
```

---

## Question 4: Rectangle Class (5 Marks)
Create a Rectangle class with length and width. Include methods for area and perimeter.

**Input:**
```
rect = Rectangle(5, 3)
rect.area()
rect.perimeter()
```

**Output:**
```
15
16
```

---

## Question 5: Vehicle Inheritance (5 Marks)
Create Vehicle base class and Car subclass with additional num_doors attribute.

**Input:**
```
car = Car("Toyota", "Camry", 4)
car.display()
```

**Output:**
```
"Toyota Camry with 4 doors"
```

---

## Question 6: MathUtils Static Methods (5 Marks)
Create MathUtils class with static methods for add, subtract, multiply, divide.

**Input:**
```
MathUtils.add(5, 3)
MathUtils.divide(10, 0)
```

**Output:**
```
8
"Cannot divide by zero"
```

---

## Question 7: User Counter (5 Marks)
Create User class that tracks instance count using class method.

**Input:**
```
user1 = User("Alice")
user2 = User("Bob")
User.get_user_count()
```

**Output:**
```
2
```

---

## Question 8: Circle with Property (5 Marks)
Create Circle class with radius property and auto-calculated area property.

**Input:**
```
circle = Circle(5)
circle.area
circle.radius = 10
circle.area
```

**Output:**
```
78.54
314.16
```

---

## Question 9: Bank Account (5 Marks)
Create BankAccount class with private balance. Include deposit, withdraw, get_balance methods.

**Input:**
```
account = BankAccount(100)
account.deposit(50)
account.get_balance()
account.withdraw(30)
account.get_balance()
```

**Output:**
```
150
120
```

---

## Question 10: Product Magic Methods (5 Marks)
Create Product class with __str__ and __add__ magic methods.

**Input:**
```
p1 = Product("Laptop", 1000)
p2 = Product("Mouse", 50)
print(p1)
combined = p1 + p2
print(combined)
```

**Output:**
```
"Laptop: $1000"
"Laptop + Mouse: $1050"
```

---

## Evaluation Criteria:
- Code correctness: 60%
- OOP principles: 20%
- Code readability: 20%
