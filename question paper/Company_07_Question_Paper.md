# Python Coding Round - Company 7
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Safe Sum (5 Marks)
Write a function that converts mixed list items to integers and returns sum. Skip invalid entries.

**Input:**
```
["10", 20, "30", "abc", 40]
```

**Output:**
```
100
```

---

## Question 2: Circle with Property (5 Marks)
Create Circle class with radius property and auto-calculated area property.

**Input:**
```
circle = Circle(5)
circle.area
circle.radius = 10
circle.area
```

**Output:**
```
78.54
314.16
```

---

## Question 3: Write CSV (5 Marks)
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

## Question 4: HTTP Status Helper (5 Marks)
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

## Question 5: String Compression (5 Marks)
Write a function that compresses string by counting consecutive characters.

**Input:**
```
"aaabbbcccc"
"abcd"
```

**Output:**
```
"a3b3c4"
"abcd"  # Return original if compressed is not shorter
```

---

## Question 6: User Statistics (5 Marks)
Write a function that returns user stats: total count and users created today from database.

**Input:**
```
get_user_stats(cursor)
```

**Output:**
```
{"total_users": 10, "users_today": 3}
```

---

## Question 7: Build Absolute URLs (5 Marks)
Write a function that converts relative URLs to absolute URLs.

**Input:**
```
base_url = "https://example.com/page/"
relative_urls = ["/about", "contact", "../home"]
make_absolute(base_url, relative_urls)
```

**Output:**
```
["https://example.com/about", "https://example.com/page/contact", "https://example.com/home"]
```

---

## Question 8: Timer Decorator (5 Marks)
Write a decorator that measures and logs execution time.

**Input:**
```
@timer
def slow_function():
    time.sleep(1)
    return "Done"

slow_function()
```

**Output:**
```
"slow_function took 1.00 seconds"
"Done"
```

---

## Question 9: Deep Merge Dicts (5 Marks)
Write a function that deep merges two nested dictionaries.

**Input:**
```
dict1 = {"a": {"b": 1, "c": 2}}
dict2 = {"a": {"c": 3, "d": 4}}
deep_merge(dict1, dict2)
```

**Output:**
```
{"a": {"b": 1, "c": 3, "d": 4}}
```

---

## Question 10: Rate Calculator (5 Marks)
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

## Evaluation Criteria:
- Code correctness: 60%
- Code readability: 20%
- Edge case handling: 20%
