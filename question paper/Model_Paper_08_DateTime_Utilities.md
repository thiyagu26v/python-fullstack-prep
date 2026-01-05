# Python Coding Round - Model Paper 08
## Topic: Date, Time & Utility Functions
### Duration: 45 Minutes | Total Marks: 50 | Fresher Level - Full Stack Role

---

## Question 1: Date Formatting (5 Marks)
Write a function that formats date object into various string formats.

**Input:**
```
dt = datetime(2024, 1, 15, 14, 30, 0)
format_date(dt, "short")
format_date(dt, "long")
format_date(dt, "iso")
```

**Output:**
```
"01/15/2024"
"January 15, 2024"
"2024-01-15T14:30:00"
```

---

## Question 2: Parse Date String (5 Marks)
Write a function that parses date strings in multiple formats.

**Input:**
```
parse_date("2024-01-15")
parse_date("15/01/2024")
parse_date("January 15, 2024")
```

**Output:**
```
datetime(2024, 1, 15)  # Returns datetime objects
```

---

## Question 3: Calculate Age (5 Marks)
Write a function that calculates age from birth date.

**Input:**
```
calculate_age(date(1990, 5, 15))
```

**Output:**
```
33  # Or current age based on today
```

---

## Question 4: Timezone Conversion (5 Marks)
Write a function that converts time between timezones using offset hours.

**Input:**
```
utc_time = datetime(2024, 1, 15, 12, 0, 0)
convert_timezone(utc_time, from_offset=0, to_offset=5.5)  # UTC to IST
```

**Output:**
```
datetime(2024, 1, 15, 17, 30, 0)
```

---

## Question 5: Working Days (5 Marks)
Write a function that calculates working days between two dates (excluding weekends).

**Input:**
```
working_days(date(2024, 1, 1), date(2024, 1, 15))
```

**Output:**
```
10  # Excluding Saturdays and Sundays
```

---

## Question 6: Relative Time (5 Marks)
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

## Question 7: UUID Generator (5 Marks)
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

## Question 8: Retry Decorator (5 Marks)
Write a decorator that retries function on failure with configurable attempts.

**Input:**
```
@retry(max_attempts=3, delay=1)
def unstable_function():
    # May fail sometimes
    pass
```

**Output:**
```
# Retries up to 3 times with 1 second delay between attempts
```

---

## Question 9: Cache Decorator (5 Marks)
Write a caching decorator that stores function results.

**Input:**
```
@cache
def expensive_function(n):
    return n * n

expensive_function(5)  # Computes
expensive_function(5)  # Returns cached
```

**Output:**
```
25  # Both calls return 25, second is from cache
```

---

## Question 10: Timer Decorator (5 Marks)
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

## Evaluation Criteria:
- Code correctness: 50%
- Date/time handling: 30%
- Code readability: 20%
