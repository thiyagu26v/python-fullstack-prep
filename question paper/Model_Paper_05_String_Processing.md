# Python Coding Round - Model Paper 05
## Topic: String Processing & Regex
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Reverse Words (5 Marks)
Write a function that reverses the order of words in a string.

**Input:**
```
"Hello World Python"
```

**Output:**
```
"Python World Hello"
```

---

## Question 2: Title Case (5 Marks)
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

## Question 3: Find All Indices (5 Marks)
Write a function that finds all occurrences of substring and returns indices.

**Input:**
```
text = "abcabcabc"
substring = "abc"
```

**Output:**
```
[0, 3, 6]
```

---

## Question 4: Email Validator (5 Marks)
Write a function that validates email address using regex.

**Input:**
```
is_valid_email("user@example.com")
is_valid_email("user@.com")
```

**Output:**
```
True
False
```

---

## Question 5: Extract Phone Numbers (5 Marks)
Write a function that extracts all phone numbers from text.

**Input:**
```
"Call me at 123-456-7890 or (098) 765-4321"
```

**Output:**
```
["123-456-7890", "(098) 765-4321"]
```

---

## Question 6: Slug Generator (5 Marks)
Write a function that converts title to URL-friendly slug.

**Input:**
```
"Hello World! This is Python 3.0"
```

**Output:**
```
"hello-world-this-is-python-3-0"
```

---

## Question 7: Camel to Snake Case (5 Marks)
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

## Question 8: Template Renderer (5 Marks)
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

## Question 9: Extract Hashtags (5 Marks)
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

## Question 10: String Compression (5 Marks)
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

## Evaluation Criteria:
- Code correctness: 50%
- Regex usage: 30%
- Code readability: 20%
