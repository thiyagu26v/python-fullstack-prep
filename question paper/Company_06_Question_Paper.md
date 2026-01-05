# Python Coding Round - Company 6
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Flatten List (5 Marks)
Write a function that flattens a nested list (one level deep).

**Input:**
```
[[1, 2], [3, 4], [5, 6]]
```

**Output:**
```
[1, 2, 3, 4, 5, 6]
```

---

## Question 2: Static MathUtils Class (5 Marks)
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

## Question 3: Try-Except-Else-Finally (5 Marks)
Write a function demonstrating all four blocks: try, except, else, finally.

**Input:**
```
process_file("exists.txt")
process_file("missing.txt")
```

**Output:**
```
"File processed successfully. Cleanup done."
"File not found. Cleanup done."
```

---

## Question 4: Filter JSON Array (5 Marks)
Write a function that filters list of objects based on criteria.

**Input:**
```
products = [
    {"name": "Laptop", "price": 1000, "category": "electronics"},
    {"name": "Phone", "price": 500, "category": "electronics"},
    {"name": "Desk", "price": 200, "category": "furniture"}
]
filter_items(products, {"category": "electronics", "price": {"min": 600}})
```

**Output:**
```
[{"name": "Laptop", "price": 1000, "category": "electronics"}]
```

---

## Question 5: Find All Indices (5 Marks)
Write a function that finds all occurrences of substring and returns indices.

**Input:**
```
text = "abcabcabc"
substring = "abc"
```

**Output:**
```
[0, 3, 6]
```

---

## Question 6: Create Users Table (5 Marks)
Write a function that creates users table with id, name, email, created_at fields.

**Input:**
```
create_users_table(cursor)
```

**Output:**
```
True  # Table created successfully
```

---

## Question 7: CSS Selector Extraction (5 Marks)
Write a function that extracts elements using CSS selectors from HTML.

**Input:**
```
html = '<div class="product"><span class="price">$100</span></div>'
extract_by_selector(html, ".product .price")
```

**Output:**
```
["$100"]
```

---

## Question 8: Cache Decorator (5 Marks)
Write a caching decorator that stores function results.

**Input:**
```
@cache
def expensive_function(n):
    return n * n

expensive_function(5)  # Computes
expensive_function(5)  # Returns cached
```

**Output:**
```
25  # Both calls return 25, second is from cache
```

---

## Question 9: Rotate List (5 Marks)
Write a function that rotates list by k positions.

**Input:**
```
rotate_list([1, 2, 3, 4, 5], 2)
```

**Output:**
```
[4, 5, 1, 2, 3]  # Rotated right by 2
```

---

## Question 10: Config Parser (5 Marks)
Write a function that parses environment-style config string.

**Input:**
```
config_str = """
DATABASE_URL=postgres://localhost:5432
DEBUG=true
MAX_CONNECTIONS=10
# This is a comment
API_KEY=secret123
"""
parse_config(config_str)
```

**Output:**
```
{"DATABASE_URL": "postgres://localhost:5432", "DEBUG": "true", "MAX_CONNECTIONS": "10", "API_KEY": "secret123"}
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
