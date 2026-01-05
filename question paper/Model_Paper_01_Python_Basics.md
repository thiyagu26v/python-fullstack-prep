# Python Coding Round - Model Paper 01
## Topic: Python Basics & Data Types
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

## Question 2: Remove Duplicates (5 Marks)
Write a function that removes duplicates from a list while maintaining the original order.

**Input:**
```
[1, 2, 2, 3, 4, 4, 5]
```

**Output:**
```
[1, 2, 3, 4, 5]
```

---

## Question 3: Merge Dictionaries (5 Marks)
Write a function that merges two dictionaries. If a key exists in both, add their values.

**Input:**
```
{'a': 1, 'b': 2}, {'b': 3, 'c': 4}
```

**Output:**
```
{'a': 1, 'b': 5, 'c': 4}
```

---

## Question 4: Filter Adults (5 Marks)
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

## Question 5: Compare Lists (5 Marks)
Write a function that returns common elements and elements that are in either list but not both.

**Input:**
```
[1, 2, 3, 4], [3, 4, 5, 6]
```

**Output:**
```
{"common": [3, 4], "different": [1, 2, 5, 6]}
```

---

## Question 6: Format User Info (5 Marks)
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

## Question 7: Safe Sum (5 Marks)
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

## Question 8: Flatten List (5 Marks)
Write a function that flattens a nested list (one level deep).

**Input:**
```
[[1, 2], [3, 4], [5, 6]]
```

**Output:**
```
[1, 2, 3, 4, 5, 6]
```

---

## Question 9: Even Squares (5 Marks)
Write a function that returns all even numbers from a list, squared.

**Input:**
```
n = [1, 2, 3, 4, 5, 6]
solution=[]
for i in n:
    if i % 2 ==0:
        solution.append(i*i)

return solution
    
        
```

**Output:**
```
[4, 16, 36]
```


---

## Question 10: Password Validator (5 Marks)
Write a function to validate password. Rules: min 8 chars, must contain digit, must contain uppercase.

**Input:**
```
"Hello123"
```

**Output:**
```
True
```

**Input:**
```
"hello123"
```

**Output:**
```
False
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Code readability & style: 20%
- Edge case handling: 20%
