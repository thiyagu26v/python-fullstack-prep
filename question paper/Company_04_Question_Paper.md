# Python Coding Round - Company 4
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Character Count (5 Marks)
Write a function that takes a string and returns a dictionary with the count of each character.

**Input:**
```
"hello"
```

**Output:**
```
{'h': 1, 'e': 1, 'l': 2, 'o': 1}
```

---

## Question 2: Temperature Converter (5 Marks)
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

## Question 3: JSON Read/Write (5 Marks)
Write functions to read and write JSON data to a file.

**Input:**
```
data = {"users": [{"name": "John"}]}
write_json("data.json", data)
read_json("data.json")
```

**Output:**
```
True
{"users": [{"name": "John"}]}
```

---

## Question 4: Validate Request (5 Marks)
Write a function that validates request data against required fields.

**Input:**
```
required = ["name", "email", "password"]
data = {"name": "John", "email": "john@test.com"}
validate_request(data, required)
```

**Output:**
```
{"valid": False, "missing": ["password"]}
```

---

## Question 5: Camel to Snake Case (5 Marks)
Write a function that converts camelCase to snake_case.

**Input:**
```
"getUserProfile"
"HTTPResponseCode"
```

**Output:**
```
"get_user_profile"
"http_response_code"
```

---

## Question 6: Bulk Insert Users (5 Marks)
Write a function that inserts multiple users in single database transaction.

**Input:**
```
users = [("Alice", "alice@test.com"), ("Bob", "bob@test.com")]
bulk_insert_users(conn, cursor, users)
```

**Output:**
```
2  # Number of users inserted
```

---

## Question 7: Parse HTML Table (5 Marks)
Write a function that converts HTML table to list of dictionaries.

**Input:**
```
html = '<table><tr><th>Name</th><th>Age</th></tr><tr><td>John</td><td>25</td></tr></table>'
parse_table(html)
```

**Output:**
```
[{"Name": "John", "Age": "25"}]
```

---

## Question 8: Working Days Calculator (5 Marks)
Write a function that calculates working days between two dates (excluding weekends).

**Input:**
```
working_days(date(2024, 1, 1), date(2024, 1, 15))
```

**Output:**
```
10  # Excluding Saturdays and Sundays
```

---

## Question 9: Two Sum (5 Marks)
Write a function that finds two numbers in list that add up to target.

**Input:**
```
nums = [2, 7, 11, 15]
target = 9
two_sum(nums, target)
```

**Output:**
```
[0, 1]  # Indices of 2 and 7
```

---

## Question 10: Leaderboard Manager (5 Marks)
Write a class that manages a game leaderboard.

**Input:**
```
board = Leaderboard()
board.add_score("Alice", 100)
board.add_score("Bob", 150)
board.add_score("Alice", 200)  # Updates Alice's score
board.get_top(2)
```

**Output:**
```
[{"name": "Alice", "score": 200}, {"name": "Bob", "score": 150}]
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
