# Python Coding Round - Model Paper 10
## Topic: Practical Full Stack Scenarios
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: User Registration Validator (5 Marks)
Write a function that validates user registration data.

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

## Question 2: Shopping Cart Total (5 Marks)
Write a function that calculates shopping cart total with discounts.

**Input:**
```
cart = [
    {"name": "Laptop", "price": 1000, "quantity": 1},
    {"name": "Mouse", "price": 50, "quantity": 2}
]
calculate_cart(cart, discount_percent=10)
```

**Output:**
```
{"subtotal": 1100, "discount": 110, "total": 990}
```

---

## Question 3: URL Shortener (5 Marks)
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

## Question 4: Rate Calculator (5 Marks)
Write a function that calculates average rating and rating distribution.

**Input:**
```
ratings = [5, 4, 5, 3, 4, 5, 5, 4, 2, 5]
calculate_ratings(ratings)
```

**Output:**
```
{"average": 4.2, "distribution": {5: 5, 4: 3, 3: 1, 2: 1, 1: 0}, "total": 10}
```

---

## Question 5: Token Generator (5 Marks)
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

## Question 6: Event Scheduler (5 Marks)
Write a class that manages scheduled events with time slots.

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

## Question 7: Config Parser (5 Marks)
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

## Question 8: Leaderboard Manager (5 Marks)
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

## Question 9: Form Validator (5 Marks)
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

## Question 10: API Rate Tracker (5 Marks)
Write a class that tracks API calls per user with limits.

**Input:**
```
tracker = RateTracker(limit=5, window_seconds=60)
tracker.can_proceed("user123")  # 1st call
tracker.can_proceed("user123")  # 2nd call
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
- Code correctness: 50%
- Practical implementation: 30%
- Code readability: 20%
