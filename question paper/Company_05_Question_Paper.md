# Python Coding Round - Company 5
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Filter Adults (5 Marks)
Write a function that takes a list of tuples (name, age) and returns names of people 18 or older.

**Input:**
```
[("Alice", 20), ("Bob", 16), ("Charlie", 25)]
```

**Output:**
```
["Alice", "Charlie"]
```

---

## Question 2: User Counter Class (5 Marks)
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

## Question 4: Transform Users (5 Marks)
Write a function that transforms list of user objects to simplified format.

**Input:**
```
[{"id": 1, "first_name": "John", "last_name": "Doe", "email": "john@test.com", "extra": "data"}]
```

**Output:**
```
[{"id": 1, "full_name": "John Doe", "email": "john@test.com"}]
```

---

## Question 5: Template Renderer (5 Marks)
Write a function that replaces {{placeholders}} with dictionary values.

**Input:**
```
template = "Hello, {{name}}! Welcome to {{city}}."
values = {"name": "John", "city": "NYC"}
```

**Output:**
```
"Hello, John! Welcome to NYC."
```

---

## Question 6: Update User in Database (5 Marks)
Write a function that updates user's name and/or email by ID.

**Input:**
```
update_user(cursor, user_id=1, name="Jane Doe", email="jane@example.com")
```

**Output:**
```
True  # If updated
False # If not found
```

---

## Question 7: Extract Form Fields (5 Marks)
Write a function that extracts all form input fields with names and types from HTML.

**Input:**
```
html = '<form><input type="text" name="username"><input type="email" name="email"></form>'
extract_form_fields(html)
```

**Output:**
```
[{"name": "username", "type": "text"}, {"name": "email", "type": "email"}]
```

---

## Question 8: UUID Generator (5 Marks)
Write a function that generates unique identifiers of different types.

**Input:**
```
generate_id("uuid")
generate_id("short")
generate_id("numeric")
```

**Output:**
```
"550e8400-e29b-41d4-a716-446655440000"
"a1b2c3d4"
"123456789012"
```

---

## Question 9: Find Duplicates (5 Marks)
Write a function that finds all duplicate elements in a list.

**Input:**
```
[1, 2, 2, 3, 3, 3, 4]
```

**Output:**
```
[2, 3]
```

---

## Question 10: Event Scheduler (5 Marks)
Write a class that manages scheduled events with time slots (no overlapping).

**Input:**
```
scheduler = EventScheduler()
scheduler.add_event("Meeting", "10:00", "11:00")
scheduler.add_event("Lunch", "10:30", "11:30")  # Should fail - overlap
scheduler.get_events()
```

**Output:**
```
True  # First event added
False  # Second event overlaps
[{"name": "Meeting", "start": "10:00", "end": "11:00"}]
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
