# Python Coding Round - Company 3
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Even Squares (5 Marks)
Write a function that returns all even numbers from a list, squared.

**Input:**
```
[1, 2, 3, 4, 5, 6]
```

**Output:**
```
[4, 16, 36]
```

---

## Question 2: Bank Account Class (5 Marks)
Create BankAccount class with private balance. Include deposit, withdraw, get_balance methods.

**Input:**
```
account = BankAccount(100)
account.deposit(50)
account.get_balance()
account.withdraw(30)
account.get_balance()
```

**Output:**
```
150
120
```

---

## Question 3: Custom Exception (5 Marks)
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

## Question 4: Paginate Items (5 Marks)
Write a function that paginates list of items with page info.

**Input:**
```
items = list(range(1, 101))  # 100 items
paginate(items, page=2, per_page=10)
```

**Output:**
```
{"data": [11,12,13,14,15,16,17,18,19,20], "page": 2, "per_page": 10, "total_items": 100, "total_pages": 10}
```

---

## Question 5: Extract Hashtags (5 Marks)
Write a function that extracts all hashtags from social media post.

**Input:**
```
"Check out #Python #programming! Learn #WebDev today"
```

**Output:**
```
["Python", "programming", "WebDev"]
```

---

## Question 6: Search Users in Database (5 Marks)
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

## Question 7: Relative Time (5 Marks)
Write a function that returns human-readable relative time.

**Input:**
```
past = datetime.now() - timedelta(hours=2)
relative_time(past)

future = datetime.now() + timedelta(days=3)
relative_time(future)
```

**Output:**
```
"2 hours ago"
"in 3 days"
```

---

## Question 8: HTML to Text (5 Marks)
Write a function that converts HTML to clean text, removing tags and extra spaces.

**Input:**
```
html = '<div><p>Hello   <b>World</b></p>\n\n<p>Test</p></div>'
html_to_text(html)
```

**Output:**
```
"Hello World Test"
```

---

## Question 9: Chunk List (5 Marks)
Write a function that splits a list into chunks of specified size.

**Input:**
```
chunk_list([1, 2, 3, 4, 5, 6, 7], 3)
```

**Output:**
```
[[1, 2, 3], [4, 5, 6], [7]]
```

---

## Question 10: Token Generator (5 Marks)
Write a function that generates and validates simple auth tokens.

**Input:**
```
token = generate_token(user_id=123, expires_in=3600)
is_valid = validate_token(token)
```

**Output:**
```
"eyJ1c2VyX2lkIjoxMjMsImV4cCI6MTY..."  # Base64 encoded token
True  # Token is valid
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
