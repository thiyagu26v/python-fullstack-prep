# Python Coding Round - Company 1
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Reverse Words (5 Marks)
Write a function that reverses the order of words in a string.

**Input:**
```
"Hello World Python"
```

**Output:**
```
"Python World Hello"
```

---

## Question 2: Rectangle Class (5 Marks)
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

## Question 3: Merge Dictionaries (5 Marks)
Write a function that merges two dictionaries. If a key exists in both, add their values.

**Input:**
```
{'a': 1, 'b': 2}, {'b': 3, 'c': 4}
```

**Output:**
```
{'a': 1, 'b': 5, 'c': 4}
```

---

## Question 4: Email Validator (5 Marks)
Write a function that validates email address using regex.

**Input:**
```
is_valid_email("user@example.com")
is_valid_email("user@.com")
```

**Output:**
```
True
False
```

---

## Question 5: Safe Division (5 Marks)
Write a function that divides two numbers with proper exception handling.

**Input:**
```
safe_divide(10, 2)
safe_divide(10, 0)
safe_divide(10, "a")
```

**Output:**
```
5.0
"Division by zero"
"Invalid type"
```

---

## Question 6: Flatten Nested JSON (5 Marks)
Write a function that flattens nested JSON to single-level dictionary.

**Input:**
```
{"user": {"name": "John", "address": {"city": "NYC"}}}
```

**Output:**
```
{"user.name": "John", "user.address.city": "NYC"}
```

---

## Question 7: Word Counter from File (5 Marks)
Write a function that reads a text file and returns total word count.

**Input:**
```
# File contains: "Hello World Python Programming"
count_words("sample.txt")
```

**Output:**
```
4
```

---

## Question 8: Shopping Cart Total (5 Marks)
Write a function that calculates shopping cart total with discounts.

**Input:**
```
cart = [
    {"name": "Laptop", "price": 1000, "quantity": 1},
    {"name": "Mouse", "price": 50, "quantity": 2}
]
calculate_cart(cart, discount_percent=10)
```

**Output:**
```
{"subtotal": 1100, "discount": 110, "total": 990}
```

---

## Question 9: Extract Links from HTML (5 Marks)
Write a function that extracts all links from HTML string.

**Input:**
```
html = '<a href="https://example.com">Link 1</a><a href="https://test.com">Link 2</a>'
extract_links(html)
```

**Output:**
```
["https://example.com", "https://test.com"]
```

---

## Question 10: Calculate Age (5 Marks)
Write a function that calculates age from birth date.

**Input:**
```
calculate_age(date(1990, 5, 15))
```

**Output:**
```
33  # Or current age based on today
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
