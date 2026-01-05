# Python Coding Round - Company 10
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

## Question 2: Find Frequency (5 Marks)
Write a function that returns the most frequent element in a list.

**Input:**
```
[1, 2, 2, 3, 3, 3, 4]
```

**Output:**
```
3  # Appeared 3 times
```

---

## Question 3: Create Database Connection (5 Marks)
Write a function that creates SQLite database connection and returns cursor.

**Input:**
```
conn, cursor = create_connection("my_database.db")
```

**Output:**
```
# Returns connection and cursor objects
```

---

## Question 4: Extract Paragraphs (5 Marks)
Write a function that extracts all paragraph text from HTML.

**Input:**
```
html = '<p>First paragraph</p><div>Not this</div><p>Second paragraph</p>'
extract_paragraphs(html)
```

**Output:**
```
["First paragraph", "Second paragraph"]
```

---

## Question 5: Date Formatting (5 Marks)
Write a function that formats date object into various string formats.

**Input:**
```
dt = datetime(2024, 1, 15, 14, 30, 0)
format_date(dt, "short")
format_date(dt, "long")
format_date(dt, "iso")
```

**Output:**
```
"01/15/2024"
"January 15, 2024"
"2024-01-15T14:30:00"
```

---

## Question 6: Difference of Lists (5 Marks)
Write a function that returns elements in first list but not in second.

**Input:**
```
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
difference(list1, list2)
```

**Output:**
```
[1, 2]
```

---

## Question 7: Fetch All Users (5 Marks)
Write a function that retrieves all users from database as list of dictionaries.

**Input:**
```
get_all_users(cursor)
```

**Output:**
```
[{"id": 1, "name": "John", "email": "john@example.com", "created_at": "..."}]
```

---

## Question 8: Form Validator (5 Marks)
Write a reusable form validator with custom rules.

**Input:**
```
rules = {
    "name": {"required": True, "min_length": 2},
    "email": {"required": True, "pattern": "email"},
    "age": {"required": False, "min_value": 0}
}
data = {"name": "J", "email": "invalid"}
validate_form(data, rules)
```

**Output:**
```
{"valid": False, "errors": {"name": "Minimum length is 2", "email": "Invalid email format"}}
```

---

## Question 9: URL Shortener (5 Marks)
Write a function that generates short codes for URLs and stores them.

**Input:**
```
shortener = URLShortener()
code = shortener.shorten("https://example.com/very/long/url")
original = shortener.get_original(code)
```

**Output:**
```
"abc123"  # Generated short code
"https://example.com/very/long/url"  # Retrieved original
```

---

## Question 10: Database Manager Context (5 Marks)
Create a context manager class for database operations with auto-commit.

**Input:**
```
with DatabaseManager("app.db") as db:
    db.execute("INSERT INTO users (name, email) VALUES (?, ?)", ("Test", "test@test.com"))
```

**Output:**
```
# Auto-commits on success, rollbacks on error
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
