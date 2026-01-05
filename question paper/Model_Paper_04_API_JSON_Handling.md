# Python Coding Round - Model Paper 04
## Topic: API & JSON Data Handling
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Extract JSON Fields (5 Marks)
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

## Question 2: Pretty Print JSON (5 Marks)
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

## Question 3: Flatten Nested JSON (5 Marks)
Write a function that flattens nested JSON to single-level dictionary.

**Input:**
```
{"user": {"name": "John", "address": {"city": "NYC"}}}
```

**Output:**
```
{"user.name": "John", "user.address.city": "NYC"}
```

---

## Question 4: API Response Builder (5 Marks)
Write a function that creates standardized API response format.

**Input:**
```
create_response(True, {"user_id": 123}, "User created")
create_response(False, None, None, "User not found")
```

**Output:**
```
{"success": True, "data": {"user_id": 123}, "message": "User created", "error": None}
{"success": False, "data": None, "message": None, "error": "User not found"}
```

---

## Question 5: Validate Request (5 Marks)
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

## Question 6: Parse Query String (5 Marks)
Write a function that parses URL query string into dictionary.

**Input:**
```
"name=John&age=25&city=NYC"
```

**Output:**
```
{"name": "John", "age": "25", "city": "NYC"}
```

---

## Question 7: Transform Users (5 Marks)
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

## Question 8: Paginate Items (5 Marks)
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

## Question 9: Filter JSON Array (5 Marks)
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

## Question 10: HTTP Status Helper (5 Marks)
Create a class with static methods for common HTTP status responses.

**Input:**
```
HttpStatus.ok({"message": "Success"})
HttpStatus.not_found("User not found")
```

**Output:**
```
{"status": 200, "status_text": "OK", "body": {"message": "Success"}}
{"status": 404, "status_text": "Not Found", "body": "User not found"}
```

---

## Evaluation Criteria:
- Code correctness: 50%
- JSON handling: 30%
- Code readability: 20%
