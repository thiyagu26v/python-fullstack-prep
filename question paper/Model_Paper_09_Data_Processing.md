# Python Coding Round - Model Paper 09
## Topic: Data Processing & Collections
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Group by Key (5 Marks)
Write a function that groups list of dictionaries by a specified key.

**Input:**
```
data = [
    {"name": "John", "dept": "IT"},
    {"name": "Jane", "dept": "HR"},
    {"name": "Bob", "dept": "IT"}
]
group_by(data, "dept")
```

**Output:**
```
{"IT": [{"name": "John", "dept": "IT"}, {"name": "Bob", "dept": "IT"}], "HR": [{"name": "Jane", "dept": "HR"}]}
```

---

## Question 2: Sort by Multiple Keys (5 Marks)
Write a function that sorts list of dictionaries by multiple keys.

**Input:**
```
data = [
    {"name": "Bob", "age": 25},
    {"name": "Alice", "age": 25},
    {"name": "Charlie", "age": 30}
]
sort_by_keys(data, ["age", "name"])
```

**Output:**
```
[{"name": "Alice", "age": 25}, {"name": "Bob", "age": 25}, {"name": "Charlie", "age": 30}]
```

---

## Question 3: Find Frequency (5 Marks)
Write a function that returns the most frequent element in a list.

**Input:**
```
[1, 2, 2, 3, 3, 3, 4]
```

**Output:**
```
3  # Appeared 3 times
```

---

## Question 4: Chunk List (5 Marks)
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

## Question 5: Deep Merge Dicts (5 Marks)
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

## Question 6: Find Duplicates (5 Marks)
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

## Question 7: Two Sum (5 Marks)
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

## Question 8: Rotate List (5 Marks)
Write a function that rotates list by k positions.

**Input:**
```
rotate_list([1, 2, 3, 4, 5], 2)
```

**Output:**
```
[4, 5, 1, 2, 3]  # Rotated right by 2
```

---

## Question 9: Zip Dictionaries (5 Marks)
Write a function that combines two lists into dictionary.

**Input:**
```
keys = ["a", "b", "c"]
values = [1, 2, 3]
zip_to_dict(keys, values)
```

**Output:**
```
{"a": 1, "b": 2, "c": 3}
```

---

## Question 10: Difference of Lists (5 Marks)
Write a function that returns elements in first list but not in second.

**Input:**
```
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
difference(list1, list2)
```

**Output:**
```
[1, 2]
```

---

## Evaluation Criteria:
- Code correctness: 60%
- Efficiency: 20%
- Code readability: 20%
