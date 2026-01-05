# Python Coding Round - Company 2
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Remove Duplicates (5 Marks)
Write a function that removes duplicates from a list while maintaining the original order.

**Input:**
```
[1, 2, 2, 3, 4, 4, 5]
```

**Output:**
```
[1, 2, 3, 4, 5]
```

---

## Question 2: Password Validator (5 Marks)
Write a function to validate password. Rules: min 8 chars, must contain digit, must contain uppercase.

**Input:**
```
"Hello123"
"hello123"
```

**Output:**
```
True
False
```

---

## Question 3: Vehicle Inheritance (5 Marks)
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

## Question 4: Parse Query String (5 Marks)
Write a function that parses URL query string into dictionary.

**Input:**
```
"name=John&age=25&city=NYC"
```

**Output:**
```
{"name": "John", "age": "25", "city": "NYC"}
```

---

## Question 5: Read CSV (5 Marks)
Write a function that reads a CSV file and returns list of dictionaries.

**Input:**
```
# CSV: name,age,city
#      John,25,NYC
read_csv("data.csv")
```

**Output:**
```
[{"name": "John", "age": "25", "city": "NYC"}]
```

---

## Question 6: Slug Generator (5 Marks)
Write a function that converts title to URL-friendly slug.

**Input:**
```
"Hello World! This is Python 3.0"
```

**Output:**
```
"hello-world-this-is-python-3-0"
```

---

## Question 7: Group by Key (5 Marks)
Write a function that groups list of dictionaries by a specified key.

**Input:**
```
data = [
    {"name": "John", "dept": "IT"},
    {"name": "Jane", "dept": "HR"},
    {"name": "Bob", "dept": "IT"}
]
group_by(data, "dept")
```

**Output:**
```
{"IT": [{"name": "John", "dept": "IT"}, {"name": "Bob", "dept": "IT"}], "HR": [{"name": "Jane", "dept": "HR"}]}
```

---

## Question 8: Retry Decorator (5 Marks)
Write a decorator that retries function on failure with configurable attempts.

**Input:**
```
@retry(max_attempts=3, delay=1)
def unstable_function():
    # May fail sometimes
    pass
```

**Output:**
```
# Retries up to 3 times with 1 second delay between attempts
```

---

## Question 9: API Response Builder (5 Marks)
Write a function that creates standardized API response format.

**Input:**
```
create_response(True, {"user_id": 123}, "User created")
create_response(False, None, None, "User not found")
```

**Output:**
```
{"success": True, "data": {"user_id": 123}, "message": "User created", "error": None}
{"success": False, "data": None, "message": None, "error": "User not found"}
```

---

## Question 10: Extract Images from HTML (5 Marks)
Write a function that extracts all image src and alt attributes from HTML.

**Input:**
```
html = '<img src="cat.jpg" alt="Cat"><img src="dog.jpg" alt="Dog">'
extract_images(html)
```

**Output:**
```
[{"src": "cat.jpg", "alt": "Cat"}, {"src": "dog.jpg", "alt": "Dog"}]
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
