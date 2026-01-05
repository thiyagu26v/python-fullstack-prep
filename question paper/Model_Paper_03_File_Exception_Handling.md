# Python Coding Round - Model Paper 03
## Topic: File Handling & Exception Management
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Word Counter (5 Marks)
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

## Question 2: Write Lines to File (5 Marks)
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

## Question 3: Log with Timestamp (5 Marks)
Write a function that appends a log message with timestamp to a log file.

**Input:**
```
log_message("app.log", "User logged in")
```

**Output:**
```
# Appends: "2024-01-15 10:30:00 - User logged in"
True
```

---

## Question 4: Read CSV (5 Marks)
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

## Question 5: Write CSV (5 Marks)
Write a function that takes list of dictionaries and writes them to CSV file.

**Input:**
```
data = [{"name": "John", "age": 25}, {"name": "Jane", "age": 30}]
write_csv("output.csv", data)
```

**Output:**
```
True  # CSV file created with headers and data
```

---

## Question 6: Safe Division (5 Marks)
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

## Question 7: Custom Age Exception (5 Marks)
Create InvalidAgeError exception and use in age validation function.

**Input:**
```
validate_age(25)
validate_age(-5)
```

**Output:**
```
"Valid age"
# Raises InvalidAgeError
```

---

## Question 8: Try-Except-Else-Finally (5 Marks)
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

## Question 9: JSON Read/Write (5 Marks)
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

## Question 10: Database Context Manager (5 Marks)
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

## Evaluation Criteria:
- Code correctness: 50%
- Exception handling: 30%
- Code readability: 20%
