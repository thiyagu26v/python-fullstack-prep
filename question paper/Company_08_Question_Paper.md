# Python Coding Round - Company 8
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Compare Lists (5 Marks)
Write a function that returns common elements and elements in either list but not both.

**Input:**
```
[1, 2, 3, 4], [3, 4, 5, 6]
```

**Output:**
```
{"common": [3, 4], "different": [1, 2, 5, 6]}
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

## Question 3: Database Context Manager (5 Marks)
Create a context manager class for database connection simulation.

**Input:**
```
with DatabaseConnection("mydb") as db:
    db.query("SELECT * FROM users")
```

**Output:**
```
"Connected to mydb"
"Executing: SELECT * FROM users"
"Disconnected"
```

---

## Question 4: Pretty Print JSON (5 Marks)
Write a function that converts Python object to formatted JSON string.

**Input:**
```
data = {"user": {"name": "John", "scores": [85, 90]}}
to_json(data)
```

**Output:**
```
{
  "user": {
    "name": "John",
    "scores": [85, 90]
  }
}
```

---

## Question 5: Extract Phone Numbers (5 Marks)
Write a function that extracts all phone numbers from text using regex.

**Input:**
```
"Call me at 123-456-7890 or (098) 765-4321"
```

**Output:**
```
["123-456-7890", "(098) 765-4321"]
```

---

## Question 6: Delete User (5 Marks)
Write a function that deletes user by ID and returns success status.

**Input:**
```
delete_user(cursor, user_id=1)
```

**Output:**
```
True  # If deleted
False # If not found
```

---

## Question 7: Extract Meta Tags (5 Marks)
Write a function that extracts meta tag information (title, description, keywords) from HTML.

**Input:**
```
html = '<head><title>My Page</title><meta name="description" content="A sample page"></head>'
extract_meta(html)
```

**Output:**
```
{"title": "My Page", "description": "A sample page", "keywords": ""}
```

---

## Question 8: Parse Date String (5 Marks)
Write a function that parses date strings in multiple formats.

**Input:**
```
parse_date("2024-01-15")
parse_date("15/01/2024")
parse_date("January 15, 2024")
```

**Output:**
```
datetime(2024, 1, 15)  # Returns datetime objects
```

---

## Question 9: Sort by Multiple Keys (5 Marks)
Write a function that sorts list of dictionaries by multiple keys.

**Input:**
```
data = [
    {"name": "Bob", "age": 25},
    {"name": "Alice", "age": 25},
    {"name": "Charlie", "age": 30}
]
sort_by_keys(data, ["age", "name"])
```

**Output:**
```
[{"name": "Alice", "age": 25}, {"name": "Bob", "age": 25}, {"name": "Charlie", "age": 30}]
```

---

## Question 10: API Rate Tracker (5 Marks)
Write a class that tracks API calls per user with limits.

**Input:**
```
tracker = RateTracker(limit=5, window_seconds=60)
tracker.can_proceed("user123")  # 1st call
# ... 5th call
tracker.can_proceed("user123")  # 6th call - should be blocked
tracker.get_remaining("user123")
```

**Output:**
```
True  # Calls 1-5
False  # 6th call blocked
0  # Remaining calls
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
