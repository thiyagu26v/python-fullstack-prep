# Python Coding Round - Model Paper 06
## Topic: Database & SQL Operations (Using Python)
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Create Connection (5 Marks)
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

## Question 2: Create Users Table (5 Marks)
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

## Question 3: Insert User (5 Marks)
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

## Question 4: Fetch All Users (5 Marks)
Write a function that retrieves all users as list of dictionaries.

**Input:**
```
get_all_users(cursor)
```

**Output:**
```
[{"id": 1, "name": "John", "email": "john@example.com", "created_at": "..."}]
```

---

## Question 5: Search Users (5 Marks)
Write a function that searches users by name (partial match, case-insensitive).

**Input:**
```
search_users(cursor, "john")
```

**Output:**
```
[{"id": 1, "name": "John Doe", ...}, {"id": 5, "name": "Johnny", ...}]
```

---

## Question 6: Update User (5 Marks)
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

## Question 7: Delete User (5 Marks)
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

## Question 8: Bulk Insert (5 Marks)
Write a function that inserts multiple users in single transaction.

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

## Question 9: User Statistics (5 Marks)
Write a function that returns user stats: total count and users created today.

**Input:**
```
get_user_stats(cursor)
```

**Output:**
```
{"total_users": 10, "users_today": 3}
```

---

## Question 10: Database Context Manager (5 Marks)
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
- Code correctness: 50%
- SQL query correctness: 30%
- Security (parameterized queries): 20%
