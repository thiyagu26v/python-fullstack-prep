# Python Coding Round - Company 9
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Format User Info (5 Marks)
Write a function that takes a user dictionary and returns a formatted string.

**Input:**
```
{"name": "John", "age": 25, "city": "NYC"}
```

**Output:**
```
"User John is 25 years old and lives in NYC."
```

---

## Question 2: Product Magic Methods (5 Marks)
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

## Question 3: Write Lines to File (5 Marks)
Write a function that takes a list of strings and writes each to a new line in file.

**Input:**
```
write_lines("output.txt", ["Line 1", "Line 2", "Line 3"])
```

**Output:**
```
True  # File created with 3 lines
```

---

## Question 4: Extract JSON Fields (5 Marks)
Write a function that parses JSON string and extracts specific fields.

**Input:**
```
json_str = '{"name": "John", "age": 25, "email": "john@example.com"}'
extract_fields(json_str, ["name", "email"])
```

**Output:**
```
{"name": "John", "email": "john@example.com"}
```

---

## Question 5: Title Case (5 Marks)
Write a function that converts string to title case, handling multiple spaces.

**Input:**
```
"hello   WORLD   python"
```

**Output:**
```
"Hello World Python"
```

---

## Question 6: Insert User (5 Marks)
Write a function that inserts new user using parameterized queries.

**Input:**
```
insert_user(cursor, "John Doe", "john@example.com")
```

**Output:**
```
1  # Returns user_id of newly inserted user
```

---

## Question 7: Rate Limiter (5 Marks)
Create a rate limiter class for web scraping to avoid overloading servers.

**Input:**
```
limiter = RateLimiter(requests_per_second=2)
limiter.wait()  # Ensures 0.5s gap between requests
```

**Output:**
```
# Waits appropriate time before allowing next request
```

---

## Question 8: Timezone Conversion (5 Marks)
Write a function that converts time between timezones using offset hours.

**Input:**
```
utc_time = datetime(2024, 1, 15, 12, 0, 0)
convert_timezone(utc_time, from_offset=0, to_offset=5.5)  # UTC to IST
```

**Output:**
```
datetime(2024, 1, 15, 17, 30, 0)
```

---

## Question 9: Zip to Dictionary (5 Marks)
Write a function that combines two lists into dictionary.

**Input:**
```
keys = ["a", "b", "c"]
values = [1, 2, 3]
zip_to_dict(keys, values)
```

**Output:**
```
{"a": 1, "b": 2, "c": 3}
```

---

## Question 10: User Registration Validator (5 Marks)
Write a function that validates user registration data with multiple rules.

**Input:**
```
data = {
    "username": "john_doe",
    "email": "john@test.com",
    "password": "Pass123!",
    "age": 25
}
validate_registration(data)
```

**Output:**
```
{"valid": True, "errors": []}

# Invalid case
{"valid": False, "errors": ["Password must contain special character", "Age must be 18+"]}
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
