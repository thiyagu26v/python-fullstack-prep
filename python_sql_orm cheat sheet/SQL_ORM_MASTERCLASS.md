---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# 🎓 SQL & Django ORM Masterclass
### From Zero to Pro - Complete Study Guide

> **Target Audience**: Complete beginners who want to master SQL/PostgreSQL and Django ORM
> **Goal**: After completing this guide, you'll be interview-ready and confident in database operations

---

# 📚 Table of Contents

1. [🎯 Introduction & Setup](#-introduction--setup)
2. [📗 LEVEL 1: BEGINNER](#-level-1-beginner-foundation)
3. [📘 LEVEL 2: INTERMEDIATE](#-level-2-intermediate-building-skills)
4. [📕 LEVEL 3: ADVANCED](#-level-3-advanced-mastery)
5. [🐘 PostgreSQL-Specific Features](#-postgresql-specific-features)
6. [🎤 Interview Questions & Answers](#-interview-questions--answers)
7. [📋 Quick Reference Cheat Sheet](#-quick-reference-cheat-sheet)
8. [🏋️ Practice Exercises](#-practice-exercises)

---

# 🎯 Introduction & Setup

## What is a Database?

### 🎯 Simple Explanation
A **database** is like a super-organized digital filing cabinet that stores information in a structured way so you can easily find, add, update, or delete data.

### 💡 Real-World Analogy
Think of a **library**:
- The **library building** = Database
- **Bookshelves** = Tables
- **Books** = Rows (Records)
- **Book properties** (title, author, ISBN) = Columns (Fields)

### 📊 Visual Representation
```
┌─────────────────────────────────────────────────────────┐
│                    DATABASE (Library)                    │
├─────────────────────────────────────────────────────────┤
│  ┌─────────────────────┐  ┌─────────────────────┐      │
│  │   TABLE: Users      │  │   TABLE: Products   │      │
│  ├─────────────────────┤  ├─────────────────────┤      │
│  │ id │ name  │ email  │  │ id │ name  │ price │      │
│  │ 1  │ John  │ j@mail │  │ 1  │ Phone │ 999   │      │
│  │ 2  │ Jane  │ jane@  │  │ 2  │ Laptop│ 1500  │      │
│  └─────────────────────┘  └─────────────────────┘      │
└─────────────────────────────────────────────────────────┘
```

---

## DBMS vs RDBMS

| Feature | DBMS | RDBMS |
|---------|------|-------|
| **Full Form** | Database Management System | Relational Database Management System |
| **Data Storage** | Files (hierarchical/network) | Tables with rows & columns |
| **Relationships** | No relationships between data | Supports relationships (Foreign Keys) |
| **Data Integrity** | Limited | Strong (ACID properties) |
| **Examples** | File systems, XML | PostgreSQL, MySQL, SQLite |
| **Normalization** | Not supported | Fully supported |

### 💡 Key Insight
> **RDBMS** is a type of DBMS that organizes data into **related tables**. All modern databases (PostgreSQL, MySQL, SQLite) are RDBMS.

---

## What is SQL?

### 🎯 Definition
**SQL** (Structured Query Language) is the standard language for communicating with databases. It lets you:
- **CREATE** structures (tables, indexes)
- **READ** data (SELECT queries)
- **UPDATE** existing data
- **DELETE** data

### 📊 SQL Command Categories
```
┌──────────────────────────────────────────────────────────────┐
│                    SQL COMMAND TYPES                          │
├──────────────────────────────────────────────────────────────┤
│  DDL (Data Definition)  │  CREATE, ALTER, DROP, TRUNCATE     │
│  DML (Data Manipulation)│  SELECT, INSERT, UPDATE, DELETE    │
│  DCL (Data Control)     │  GRANT, REVOKE                     │
│  TCL (Transaction)      │  COMMIT, ROLLBACK, SAVEPOINT       │
└──────────────────────────────────────────────────────────────┘
```

---

## What is an ORM?

### 🎯 Definition
**ORM** (Object-Relational Mapping) is a technique that lets you interact with your database using your programming language (Python) instead of writing raw SQL.

### 💡 Why Use ORM?
| Without ORM (Raw SQL) | With ORM (Django) |
|-----------------------|-------------------|
| Write SQL strings in Python | Write Python code |
| Prone to SQL injection | Automatically escaped |
| Database-specific syntax | Database-agnostic |
| Manual connection handling | Automatic management |

### 📊 Visual Comparison
```python
# ❌ WITHOUT ORM (Raw SQL)
cursor.execute("SELECT * FROM users WHERE age > 18")

# ✅ WITH ORM (Django)
User.objects.filter(age__gt=18)
```

---

## Setup: Our Sample Database

For all examples, we'll use this Django model structure:

```python
# models.py - Our practice models

from django.db import models

class Author(models.Model):
    """Represents a book author"""
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    birth_date = models.DateField(null=True, blank=True)
    country = models.CharField(max_length=50, default='Unknown')
    
    def __str__(self):
        return self.name

class Category(models.Model):
    """Book categories/genres"""
    name = models.CharField(max_length=50)
    description = models.TextField(blank=True)
    
    def __str__(self):
        return self.name

class Book(models.Model):
    """Represents a book in the store"""
    title = models.CharField(max_length=200)
    author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')
    category = models.ForeignKey(Category, on_delete=models.SET_NULL, null=True)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField(default=0)
    published_date = models.DateField()
    is_available = models.BooleanField(default=True)
    rating = models.FloatField(default=0.0)
    
    def __str__(self):
        return self.title

class Order(models.Model):
    """Customer orders"""
    customer_name = models.CharField(max_length=100)
    book = models.ForeignKey(Book, on_delete=models.CASCADE)
    quantity = models.IntegerField(default=1)
    order_date = models.DateTimeField(auto_now_add=True)
    total_price = models.DecimalField(max_digits=10, decimal_places=2)
    
    def __str__(self):
        return f"{self.customer_name} - {self.book.title}"
```

### 📊 Equivalent SQL Tables
```sql
-- Authors table
CREATE TABLE author (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(254) UNIQUE NOT NULL,
    birth_date DATE,
    country VARCHAR(50) DEFAULT 'Unknown'
);

-- Categories table
CREATE TABLE category (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    description TEXT
);

-- Books table
CREATE TABLE book (
    id SERIAL PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    author_id INTEGER REFERENCES author(id) ON DELETE CASCADE,
    category_id INTEGER REFERENCES category(id) ON DELETE SET NULL,
    price DECIMAL(10, 2) NOT NULL,
    stock INTEGER DEFAULT 0,
    published_date DATE NOT NULL,
    is_available BOOLEAN DEFAULT TRUE,
    rating FLOAT DEFAULT 0.0
);

-- Orders table
CREATE TABLE "order" (
    id SERIAL PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    book_id INTEGER REFERENCES book(id) ON DELETE CASCADE,
    quantity INTEGER DEFAULT 1,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_price DECIMAL(10, 2) NOT NULL
);
```

---

# 📗 LEVEL 1: BEGINNER (Foundation)

## 1.1 Retrieving All Data (SELECT *)

### 🎯 What is it?
Fetches **all rows and all columns** from a table.

### 💡 When to use?
- When you need to see everything in a table
- During development/debugging
- **⚠️ Avoid in production** for large tables (performance issues)

### 🔧 SQL Syntax
```sql
-- Get all books
SELECT * FROM book;

-- Get all authors
SELECT * FROM author;
```

### � Sample Output
```
┌────┬───────────────────┬───────────┬─────────┬───────┬────────────────┬──────────────┬────────┐
│ id │ title             │ author_id │ price   │ stock │ published_date │ is_available │ rating │
├────┼───────────────────┼───────────┼─────────┼───────┼────────────────┼──────────────┼────────┤
│ 1  │ Python Mastery    │ 1         │ 49.99   │ 25    │ 2023-01-15     │ TRUE         │ 4.5    │
│ 2  │ Django Deep Dive  │ 1         │ 59.99   │ 18    │ 2023-06-20     │ TRUE         │ 4.8    │
│ 3  │ SQL Fundamentals  │ 2         │ 34.99   │ 42    │ 2022-11-10     │ TRUE         │ 4.2    │
│ 4  │ Web Development   │ 3         │ 79.99   │ 0     │ 2024-02-28     │ FALSE        │ 4.6    │
│ 5  │ Data Science 101  │ 2         │ 44.99   │ 31    │ 2023-09-05     │ TRUE         │ 4.0    │
└────┴───────────────────┴───────────┴─────────┴───────┴────────────────┴──────────────┴────────┘
(5 rows)
```

### �🐍 Django ORM Equivalent
```python
# Get all books
books = Book.objects.all()

# Get all authors  
authors = Author.objects.all()

# Note: This returns a QuerySet (lazy evaluation)
# Data is NOT fetched until you iterate or evaluate
```

### 📊 Side-by-Side Comparison
| SQL | Django ORM |
|-----|------------|
| `SELECT * FROM book;` | `Book.objects.all()` |
| `SELECT * FROM author;` | `Author.objects.all()` |

### 🎓 Pro Tips
1. **Lazy Evaluation**: Django QuerySets don't hit the database until needed
2. **Avoid SELECT ***: In production, select only needed columns

---


## 1.2 Selecting Specific Columns

### 🎯 What is it?
Fetches only the **columns you need** instead of everything.

### 💡 Why use it?
- **Performance**: Less data transferred
- **Security**: Don't expose sensitive columns
- **Clarity**: Get only what you need

### 🔧 SQL Syntax
```sql
-- Get only title and price of books
SELECT title, price FROM book;

-- Get author name and email
SELECT name, email FROM author;
```

### � Sample Output
```
┌───────────────────┬─────────┐
│ title             │ price   │
├───────────────────┼─────────┤
│ Python Mastery    │ 49.99   │
│ Django Deep Dive  │ 59.99   │
│ SQL Fundamentals  │ 34.99   │
│ Web Development   │ 79.99   │
│ Data Science 101  │ 44.99   │
└───────────────────┴─────────┘
(5 rows)
```

### �🐍 Django ORM Equivalent
```python
# Method 1: values() - Returns dictionaries
books = Book.objects.values('title', 'price')
# Result: <QuerySet [{'title': 'Book1', 'price': 29.99}, ...]>

# Method 2: values_list() - Returns tuples
books = Book.objects.values_list('title', 'price')
# Result: <QuerySet [('Book1', 29.99), ...]>

# Method 3: values_list with flat=True (single column only)
titles = Book.objects.values_list('title', flat=True)
# Result: <QuerySet ['Book1', 'Book2', ...]>
```

### 📊 ORM Output Example
```python
# values() output:
[
    {'title': 'Python Mastery', 'price': Decimal('49.99')},
    {'title': 'Django Deep Dive', 'price': Decimal('59.99')},
    {'title': 'SQL Fundamentals', 'price': Decimal('34.99')},
    ...
]

# values_list() output:
[
    ('Python Mastery', Decimal('49.99')),
    ('Django Deep Dive', Decimal('59.99')),
    ...
]

# values_list(flat=True) output:
['Python Mastery', 'Django Deep Dive', 'SQL Fundamentals', ...]
```

### 📊 Side-by-Side Comparison
| SQL | Django ORM | Returns |
|-----|------------|---------|
| `SELECT title, price FROM book;` | `.values('title', 'price')` | List of dicts |
| `SELECT title, price FROM book;` | `.values_list('title', 'price')` | List of tuples |
| `SELECT title FROM book;` | `.values_list('title', flat=True)` | Flat list |

### 🎓 Pro Tips
1. **values()** is great for JSON APIs
2. **values_list()** is faster for processing
3. Use **only()** and **defer()** for model instances with fewer fields

---


## 1.3 Filtering Data (WHERE Clause)

### 🎯 What is it?
Filters rows based on **conditions**. Only matching rows are returned.

### 💡 Real-World Use Cases
- Find users from a specific country
- Get products under a certain price
- Search for orders from today

### 🔧 SQL Syntax
```sql
-- Books cheaper than $50
SELECT * FROM book WHERE price < 50;

-- Books by a specific author (author_id = 1)
SELECT * FROM book WHERE author_id = 1;

-- Available books only
SELECT * FROM book WHERE is_available = TRUE;
```

### � Sample Output (WHERE price < 50)
```
┌────┬───────────────────┬───────────┬─────────┬───────┬────────────────┬──────────────┬────────┐
│ id │ title             │ author_id │ price   │ stock │ published_date │ is_available │ rating │
├────┼───────────────────┼───────────┼─────────┼───────┼────────────────┼──────────────┼────────┤
│ 1  │ Python Mastery    │ 1         │ 49.99   │ 25    │ 2023-01-15     │ TRUE         │ 4.5    │
│ 3  │ SQL Fundamentals  │ 2         │ 34.99   │ 42    │ 2022-11-10     │ TRUE         │ 4.2    │
│ 5  │ Data Science 101  │ 2         │ 44.99   │ 31    │ 2023-09-05     │ TRUE         │ 4.0    │
└────┴───────────────────┴───────────┴─────────┴───────┴────────────────┴──────────────┴────────┘
(3 rows) -- Only books with price < 50 are returned
```

### �🐍 Django ORM Equivalent
```python
# Books cheaper than $50
cheap_books = Book.objects.filter(price__lt=50)

# Books by a specific author
author_books = Book.objects.filter(author_id=1)
# OR using the relationship
author_books = Book.objects.filter(author__id=1)

# Available books only
available = Book.objects.filter(is_available=True)
```

### 📊 ORM Output Example
```python
# Book.objects.filter(price__lt=50)
<QuerySet [
    <Book: Python Mastery>,
    <Book: SQL Fundamentals>,
    <Book: Data Science 101>
]>
```

### 📊 Complete Lookup Reference
| SQL Operator | Django Lookup | Example |
|--------------|---------------|---------|
| `=` | `field=value` | `filter(price=50)` |
| `<` | `__lt` | `filter(price__lt=50)` |
| `>` | `__gt` | `filter(price__gt=50)` |
| `<=` | `__lte` | `filter(price__lte=50)` |
| `>=` | `__gte` | `filter(price__gte=50)` |
| `<>` or `!=` | `exclude()` | `exclude(price=50)` |
| `BETWEEN` | `__range` | `filter(price__range=(10, 50))` |
| `IS NULL` | `__isnull` | `filter(author__isnull=True)` |

### 🎓 Pro Tips
1. **filter()** returns a QuerySet (chainable)
2. **get()** returns a single object (raises error if not found)
3. Use **exclude()** for "NOT" conditions

---


## 1.4 Multiple Conditions (AND / OR)

### 🎯 What is it?
Combine multiple conditions using **AND** or **OR** logic.

### 🔧 SQL Syntax
```sql
-- AND: Both conditions must be true
SELECT * FROM book 
WHERE price < 50 AND is_available = TRUE;

-- OR: Either condition can be true
SELECT * FROM book 
WHERE price < 20 OR stock > 100;

-- Complex: Combining AND and OR
SELECT * FROM book 
WHERE (price < 50 AND is_available = TRUE) OR stock > 100;
```

### 🐍 Django ORM Equivalent
```python
from django.db.models import Q

# AND: Chain filter() or use multiple arguments
books = Book.objects.filter(price__lt=50, is_available=True)
# OR
books = Book.objects.filter(price__lt=50).filter(is_available=True)

# OR: Use Q objects
books = Book.objects.filter(Q(price__lt=20) | Q(stock__gt=100))

# Complex: Combining AND and OR with Q objects
books = Book.objects.filter(
    (Q(price__lt=50) & Q(is_available=True)) | Q(stock__gt=100)
)

# NOT: Use ~ with Q objects
books = Book.objects.filter(~Q(price__lt=50))  # price >= 50
```

### 📊 Q Objects Reference
| SQL | Django Q Object |
|-----|-----------------|
| `AND` | `Q(...) & Q(...)` |
| `OR` | `Q(...) \| Q(...)` |
| `NOT` | `~Q(...)` |

### 🎓 Pro Tips
1. **Chaining filter()** is AND
2. **Q objects** are needed for OR logic
3. Use parentheses for complex conditions

---

## 1.5 Text Pattern Matching (LIKE)

### 🎯 What is it?
Search for patterns in text fields using wildcards.

### 💡 SQL Wildcards
- `%` = Any number of characters (including zero)
- `_` = Exactly one character

### 🔧 SQL Syntax
```sql
-- Titles starting with "The"
SELECT * FROM book WHERE title LIKE 'The%';

-- Titles ending with "Story"
SELECT * FROM book WHERE title LIKE '%Story';

-- Titles containing "Python"
SELECT * FROM book WHERE title LIKE '%Python%';

-- Case-insensitive (PostgreSQL)
SELECT * FROM book WHERE title ILIKE '%python%';
```

### 🐍 Django ORM Equivalent
```python
# Starts with "The" (case-sensitive)
books = Book.objects.filter(title__startswith='The')

# Starts with "the" (case-insensitive)
books = Book.objects.filter(title__istartswith='the')

# Ends with "Story"
books = Book.objects.filter(title__endswith='Story')

# Contains "Python" (case-sensitive)
books = Book.objects.filter(title__contains='Python')

# Contains "python" (case-insensitive) - MOST COMMON
books = Book.objects.filter(title__icontains='python')

# Exact match
books = Book.objects.filter(title__exact='The Great Gatsby')
books = Book.objects.filter(title__iexact='the great gatsby')  # case-insensitive
```

### 📊 Complete Text Lookups
| SQL LIKE | Django Lookup | Case-Insensitive |
|----------|---------------|------------------|
| `LIKE 'abc%'` | `__startswith='abc'` | `__istartswith` |
| `LIKE '%abc'` | `__endswith='abc'` | `__iendswith` |
| `LIKE '%abc%'` | `__contains='abc'` | `__icontains` |
| `= 'abc'` | `__exact='abc'` | `__iexact` |
| `~ 'pattern'` | `__regex='pattern'` | `__iregex` |

---

## 1.6 Matching Multiple Values (IN Clause)

### 🎯 What is it?
Check if a value matches **any value in a list**.

### 🔧 SQL Syntax
```sql
-- Books with specific IDs
SELECT * FROM book WHERE id IN (1, 3, 5, 7);

-- Books in specific categories
SELECT * FROM book WHERE category_id IN (1, 2);

-- NOT IN
SELECT * FROM book WHERE id NOT IN (1, 3, 5);
```

### 🐍 Django ORM Equivalent
```python
# Books with specific IDs
books = Book.objects.filter(id__in=[1, 3, 5, 7])

# Books in specific categories
books = Book.objects.filter(category_id__in=[1, 2])

# NOT IN using exclude()
books = Book.objects.exclude(id__in=[1, 3, 5])

# Using a QuerySet as the IN list (subquery)
cheap_book_ids = Book.objects.filter(price__lt=20).values_list('id', flat=True)
cheap_books = Book.objects.filter(id__in=cheap_book_ids)
```

### 🎓 Pro Tips
1. **__in** can accept lists, tuples, or QuerySets
2. Using a QuerySet creates a **subquery** automatically
3. For large lists, consider chunking to avoid performance issues

---

## 1.7 Sorting Results (ORDER BY)

### 🎯 What is it?
Arrange results in a specific order (ascending or descending).

### 🔧 SQL Syntax
```sql
-- Sort by price (ascending - default)
SELECT * FROM book ORDER BY price;
SELECT * FROM book ORDER BY price ASC;

-- Sort by price (descending)
SELECT * FROM book ORDER BY price DESC;

-- Multiple columns
SELECT * FROM book ORDER BY category_id, price DESC;

-- Random order
SELECT * FROM book ORDER BY RANDOM();
```

### 🐍 Django ORM Equivalent
```python
# Ascending (default)
books = Book.objects.order_by('price')

# Descending (use minus sign)
books = Book.objects.order_by('-price')

# Multiple columns
books = Book.objects.order_by('category_id', '-price')

# Random order
books = Book.objects.order_by('?')

# Clear default ordering
books = Book.objects.order_by()  # No ordering

# Ordering by related field
books = Book.objects.order_by('author__name')
```

### 📊 Side-by-Side
| SQL | Django ORM |
|-----|------------|
| `ORDER BY price` | `.order_by('price')` |
| `ORDER BY price DESC` | `.order_by('-price')` |
| `ORDER BY RANDOM()` | `.order_by('?')` |

---

## 1.8 Limiting Results (LIMIT & OFFSET)

### 🎯 What is it?
Control **how many rows** to return and **where to start**.

### 💡 Use Cases
- Pagination (10 items per page)
- Get "Top 5" results
- Skip first N records

### 🔧 SQL Syntax
```sql
-- First 10 books
SELECT * FROM book LIMIT 10;

-- 10 books, starting from 21st (skip first 20)
SELECT * FROM book LIMIT 10 OFFSET 20;

-- PostgreSQL specific: LIMIT ALL (no limit)
SELECT * FROM book LIMIT ALL;
```

### 🐍 Django ORM Equivalent
```python
# First 10 books (Python slicing!)
books = Book.objects.all()[:10]

# 10 books, starting from 21st (pagination)
books = Book.objects.all()[20:30]

# Get single item at position
fifth_book = Book.objects.all()[4]  # 0-indexed, so 4 = 5th item

# Combined with ordering (Top 5 most expensive)
top_expensive = Book.objects.order_by('-price')[:5]

# First item
first_book = Book.objects.first()
last_book = Book.objects.last()
```

### 📊 Pagination Example
```python
# Page 1 (items 0-9)
page_1 = Book.objects.all()[0:10]

# Page 2 (items 10-19)
page_2 = Book.objects.all()[10:20]

# Page 3 (items 20-29)
page_3 = Book.objects.all()[20:30]

# Generic formula: page N with size S
# Book.objects.all()[(N-1)*S : N*S]
```

### 🎓 Pro Tips
1. **Slicing is efficient** - Django adds LIMIT/OFFSET to SQL
2. **Negative indexing not supported** (`[-1]` won't work)
3. Use `first()` and `last()` for single items

---

## 1.9 Creating Data (INSERT)

### 🎯 What is it?
Add new rows to a table.

### 🔧 SQL Syntax
```sql
-- Insert single row
INSERT INTO author (name, email, country) 
VALUES ('John Doe', 'john@example.com', 'USA');

-- Insert multiple rows
INSERT INTO author (name, email, country) VALUES 
    ('Jane Smith', 'jane@example.com', 'UK'),
    ('Bob Wilson', 'bob@example.com', 'Canada');

-- Insert and return the created row (PostgreSQL)
INSERT INTO author (name, email) 
VALUES ('Alice', 'alice@example.com') 
RETURNING *;
```

### 🐍 Django ORM Equivalent
```python
# Method 1: create() - Creates and saves in one step
author = Author.objects.create(
    name='John Doe',
    email='john@example.com',
    country='USA'
)

# Method 2: Instantiate then save()
author = Author(name='Jane Smith', email='jane@example.com')
author.country = 'UK'  # Can modify before saving
author.save()

# Method 3: Bulk create (efficient for multiple objects)
authors = Author.objects.bulk_create([
    Author(name='Alice', email='alice@example.com'),
    Author(name='Bob', email='bob@example.com'),
    Author(name='Charlie', email='charlie@example.com'),
])

# Method 4: get_or_create() - Avoid duplicates
author, created = Author.objects.get_or_create(
    email='john@example.com',
    defaults={'name': 'John Doe', 'country': 'USA'}
)
# created = True if new, False if existed
```

### 📊 Comparison
| SQL | Django ORM | Notes |
|-----|------------|-------|
| `INSERT INTO` | `.create()` | Single row, returns object |
| `INSERT INTO ... VALUES` | `.bulk_create()` | Multiple rows, efficient |
| N/A | `.get_or_create()` | Create if doesn't exist |
| N/A | `.update_or_create()` | Create or update |

---

## 1.10 Updating Data (UPDATE)

### 🎯 What is it?
Modify existing rows in a table.

### 🔧 SQL Syntax
```sql
-- Update single column
UPDATE book SET price = 29.99 WHERE id = 1;

-- Update multiple columns
UPDATE book SET price = 29.99, stock = 50 WHERE id = 1;

-- Update multiple rows
UPDATE book SET is_available = FALSE WHERE stock = 0;

-- Update all rows (DANGEROUS!)
UPDATE book SET rating = 0;
```

### 🐍 Django ORM Equivalent
```python
# Method 1: Update single object (fetches first, then saves)
book = Book.objects.get(id=1)
book.price = 29.99
book.save()

# Method 2: update() on QuerySet (direct database update - FASTER)
Book.objects.filter(id=1).update(price=29.99)

# Update multiple columns
Book.objects.filter(id=1).update(price=29.99, stock=50)

# Update multiple rows
Book.objects.filter(stock=0).update(is_available=False)

# Update all rows (DANGEROUS!)
Book.objects.all().update(rating=0)

# Update with F() expression (database-level calculation)
from django.db.models import F
Book.objects.filter(id=1).update(stock=F('stock') - 1)  # Decrement stock
Book.objects.all().update(price=F('price') * 1.1)  # 10% price increase
```

### 📊 save() vs update()
| Method | Use Case | Pros | Cons |
|--------|----------|------|------|
| `.save()` | Single object | Runs model validations, signals | 2 queries (SELECT + UPDATE) |
| `.update()` | Multiple objects | Single query, efficient | No validations, no signals |

### 🎓 Pro Tips
1. **update()** is faster but skips model validations
2. Use **F()** for database-level calculations (avoids race conditions)
3. **Always use filter()** before update() to avoid updating all rows

---

## 1.11 Deleting Data (DELETE)

### 🎯 What is it?
Remove rows from a table.

### 🔧 SQL Syntax
```sql
-- Delete specific row
DELETE FROM book WHERE id = 1;

-- Delete multiple rows
DELETE FROM book WHERE stock = 0;

-- Delete all rows (DANGEROUS!)
DELETE FROM book;

-- Delete with condition on related table
DELETE FROM book WHERE author_id IN (
    SELECT id FROM author WHERE country = 'Unknown'
);
```

### 🐍 Django ORM Equivalent
```python
# Method 1: Delete single object
book = Book.objects.get(id=1)
book.delete()

# Method 2: Delete using QuerySet (more efficient)
Book.objects.filter(id=1).delete()

# Delete multiple rows
deleted_count, details = Book.objects.filter(stock=0).delete()
# deleted_count = number of deleted objects
# details = {'app.Book': 5, 'app.Order': 10} breakdown by model

# Delete all rows (DANGEROUS!)
Book.objects.all().delete()

# Delete with condition on related table
Book.objects.filter(author__country='Unknown').delete()
```

### ⚠️ CASCADE Behavior
```python
# When you delete an Author, what happens to their Books?
# Depends on on_delete setting in ForeignKey

class Book(models.Model):
    # CASCADE: Delete books when author is deleted
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    
    # PROTECT: Prevent deletion if books exist
    author = models.ForeignKey(Author, on_delete=models.PROTECT)
    
    # SET_NULL: Set author to NULL when deleted
    author = models.ForeignKey(Author, on_delete=models.SET_NULL, null=True)
    
    # SET_DEFAULT: Set to default value
    author = models.ForeignKey(Author, on_delete=models.SET_DEFAULT, default=1)
```

### 🎓 Pro Tips
1. **delete()** on QuerySet is efficient (single query)
2. **CASCADE** can delete related objects automatically
3. Always **test delete operations** in development first!

---

## 1.12 Getting Single Objects

### 🎯 What is it?
Retrieve exactly **one** row from the database.

### 🔧 SQL Syntax
```sql
-- Get specific book (assumes only one result)
SELECT * FROM book WHERE id = 1;

-- Get first result
SELECT * FROM book ORDER BY id LIMIT 1;
```

### 🐍 Django ORM Equivalent
```python
# get() - Returns single object, raises error if not found or multiple
try:
    book = Book.objects.get(id=1)
except Book.DoesNotExist:
    print("Book not found")
except Book.MultipleObjectsReturned:
    print("Multiple books found")

# first() - Returns first object or None
book = Book.objects.filter(price__lt=50).first()

# last() - Returns last object or None
book = Book.objects.order_by('id').last()

# get_or_create() - Get or create if doesn't exist
book, created = Book.objects.get_or_create(
    title='New Book',
    defaults={'price': 19.99, 'author_id': 1}
)

# filter()[0] - Like first() but raises IndexError
book = Book.objects.filter(price__lt=50)[0]
```

### 📊 Comparison
| Method | Returns | If Not Found | If Multiple |
|--------|---------|--------------|-------------|
| `get()` | Object | DoesNotExist | MultipleObjectsReturned |
| `first()` | Object or None | None | First one |
| `last()` | Object or None | None | Last one |
| `[0]` | Object | IndexError | First one |

---

## 1.13 Counting Results

### 🎯 What is it?
Get the **number of rows** matching your query.

### 🔧 SQL Syntax
```sql
-- Count all books
SELECT COUNT(*) FROM book;

-- Count with condition
SELECT COUNT(*) FROM book WHERE is_available = TRUE;

-- Count distinct values
SELECT COUNT(DISTINCT category_id) FROM book;
```

### 🐍 Django ORM Equivalent
```python
# Count all books
total = Book.objects.count()

# Count with condition
available = Book.objects.filter(is_available=True).count()

# Count distinct values
from django.db.models import Count
categories = Book.objects.values('category_id').distinct().count()

# exists() - More efficient than count() > 0
if Book.objects.filter(stock=0).exists():
    print("Some books are out of stock")
```

### 🎓 Pro Tips
1. **count()** is translated to `SELECT COUNT(*)`
2. Use **exists()** instead of `count() > 0` (stops at first match)
3. **len(queryset)** fetches all objects first - avoid for counting!

---

# 📘 LEVEL 2: INTERMEDIATE (Building Skills)

## 2.1 Aggregation Functions

### 🎯 What is it?
Perform **calculations on groups of rows** and return a single value (SUM, AVG, MIN, MAX, COUNT).

### 💡 Real-World Use Cases
- Calculate total revenue
- Find average product rating
- Get highest/lowest prices
- Count orders per customer

### 🔧 SQL Syntax
```sql
-- Sum of all book prices
SELECT SUM(price) FROM book;

-- Average rating
SELECT AVG(rating) FROM book;

-- Minimum and Maximum price
SELECT MIN(price), MAX(price) FROM book;

-- Multiple aggregations
SELECT 
    COUNT(*) as total_books,
    SUM(stock) as total_stock,
    AVG(price) as avg_price,
    MIN(price) as cheapest,
    MAX(price) as most_expensive
FROM book;
```

### 🐍 Django ORM Equivalent
```python
from django.db.models import Sum, Avg, Min, Max, Count

# Sum of all book prices
total = Book.objects.aggregate(Sum('price'))
# Result: {'price__sum': Decimal('1234.56')}

# Average rating
avg = Book.objects.aggregate(Avg('rating'))
# Result: {'rating__avg': 4.25}

# Min and Max
extremes = Book.objects.aggregate(Min('price'), Max('price'))
# Result: {'price__min': 9.99, 'price__max': 199.99}

# Multiple aggregations with custom names
stats = Book.objects.aggregate(
    total_books=Count('id'),
    total_stock=Sum('stock'),
    avg_price=Avg('price'),
    cheapest=Min('price'),
    most_expensive=Max('price')
)

# Aggregate with filter
cheap_avg = Book.objects.filter(price__lt=50).aggregate(Avg('price'))
```

### 📊 Aggregation Functions Reference
| SQL | Django | Description |
|-----|--------|-------------|
| `COUNT(*)` | `Count('id')` | Count rows |
| `SUM(column)` | `Sum('field')` | Sum of values |
| `AVG(column)` | `Avg('field')` | Average value |
| `MIN(column)` | `Min('field')` | Minimum value |
| `MAX(column)` | `Max('field')` | Maximum value |

### 🎓 Pro Tips
1. **aggregate()** returns a dictionary, not a QuerySet
2. Use **output_field** for type hints: `Sum('price', output_field=FloatField())`
3. Combine with **filter()** to aggregate subsets

---

## 2.2 GROUP BY (Grouping Data)

### 🎯 What is it?
**Group rows** that have the same values and apply aggregate functions to each group.

### 💡 Real-World Use Cases
- Sales per category
- Books per author
- Orders per day
- Revenue per region

### 🔧 SQL Syntax
```sql
-- Count books per category
SELECT category_id, COUNT(*) as book_count
FROM book
GROUP BY category_id;

-- Total stock per author
SELECT author_id, SUM(stock) as total_stock
FROM book
GROUP BY author_id;

-- Multiple aggregations per group
SELECT 
    author_id,
    COUNT(*) as num_books,
    AVG(price) as avg_price,
    SUM(stock) as total_stock
FROM book
GROUP BY author_id;
```

### 🐍 Django ORM Equivalent
```python
from django.db.models import Count, Sum, Avg

# Count books per category
category_counts = Book.objects.values('category_id').annotate(
    book_count=Count('id')
)
# Result: <QuerySet [{'category_id': 1, 'book_count': 5}, ...]>

# Total stock per author
author_stock = Book.objects.values('author_id').annotate(
    total_stock=Sum('stock')
)

# Multiple aggregations per group
author_stats = Book.objects.values('author_id').annotate(
    num_books=Count('id'),
    avg_price=Avg('price'),
    total_stock=Sum('stock')
)

# With related field names (better output)
author_stats = Book.objects.values('author__name').annotate(
    num_books=Count('id'),
    avg_price=Avg('price')
)
# Result: <QuerySet [{'author__name': 'John', 'num_books': 3, 'avg_price': 29.99}, ...]>

# Order groups by aggregation
top_authors = Book.objects.values('author__name').annotate(
    num_books=Count('id')
).order_by('-num_books')[:5]
```

### 📊 Pattern: values() + annotate() = GROUP BY
```
SQL:     GROUP BY column    + aggregate functions
Django:  values('field')    + annotate(aggregations)
```

### 🎓 Pro Tips
1. **values()** before **annotate()** = GROUP BY
2. **annotate()** without **values()** = add field to each object
3. You can order by the annotated field

---

## 2.3 HAVING (Filter Groups)

### 🎯 What is it?
Filter **groups** (after GROUP BY) based on aggregate conditions.

### 💡 WHERE vs HAVING
- **WHERE**: Filters individual rows BEFORE grouping
- **HAVING**: Filters groups AFTER aggregation

### 🔧 SQL Syntax
```sql
-- Categories with more than 5 books
SELECT category_id, COUNT(*) as book_count
FROM book
GROUP BY category_id
HAVING COUNT(*) > 5;

-- Authors with average book price > $30
SELECT author_id, AVG(price) as avg_price
FROM book
GROUP BY author_id
HAVING AVG(price) > 30;

-- Combining WHERE and HAVING
SELECT author_id, COUNT(*) as available_books
FROM book
WHERE is_available = TRUE       -- Filter rows first
GROUP BY author_id
HAVING COUNT(*) > 2;            -- Then filter groups
```

### 🐍 Django ORM Equivalent
```python
from django.db.models import Count, Avg

# Categories with more than 5 books
popular_categories = Book.objects.values('category_id').annotate(
    book_count=Count('id')
).filter(book_count__gt=5)  # filter AFTER annotate = HAVING

# Authors with average book price > $30
premium_authors = Book.objects.values('author_id').annotate(
    avg_price=Avg('price')
).filter(avg_price__gt=30)

# Combining WHERE and HAVING
# filter BEFORE annotate = WHERE
# filter AFTER annotate = HAVING
active_authors = Book.objects.filter(
    is_available=True           # WHERE
).values('author_id').annotate(
    available_books=Count('id')
).filter(available_books__gt=2)  # HAVING
```

### 📊 WHERE vs HAVING in Django
```python
# WHERE: filter() BEFORE values().annotate()
Book.objects.filter(is_available=True).values('author').annotate(...)

# HAVING: filter() AFTER values().annotate()
Book.objects.values('author').annotate(count=Count('id')).filter(count__gt=5)
```

---

## 2.4 INNER JOIN

### 🎯 What is it?
Combine rows from two tables where there's a **matching value** in both tables.

### 💡 Visual Representation
```
┌─────────┐           ┌─────────┐
│  Books  │           │ Authors │
├─────────┤           ├─────────┤
│ id=1 ───┼──────────►│ id=1    │ ✅ Match
│ id=2 ───┼──────────►│ id=2    │ ✅ Match
│ id=3 ───┼──X        │ id=5    │ ❌ No match (excluded)
└─────────┘           └─────────┘
```

### 🔧 SQL Syntax
```sql
-- Get books with their author names
SELECT book.title, author.name as author_name
FROM book
INNER JOIN author ON book.author_id = author.id;

-- With additional conditions
SELECT book.title, author.name, category.name as category
FROM book
INNER JOIN author ON book.author_id = author.id
INNER JOIN category ON book.category_id = category.id
WHERE book.price < 50;
```

### 🐍 Django ORM Equivalent
```python
# Method 1: Access through relationship (lazy - causes N+1!)
books = Book.objects.all()
for book in books:
    print(book.title, book.author.name)  # Each access = 1 query!

# Method 2: select_related() - EAGER loading (RECOMMENDED)
books = Book.objects.select_related('author')
for book in books:
    print(book.title, book.author.name)  # No extra queries!

# Multiple JOINs
books = Book.objects.select_related('author', 'category')

# With filtering
cheap_books = Book.objects.select_related('author').filter(price__lt=50)

# Get specific fields with JOIN
books = Book.objects.select_related('author').values(
    'title', 'price', 'author__name', 'author__email'
)
```

### 📊 select_related Explained
| Without select_related | With select_related |
|------------------------|---------------------|
| 1 query for books | 1 query with JOIN |
| N queries for authors | 0 extra queries |
| Total: N+1 queries | Total: 1 query |

### 🎓 Pro Tips
1. **select_related()** for ForeignKey and OneToOne relationships
2. **prefetch_related()** for reverse FK and ManyToMany (covered next)
3. Always use for loops that access related objects

---

## 2.5 LEFT JOIN

### 🎯 What is it?
Return **all rows from the left table**, and matching rows from the right table. Non-matching rows get NULL.

### 💡 Visual Representation
```
┌─────────┐           ┌─────────┐
│  Books  │           │Category │
├─────────┤           ├─────────┤
│ id=1 ───┼──────────►│ id=1    │ ✅ Match
│ id=2 ───┼──────────►│ id=2    │ ✅ Match  
│ id=3 ───┼──► NULL   │         │ ✅ Included with NULL
└─────────┘           └─────────┘
```

### 🔧 SQL Syntax
```sql
-- All books, with category if exists
SELECT book.title, category.name as category
FROM book
LEFT JOIN category ON book.category_id = category.id;

-- Find books without a category
SELECT book.title
FROM book
LEFT JOIN category ON book.category_id = category.id
WHERE category.id IS NULL;
```

### 🐍 Django ORM Equivalent
```python
# select_related with nullable FK acts like LEFT JOIN
books = Book.objects.select_related('category')
for book in books:
    category_name = book.category.name if book.category else 'No Category'

# Find books without a category
books_without_category = Book.objects.filter(category__isnull=True)

# All books including those without category
all_books = Book.objects.select_related('category').all()
```

### 💡 When Django Uses LEFT JOIN
- Foreign key is **nullable** (`null=True`)
- Using `filter(related__isnull=True)`
- Using `select_related()` on nullable FK

---

## 2.6 Prefetch Related (Reverse FK & ManyToMany)

### 🎯 What is it?
Efficiently load related objects for **reverse ForeignKey** and **ManyToMany** relationships.

### 💡 The Problem
```python
# N+1 Problem: 101 queries for 100 authors!
authors = Author.objects.all()  # 1 query
for author in authors:
    books = author.books.all()  # 100 queries (1 per author)
```

### 🔧 SQL Equivalent
```sql
-- Two separate queries, combined in Python
-- Query 1: Get all authors
SELECT * FROM author;

-- Query 2: Get all books for those authors
SELECT * FROM book WHERE author_id IN (1, 2, 3, ...);
```

### 🐍 Django ORM Solution
```python
from django.db.models import Prefetch

# Basic prefetch_related
authors = Author.objects.prefetch_related('books')
for author in authors:
    for book in author.books.all():  # No extra queries!
        print(book.title)

# Chain multiple prefetches
authors = Author.objects.prefetch_related('books', 'books__category')

# Custom Prefetch with filtering
from django.db.models import Prefetch

authors = Author.objects.prefetch_related(
    Prefetch(
        'books',
        queryset=Book.objects.filter(is_available=True),
        to_attr='available_books'  # Custom attribute name
    )
)
for author in authors:
    for book in author.available_books:  # Use custom attr
        print(book.title)

# Prefetch with ordering
authors = Author.objects.prefetch_related(
    Prefetch('books', queryset=Book.objects.order_by('-rating'))
)
```

### 📊 select_related vs prefetch_related
| Feature | select_related | prefetch_related |
|---------|----------------|------------------|
| Relationship | ForeignKey, OneToOne | ManyToMany, Reverse FK |
| SQL Method | JOIN | Separate query |
| When to use | Single related object | Multiple related objects |

---

## 2.7 Subqueries

### 🎯 What is it?
A **query inside another query**. Used to filter based on results from another table.

### 💡 Types of Subqueries
1. **Scalar**: Returns single value
2. **Column**: Returns list of values
3. **Correlated**: References outer query

### 🔧 SQL Syntax
```sql
-- Scalar subquery: Books priced above average
SELECT * FROM book
WHERE price > (SELECT AVG(price) FROM book);

-- Column subquery: Books by authors from USA
SELECT * FROM book
WHERE author_id IN (
    SELECT id FROM author WHERE country = 'USA'
);

-- Correlated subquery: Authors with books > $50
SELECT * FROM author
WHERE EXISTS (
    SELECT 1 FROM book 
    WHERE book.author_id = author.id AND book.price > 50
);
```

### 🐍 Django ORM Equivalent
```python
from django.db.models import Subquery, OuterRef, Avg, Exists

# Scalar subquery: Books priced above average
avg_price = Book.objects.aggregate(avg=Avg('price'))['avg']
expensive_books = Book.objects.filter(price__gt=avg_price)

# Using Subquery for dynamic values
from django.db.models import Subquery

# Get the most recent order date for each book
newest_order = Order.objects.filter(
    book=OuterRef('pk')
).order_by('-order_date').values('order_date')[:1]

books_with_recent_order = Book.objects.annotate(
    latest_order_date=Subquery(newest_order)
)

# Column subquery: Books by authors from USA
usa_author_ids = Author.objects.filter(country='USA').values('id')
usa_books = Book.objects.filter(author_id__in=usa_author_ids)
# This creates a subquery automatically!

# Correlated subquery with Exists
from django.db.models import Exists

expensive_book_exists = Book.objects.filter(
    author=OuterRef('pk'),
    price__gt=50
)
authors_with_expensive = Author.objects.annotate(
    has_expensive_book=Exists(expensive_book_exists)
).filter(has_expensive_book=True)
```

### 📊 Key Subquery Patterns
| Pattern | SQL | Django |
|---------|-----|--------|
| Scalar | `WHERE x > (SELECT ...)` | `Subquery(...).values(...)[:1]` |
| IN list | `WHERE x IN (SELECT ...)` | `filter(field__in=queryset)` |
| EXISTS | `WHERE EXISTS (...)` | `Exists(queryset)` |
| Outer ref | Referencing outer query | `OuterRef('field')` |

---

## 2.8 DISTINCT (Unique Values)

### 🎯 What is it?
Remove **duplicate rows** from results.

### 🔧 SQL Syntax
```sql
-- Unique countries
SELECT DISTINCT country FROM author;

-- Unique category-author combinations
SELECT DISTINCT category_id, author_id FROM book;

-- Count distinct values
SELECT COUNT(DISTINCT category_id) FROM book;
```

### 🐍 Django ORM Equivalent
```python
# Unique countries
countries = Author.objects.values_list('country', flat=True).distinct()

# Unique combinations
combos = Book.objects.values('category_id', 'author_id').distinct()

# Count distinct
from django.db.models import Count
distinct_count = Book.objects.aggregate(
    unique_categories=Count('category_id', distinct=True)
)

# distinct() on QuerySet (entire row)
books = Book.objects.order_by('title').distinct()

# PostgreSQL: DISTINCT ON (first per group)
# Get first book per author
first_books = Book.objects.order_by('author_id', 'published_date').distinct('author_id')
```

### ⚠️ PostgreSQL-Specific
```python
# DISTINCT ON - only works in PostgreSQL!
# Get one book per category (the cheapest)
Book.objects.order_by('category_id', 'price').distinct('category_id')
```

---

## 2.9 UNION (Combining Results)

### 🎯 What is it?
Combine results from **multiple queries** into one result set.

### 🔧 SQL Syntax
```sql
-- Combine cheap and highly rated books
SELECT id, title FROM book WHERE price < 20
UNION
SELECT id, title FROM book WHERE rating > 4.5;

-- UNION ALL (keep duplicates)
SELECT id, title FROM book WHERE price < 20
UNION ALL
SELECT id, title FROM book WHERE rating > 4.5;
```

### 🐍 Django ORM Equivalent
```python
# Union of two querysets (removes duplicates)
cheap = Book.objects.filter(price__lt=20)
rated = Book.objects.filter(rating__gt=4.5)
combined = cheap.union(rated)

# Union all (keep duplicates)
combined_all = cheap.union(rated, all=True)

# Multiple unions
qs1 = Book.objects.filter(price__lt=20)
qs2 = Book.objects.filter(rating__gt=4.5)
qs3 = Book.objects.filter(stock__gt=100)
combined = qs1.union(qs2, qs3)

# Intersection (common to both)
common = cheap.intersection(rated)

# Difference (in first but not second)
diff = cheap.difference(rated)
```

### 📊 Set Operations
| SQL | Django | Description |
|-----|--------|-------------|
| `UNION` | `.union(qs)` | Combine, remove duplicates |
| `UNION ALL` | `.union(qs, all=True)` | Combine, keep duplicates |
| `INTERSECT` | `.intersection(qs)` | Common rows |
| `EXCEPT` | `.difference(qs)` | Rows in first, not second |

---

## 2.10 Conditional Expressions (CASE WHEN)

### 🎯 What is it?
Add **conditional logic** directly in SQL/ORM queries.

### 🔧 SQL Syntax
```sql
-- Categorize books by price
SELECT title, price,
    CASE 
        WHEN price < 20 THEN 'Budget'
        WHEN price < 50 THEN 'Mid-range'
        ELSE 'Premium'
    END as price_tier
FROM book;

-- Conditional count
SELECT 
    COUNT(CASE WHEN is_available THEN 1 END) as available,
    COUNT(CASE WHEN NOT is_available THEN 1 END) as unavailable
FROM book;
```

### 🐍 Django ORM Equivalent
```python
from django.db.models import Case, When, Value, CharField, IntegerField

# Categorize books by price
books = Book.objects.annotate(
    price_tier=Case(
        When(price__lt=20, then=Value('Budget')),
        When(price__lt=50, then=Value('Mid-range')),
        default=Value('Premium'),
        output_field=CharField()
    )
)

for book in books:
    print(f"{book.title}: {book.price_tier}")

# Conditional count
from django.db.models import Count, Q

stats = Book.objects.aggregate(
    available=Count('id', filter=Q(is_available=True)),
    unavailable=Count('id', filter=Q(is_available=False))
)

# Update based on condition
Book.objects.update(
    is_available=Case(
        When(stock__gt=0, then=Value(True)),
        default=Value(False)
    )
)
```

---

## 2.11 COALESCE (Default Values)

### 🎯 What is it?
Return the **first non-NULL value** from a list of values.

### 🔧 SQL Syntax
```sql
-- Use 'Unknown' if country is NULL
SELECT name, COALESCE(country, 'Unknown') as country
FROM author;

-- Multiple fallbacks
SELECT title, COALESCE(discount_price, regular_price, 0) as final_price
FROM products;
```

### 🐍 Django ORM Equivalent
```python
from django.db.models.functions import Coalesce
from django.db.models import Value

# Use 'Unknown' if country is NULL
authors = Author.objects.annotate(
    display_country=Coalesce('country', Value('Unknown'))
)

# Multiple fallbacks
products = Product.objects.annotate(
    final_price=Coalesce('discount_price', 'regular_price', Value(0))
)

# In aggregations
from django.db.models import Sum
total = Order.objects.aggregate(
    revenue=Coalesce(Sum('total_price'), Value(0))
)
# If no orders, returns 0 instead of None
```

---

# 📕 LEVEL 3: ADVANCED (Mastery)

## 3.1 F() Expressions (Database-Level Operations)

### 🎯 What is it?
**F() expressions** let you reference database field values directly in queries, enabling:
- Comparisons between two fields
- Database-level calculations
- Atomic updates (avoiding race conditions)

### 💡 Why is it Important?
```python
# ❌ WITHOUT F() - Race condition!
# Two users buy the same book simultaneously
book = Book.objects.get(id=1)  # Both read stock=10
book.stock -= 1                 # Both calculate 9
book.save()                     # Both save 9, but should be 8!

# ✅ WITH F() - Atomic update!
Book.objects.filter(id=1).update(stock=F('stock') - 1)
# Database handles: SET stock = stock - 1
```

### 🔧 SQL Equivalent
```sql
-- Compare two fields
SELECT * FROM book WHERE stock < min_stock;

-- Update with calculation
UPDATE book SET price = price * 1.10 WHERE category_id = 1;

-- Reference another field
UPDATE book SET sale_price = price * 0.8;
```

### 🐍 Django ORM with F()
```python
from django.db.models import F

# Compare two fields
low_stock = Book.objects.filter(stock__lt=F('min_stock'))

# Filter: where price > avg_rating * 10
books = Book.objects.filter(price__gt=F('rating') * 10)

# Update with field reference (10% price increase)
Book.objects.filter(category_id=1).update(price=F('price') * 1.10)

# Bulk update sale prices
Book.objects.update(sale_price=F('price') * 0.8)

# Reference related field
Book.objects.filter(price__gt=F('author__min_book_price'))

# Annotations with F()
from datetime import timedelta
Book.objects.annotate(
    days_since_published=F('published_date') - timedelta(days=30)
)

# Combine F() with Value()
from django.db.models import Value
Book.objects.update(title=F('title') + Value(' (Updated)'))
```

### 📊 F() Use Cases
| Use Case | Example |
|----------|---------|
| Atomic increment | `update(views=F('views') + 1)` |
| Field comparison | `filter(stock__lt=F('min_stock'))` |
| Calculated updates | `update(price=F('price') * 1.1)` |
| Related field access | `filter(price__gt=F('author__fee'))` |

---

## 3.2 Q() Objects (Complex Queries)

### 🎯 What is it?
**Q() objects** enable complex queries with **OR, AND, NOT** logic that can't be expressed with simple filter() chaining.

### 🔧 SQL Equivalent
```sql
-- OR condition
SELECT * FROM book WHERE price < 20 OR rating > 4.5;

-- NOT condition
SELECT * FROM book WHERE NOT (price > 100);

-- Complex nested conditions
SELECT * FROM book 
WHERE (price < 20 AND rating > 4) OR (price < 50 AND stock > 100);
```

### 🐍 Django ORM with Q()
```python
from django.db.models import Q

# OR: Books that are cheap OR highly rated
books = Book.objects.filter(Q(price__lt=20) | Q(rating__gt=4.5))

# NOT: Books that are NOT expensive
books = Book.objects.filter(~Q(price__gt=100))

# Complex nested: (cheap AND good rating) OR (mid-price AND high stock)
books = Book.objects.filter(
    (Q(price__lt=20) & Q(rating__gt=4)) | 
    (Q(price__lt=50) & Q(stock__gt=100))
)

# Dynamic Q objects
conditions = Q()
if search_title:
    conditions &= Q(title__icontains=search_title)
if min_price:
    conditions &= Q(price__gte=min_price)
if max_price:
    conditions &= Q(price__lte=max_price)

books = Book.objects.filter(conditions)

# Combine Q with regular kwargs
books = Book.objects.filter(
    Q(title__icontains='python') | Q(title__icontains='django'),
    is_available=True  # AND with regular kwarg
)
```

### 📊 Q() Operators
| Operator | Meaning | Example |
|----------|---------|---------|
| `\|` | OR | `Q(a=1) \| Q(b=2)` |
| `&` | AND | `Q(a=1) & Q(b=2)` |
| `~` | NOT | `~Q(a=1)` |

---

## 3.3 Window Functions

### 🎯 What is it?
Perform calculations across a **set of rows related to the current row** without collapsing them into one (unlike GROUP BY).

### 💡 Common Window Functions
- **ROW_NUMBER()**: Unique sequential number
- **RANK()**: Ranking with gaps for ties
- **DENSE_RANK()**: Ranking without gaps
- **LAG/LEAD**: Access previous/next rows
- **SUM() OVER**: Running totals

### 🔧 SQL Syntax
```sql
-- Row number per category
SELECT title, category_id, price,
    ROW_NUMBER() OVER (PARTITION BY category_id ORDER BY price) as price_rank
FROM book;

-- Rank books by rating
SELECT title, rating,
    RANK() OVER (ORDER BY rating DESC) as rating_rank
FROM book;

-- Running total
SELECT title, price,
    SUM(price) OVER (ORDER BY id) as running_total
FROM book;

-- Previous and next book price
SELECT title, price,
    LAG(price) OVER (ORDER BY id) as prev_price,
    LEAD(price) OVER (ORDER BY id) as next_price
FROM book;
```

### 🐍 Django ORM Equivalent
```python
from django.db.models import Window, F
from django.db.models.functions import RowNumber, Rank, DenseRank, Lag, Lead, Sum

# Row number per category
books = Book.objects.annotate(
    price_rank=Window(
        expression=RowNumber(),
        partition_by=[F('category_id')],
        order_by=F('price').asc()
    )
)

# Rank books by rating (global)
books = Book.objects.annotate(
    rating_rank=Window(
        expression=Rank(),
        order_by=F('rating').desc()
    )
)

# Running total
books = Book.objects.annotate(
    running_total=Window(
        expression=Sum('price'),
        order_by=F('id').asc()
    )
)

# Previous and next price
books = Book.objects.annotate(
    prev_price=Window(
        expression=Lag('price'),
        order_by=F('id').asc()
    ),
    next_price=Window(
        expression=Lead('price'),
        order_by=F('id').asc()
    )
)

# Get top 3 books per category
from django.db.models import Window
from django.db.models.functions import RowNumber

ranked = Book.objects.annotate(
    rank=Window(
        expression=RowNumber(),
        partition_by=['category_id'],
        order_by=F('rating').desc()
    )
).filter(rank__lte=3)
```

---

## 3.4 Transactions

### 🎯 What is it?
A **transaction** groups multiple database operations so they either ALL succeed or ALL fail (atomic operation).

### 💡 ACID Properties
| Property | Meaning |
|----------|---------|
| **A**tomicity | All or nothing |
| **C**onsistency | Valid state before & after |
| **I**solation | Transactions don't interfere |
| **D**urability | Committed data is permanent |

### 🔧 SQL Syntax
```sql
-- Start transaction
BEGIN;

-- Operations
UPDATE account SET balance = balance - 100 WHERE id = 1;
UPDATE account SET balance = balance + 100 WHERE id = 2;

-- If all good: COMMIT, if error: ROLLBACK
COMMIT;

-- Or in case of error
ROLLBACK;
```

### 🐍 Django ORM Equivalent
```python
from django.db import transaction

# Method 1: Decorator (entire function is atomic)
@transaction.atomic
def transfer_money(from_account, to_account, amount):
    from_account.balance -= amount
    from_account.save()
    
    to_account.balance += amount
    to_account.save()
    # If any error, both saves are rolled back

# Method 2: Context manager (specific block is atomic)
def process_order(order):
    with transaction.atomic():
        order.status = 'processing'
        order.save()
        
        # Reduce stock
        order.book.stock -= order.quantity
        order.book.save()
        
        # Create payment record
        Payment.objects.create(order=order, amount=order.total)
        # If any step fails, all changes are rolled back

# Method 3: Savepoints (nested transactions)
with transaction.atomic():
    # This will be saved
    author = Author.objects.create(name='John')
    
    try:
        with transaction.atomic():
            # This might fail
            Book.objects.create(title='', author=author)  # Error!
    except Exception:
        pass  # Inner transaction rolled back, outer continues
    
    # This still works
    author.email = 'john@example.com'
    author.save()

# Method 4: Manual savepoints
with transaction.atomic():
    a = Author.objects.create(name='Alice')
    
    sid = transaction.savepoint()  # Create savepoint
    try:
        Book.objects.create(title='Test', author=a, price=-5)  # Error
    except Exception:
        transaction.savepoint_rollback(sid)  # Rollback to savepoint
    
    transaction.savepoint_commit(sid)  # Or commit savepoint
```

---

## 3.5 Select For Update (Row Locking)

### 🎯 What is it?
**Lock rows** during a transaction to prevent other transactions from modifying them until you're done.

### 🔧 SQL Syntax
```sql
BEGIN;
SELECT * FROM book WHERE id = 1 FOR UPDATE;
-- Row is now locked
UPDATE book SET stock = stock - 1 WHERE id = 1;
COMMIT;
-- Lock released
```

### 🐍 Django ORM Equivalent
```python
from django.db import transaction

# Basic select_for_update
with transaction.atomic():
    book = Book.objects.select_for_update().get(id=1)
    book.stock -= 1
    book.save()
    # Lock released when transaction ends

# Lock multiple rows
with transaction.atomic():
    cheap_books = Book.objects.select_for_update().filter(price__lt=20)
    cheap_books.update(price=F('price') * 1.1)

# nowait=True: Raise error immediately if locked
try:
    with transaction.atomic():
        book = Book.objects.select_for_update(nowait=True).get(id=1)
except DatabaseError:
    print("Row is locked by another transaction")

# skip_locked=True: Skip locked rows (PostgreSQL 9.5+)
with transaction.atomic():
    available_books = Book.objects.select_for_update(
        skip_locked=True
    ).filter(is_available=True)[:5]
    # Only returns books that aren't locked

# of=['self']: Lock only specific tables in JOINs
with transaction.atomic():
    books = Book.objects.select_for_update(
        of=['self']  # Only lock book table, not author
    ).select_related('author').filter(id=1)
```

---

## 3.6 Indexing & Query Optimization

### 🎯 What is it?
**Indexes** speed up data retrieval by creating a quick lookup structure (like a book's index).

### 💡 When to Index
| ✅ Good for Indexing | ❌ Avoid Indexing |
|---------------------|-------------------|
| Frequently filtered columns | Rarely queried columns |
| JOIN columns (FKs) | Small tables |
| ORDER BY columns | Frequently updated columns |
| Unique constraints | Low cardinality (few unique values) |

### 🔧 SQL Syntax
```sql
-- Create index
CREATE INDEX idx_book_price ON book(price);

-- Composite index
CREATE INDEX idx_book_cat_price ON book(category_id, price);

-- Unique index
CREATE UNIQUE INDEX idx_author_email ON author(email);

-- Partial index (PostgreSQL)
CREATE INDEX idx_available_books ON book(title) WHERE is_available = TRUE;

-- Analyze query performance
EXPLAIN ANALYZE SELECT * FROM book WHERE price < 50;
```

### 🐍 Django ORM Equivalent
```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2, db_index=True)
    published_date = models.DateField(db_index=True)
    
    class Meta:
        # Composite index
        indexes = [
            models.Index(fields=['category', 'price']),
            models.Index(fields=['author', '-published_date']),
            
            # Named index
            models.Index(fields=['title'], name='book_title_idx'),
            
            # Partial index (PostgreSQL)
            models.Index(
                fields=['title'],
                condition=models.Q(is_available=True),
                name='available_books_idx'
            ),
        ]
        
        # Unique constraint (creates unique index)
        constraints = [
            models.UniqueConstraint(fields=['author', 'title'], name='unique_author_title')
        ]

# Explain query (Django 4.0+)
queryset = Book.objects.filter(price__lt=50)
print(queryset.explain())  # Shows execution plan

# Verbose explain
print(queryset.explain(verbose=True, analyze=True))
```

---

## 3.7 Raw SQL Queries

### 🎯 What is it?
Execute **raw SQL** when ORM isn't enough (complex queries, database-specific features).

### 💡 When to Use Raw SQL
- Complex queries that are hard to express in ORM
- Database-specific features (CTEs, recursive queries)
- Performance-critical queries
- Legacy database schemas

### 🐍 Django ORM Methods
```python
from django.db import connection

# Method 1: raw() - Returns model instances
books = Book.objects.raw('SELECT * FROM book WHERE price < %s', [50])
for book in books:
    print(book.title)  # Still a Book object!

# With joins (map columns to model fields)
books = Book.objects.raw('''
    SELECT b.*, a.name as author_name 
    FROM book b 
    JOIN author a ON b.author_id = a.id
''')

# Method 2: connection.cursor() - Pure SQL
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute('SELECT COUNT(*) FROM book WHERE price < %s', [50])
    count = cursor.fetchone()[0]

# Fetch multiple rows
with connection.cursor() as cursor:
    cursor.execute('SELECT id, title FROM book')
    rows = cursor.fetchall()  # List of tuples
    
    # Or as dictionaries
    columns = [col[0] for col in cursor.description]
    rows = [dict(zip(columns, row)) for row in cursor.fetchall()]

# Method 3: Extra (deprecated but still works)
# ⚠️ Deprecated in Django 4.0+
books = Book.objects.extra(
    where=['price < %s'],
    params=[50],
    select={'discounted': 'price * 0.9'}
)

# Method 4: RawSQL expression
from django.db.models.expressions import RawSQL

books = Book.objects.annotate(
    discounted_price=RawSQL('price * %s', (0.9,))
)
```

### ⚠️ SQL Injection Warning
```python
# ❌ NEVER do this - SQL injection vulnerability!
Book.objects.raw(f"SELECT * FROM book WHERE title = '{user_input}'")

# ✅ Always use parameterized queries
Book.objects.raw("SELECT * FROM book WHERE title = %s", [user_input])
```

---

## 3.8 Common Table Expressions (CTEs)

### 🎯 What is it?
**CTEs** (WITH clause) create temporary named result sets for cleaner, more readable complex queries.

### 🔧 SQL Syntax
```sql
-- Basic CTE
WITH cheap_books AS (
    SELECT * FROM book WHERE price < 20
)
SELECT author_id, COUNT(*) 
FROM cheap_books 
GROUP BY author_id;

-- Multiple CTEs
WITH 
    cheap_books AS (SELECT * FROM book WHERE price < 20),
    popular_authors AS (SELECT * FROM author WHERE country = 'USA')
SELECT b.title, a.name
FROM cheap_books b
JOIN popular_authors a ON b.author_id = a.id;

-- Recursive CTE (hierarchical data)
WITH RECURSIVE category_tree AS (
    SELECT id, name, parent_id, 1 as level
    FROM category
    WHERE parent_id IS NULL
    
    UNION ALL
    
    SELECT c.id, c.name, c.parent_id, ct.level + 1
    FROM category c
    JOIN category_tree ct ON c.parent_id = ct.id
)
SELECT * FROM category_tree;
```

### 🐍 Django ORM Options
```python
# Option 1: Use Subquery (often replaces simple CTEs)
from django.db.models import Subquery, OuterRef

cheap_authors = Book.objects.filter(
    price__lt=20
).values('author_id').distinct()

authors_with_cheap_books = Author.objects.filter(
    id__in=Subquery(cheap_authors)
)

# Option 2: django-cte package (for proper CTE support)
# pip install django-cte

from django_cte import With

# Create CTE
cheap_books_cte = With(
    Book.objects.filter(price__lt=20).values('author_id', 'title')
)

# Use CTE in query
result = cheap_books_cte.join(
    Author.objects.all(),
    id=cheap_books_cte.col.author_id
).annotate(
    book_title=cheap_books_cte.col.title
)

# Option 3: Raw SQL for complex CTEs
with connection.cursor() as cursor:
    cursor.execute('''
        WITH RECURSIVE category_tree AS (
            SELECT id, name, parent_id, 1 as level
            FROM category WHERE parent_id IS NULL
            UNION ALL
            SELECT c.id, c.name, c.parent_id, ct.level + 1
            FROM category c
            JOIN category_tree ct ON c.parent_id = ct.id
        )
        SELECT * FROM category_tree ORDER BY level, name
    ''')
    categories = cursor.fetchall()
```

---

## 3.9 Database Views

### 🎯 What is it?
A **view** is a virtual table based on a SQL query. It doesn't store data but provides a convenient way to access complex queries.

### 🔧 SQL Syntax
```sql
-- Create a view
CREATE VIEW book_summary AS
SELECT 
    b.id,
    b.title,
    b.price,
    a.name as author_name,
    c.name as category_name
FROM book b
LEFT JOIN author a ON b.author_id = a.id
LEFT JOIN category c ON b.category_id = c.id;

-- Use the view
SELECT * FROM book_summary WHERE price < 50;
```

### 🐍 Django ORM with Views
```python
# Step 1: Create migration for the view
# In migrations/0002_create_view.py

from django.db import migrations

class Migration(migrations.Migration):
    dependencies = [
        ('myapp', '0001_initial'),
    ]
    
    operations = [
        migrations.RunSQL(
            sql='''
                CREATE OR REPLACE VIEW book_summary AS
                SELECT 
                    b.id,
                    b.title,
                    b.price,
                    a.name as author_name,
                    c.name as category_name
                FROM book b
                LEFT JOIN author a ON b.author_id = a.id
                LEFT JOIN category c ON b.category_id = c.id
            ''',
            reverse_sql='DROP VIEW IF EXISTS book_summary'
        ),
    ]

# Step 2: Create unmanaged model for the view
class BookSummary(models.Model):
    title = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    author_name = models.CharField(max_length=100)
    category_name = models.CharField(max_length=50)
    
    class Meta:
        managed = False  # Django won't create/alter this table
        db_table = 'book_summary'  # Name of the view

# Step 3: Use like a regular model (read-only!)
summaries = BookSummary.objects.filter(price__lt=50)
for s in summaries:
    print(f"{s.title} by {s.author_name}")
```

---

## 3.10 Bulk Operations

### 🎯 What is it?
Efficiently handle **large amounts of data** with minimal database queries.

### 🐍 Django ORM Bulk Methods
```python
# bulk_create - Insert many objects at once
books = [
    Book(title=f'Book {i}', author_id=1, price=i*10)
    for i in range(1000)
]
Book.objects.bulk_create(books, batch_size=100)
# 10 queries instead of 1000!

# bulk_create with ignore_conflicts (skip duplicates)
Book.objects.bulk_create(books, ignore_conflicts=True)

# bulk_create with update_conflicts (upsert - PostgreSQL 9.5+)
Book.objects.bulk_create(
    books,
    update_conflicts=True,
    update_fields=['price', 'stock'],
    unique_fields=['title', 'author_id']
)

# bulk_update - Update many objects at once
books = Book.objects.filter(category_id=1)
for book in books:
    book.price *= 1.1

Book.objects.bulk_update(books, ['price'], batch_size=100)

# Update with a single query (most efficient)
Book.objects.filter(category_id=1).update(price=F('price') * 1.1)

# Delete efficiently
Book.objects.filter(stock=0).delete()

# Chunked processing for very large datasets
def process_in_chunks(queryset, chunk_size=1000):
    total = queryset.count()
    for i in range(0, total, chunk_size):
        chunk = queryset[i:i + chunk_size]
        for obj in chunk:
            process(obj)
        print(f"Processed {min(i + chunk_size, total)} of {total}")

# Using iterator() for memory efficiency
for book in Book.objects.all().iterator(chunk_size=1000):
    process(book)  # Only chunk_size objects in memory at a time
```

---

# 🐘 PostgreSQL-Specific Features

## 4.1 JSONB Fields

### 🎯 What is it?
Store and query **JSON data** directly in PostgreSQL. JSONB is a binary format that's faster than JSON.

### 💡 When to Use
- Flexible/dynamic attributes
- User preferences/settings
- API response caching
- Semi-structured data

### 🔧 SQL Syntax
```sql
-- Create table with JSONB
CREATE TABLE product (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    metadata JSONB
);

-- Insert JSON data
INSERT INTO product (name, metadata) VALUES (
    'Laptop',
    '{"brand": "Dell", "specs": {"ram": 16, "storage": 512}, "tags": ["computer", "work"]}'
);

-- Query JSONB fields
SELECT * FROM product WHERE metadata->>'brand' = 'Dell';
SELECT * FROM product WHERE metadata->'specs'->>'ram' = '16';
SELECT * FROM product WHERE metadata @> '{"brand": "Dell"}';
SELECT * FROM product WHERE metadata ? 'brand';  -- Has key

-- JSONB operators
-- ->  : Get JSON object field (returns JSON)
-- ->> : Get JSON object field as text
-- @>  : Contains
-- ?   : Key exists
-- ?|  : Any key exists
-- ?&  : All keys exist
```

### 🐍 Django ORM Equivalent
```python
from django.db import models
from django.contrib.postgres.fields import JSONField  # Django < 3.1
# from django.db.models import JSONField  # Django 3.1+

class Product(models.Model):
    name = models.CharField(max_length=100)
    metadata = models.JSONField(default=dict)

# Insert JSON data
Product.objects.create(
    name='Laptop',
    metadata={
        'brand': 'Dell',
        'specs': {'ram': 16, 'storage': 512},
        'tags': ['computer', 'work']
    }
)

# Query by key value
dell_products = Product.objects.filter(metadata__brand='Dell')

# Query nested keys
high_ram = Product.objects.filter(metadata__specs__ram=16)

# Check if key exists
has_brand = Product.objects.filter(metadata__has_key='brand')

# Check if any keys exist
has_any = Product.objects.filter(metadata__has_any_keys=['brand', 'model'])

# Check if all keys exist
has_all = Product.objects.filter(metadata__has_keys=['brand', 'specs'])

# Contains (partial match)
dell_match = Product.objects.filter(metadata__contains={'brand': 'Dell'})

# Contained by
contained = Product.objects.filter(metadata__contained_by={'brand': 'Dell', 'model': 'XPS'})

# Update JSON field
from django.db.models import F
from django.db.models.functions import JSONObject
from django.contrib.postgres.fields.jsonb import KeyTransform

# Annotate with JSON value
products = Product.objects.annotate(
    brand_name=KeyTransform('brand', 'metadata')
)
```

---

## 4.2 Array Fields

### 🎯 What is it?
Store **arrays/lists** directly in a PostgreSQL column.

### 🔧 SQL Syntax
```sql
-- Create table with array
CREATE TABLE book (
    id SERIAL PRIMARY KEY,
    title VARCHAR(200),
    tags TEXT[]
);

-- Insert array data
INSERT INTO book (title, tags) VALUES ('Python Guide', ARRAY['programming', 'python', 'tutorial']);

-- Query arrays
SELECT * FROM book WHERE 'python' = ANY(tags);
SELECT * FROM book WHERE tags @> ARRAY['python'];  -- Contains
SELECT * FROM book WHERE tags && ARRAY['python', 'java'];  -- Overlaps
```

### 🐍 Django ORM Equivalent
```python
from django.contrib.postgres.fields import ArrayField

class Book(models.Model):
    title = models.CharField(max_length=200)
    tags = ArrayField(
        models.CharField(max_length=50),
        default=list,
        blank=True
    )
    
    # Nested array
    matrix = ArrayField(
        ArrayField(models.IntegerField()),
        default=list
    )

# Create with array
Book.objects.create(
    title='Python Guide',
    tags=['programming', 'python', 'tutorial']
)

# Query: contains value
python_books = Book.objects.filter(tags__contains=['python'])

# Query: is contained by
simple_tags = Book.objects.filter(tags__contained_by=['python', 'java', 'tutorial'])

# Query: overlaps (any match)
tech_books = Book.objects.filter(tags__overlap=['python', 'java'])

# Query: exact array length
three_tags = Book.objects.filter(tags__len=3)

# Query: index access (PostgreSQL arrays are 1-indexed in SQL, but Django uses 0)
first_tag = Book.objects.filter(tags__0='programming')

# Query: slice
first_two = Book.objects.filter(tags__0_2=['programming', 'python'])
```

---

## 4.3 Full-Text Search

### 🎯 What is it?
Powerful **text search** capabilities built into PostgreSQL (like a mini search engine).

### 🔧 SQL Syntax
```sql
-- Basic full-text search
SELECT * FROM book 
WHERE to_tsvector('english', title || ' ' || description) @@ to_tsquery('python & programming');

-- With ranking
SELECT title, ts_rank(to_tsvector('english', description), to_tsquery('python')) as rank
FROM book
WHERE to_tsvector('english', description) @@ to_tsquery('python')
ORDER BY rank DESC;

-- Create GIN index for performance
CREATE INDEX book_search_idx ON book USING GIN (to_tsvector('english', title || ' ' || description));
```

### 🐍 Django ORM Equivalent
```python
from django.contrib.postgres.search import (
    SearchVector, SearchQuery, SearchRank, 
    SearchHeadline, TrigramSimilarity
)

# Basic search
books = Book.objects.annotate(
    search=SearchVector('title', 'description')
).filter(search='python programming')

# Search with query parsing
query = SearchQuery('python') & SearchQuery('programming')
books = Book.objects.annotate(
    search=SearchVector('title', 'description')
).filter(search=query)

# Search with ranking
vector = SearchVector('title', weight='A') + SearchVector('description', weight='B')
query = SearchQuery('python')
books = Book.objects.annotate(
    rank=SearchRank(vector, query)
).filter(rank__gte=0.1).order_by('-rank')

# Highlight search terms
books = Book.objects.annotate(
    headline=SearchHeadline(
        'description',
        SearchQuery('python'),
        start_sel='<b>',
        stop_sel='</b>'
    )
)

# Trigram similarity (fuzzy matching) - requires pg_trgm extension
from django.contrib.postgres.search import TrigramSimilarity

books = Book.objects.annotate(
    similarity=TrigramSimilarity('title', 'pyhton')  # typo intentional
).filter(similarity__gt=0.3).order_by('-similarity')

# Combined search
from django.contrib.postgres.search import TrigramWordSimilarity

books = Book.objects.annotate(
    similarity=TrigramWordSimilarity('pyton', 'title')
).filter(similarity__gt=0.3)
```

### 📊 Search Weights
| Weight | Value | Use For |
|--------|-------|---------|
| A | 1.0 | Title, Name |
| B | 0.4 | Subtitle, Tags |
| C | 0.2 | Body text |
| D | 0.1 | Metadata |

---

## 4.4 Range Types

### 🎯 What is it?
Store **ranges of values** (dates, numbers) efficiently.

### 🔧 SQL Syntax
```sql
-- Create table with range
CREATE TABLE event (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    duration TSTZRANGE  -- Timestamp with timezone range
);

-- Insert range
INSERT INTO event (name, duration) VALUES (
    'Conference',
    '[2024-01-15 09:00, 2024-01-15 17:00)'
);

-- Query ranges
SELECT * FROM event WHERE duration @> '2024-01-15 12:00'::timestamptz;  -- Contains timestamp
SELECT * FROM event WHERE duration && '[2024-01-15, 2024-01-16)';  -- Overlaps
```

### 🐍 Django ORM Equivalent
```python
from django.contrib.postgres.fields import (
    IntegerRangeField, DateRangeField, DateTimeRangeField
)
from psycopg2.extras import DateTimeTZRange, NumericRange

class Event(models.Model):
    name = models.CharField(max_length=100)
    duration = DateTimeRangeField()

class Room(models.Model):
    name = models.CharField(max_length=50)
    capacity_range = IntegerRangeField()  # e.g., 10-50 people

# Create with range
from datetime import datetime
from psycopg2.extras import DateTimeTZRange

Event.objects.create(
    name='Conference',
    duration=DateTimeTZRange(
        lower=datetime(2024, 1, 15, 9, 0),
        upper=datetime(2024, 1, 15, 17, 0)
    )
)

# Query: contains timestamp
midday = datetime(2024, 1, 15, 12, 0)
events = Event.objects.filter(duration__contains=midday)

# Query: overlaps
jan_15 = DateTimeTZRange(
    datetime(2024, 1, 15), 
    datetime(2024, 1, 16)
)
overlapping = Event.objects.filter(duration__overlap=jan_15)

# Query: fully contained
contained = Event.objects.filter(duration__contained_by=jan_15)

# Query: adjacent ranges
adjacent = Event.objects.filter(duration__adjacent_to=other_range)

# Query: start/end
events = Event.objects.filter(duration__startswith=datetime(2024, 1, 15, 9, 0))
events = Event.objects.filter(duration__endswith=datetime(2024, 1, 15, 17, 0))
```

---

# 🎤 Interview Questions & Answers

## Category 1: Database Basics

### Q1: What is a Database?
**Answer:** A database is an organized collection of structured data stored electronically. It allows efficient storage, retrieval, modification, and deletion of data.

**Pro Tip:** Mention that databases provide data integrity, security, and concurrent access.

---

### Q2: What is the difference between DBMS and RDBMS?
| Feature | DBMS | RDBMS |
|---------|------|-------|
| Data Storage | Files | Tables with rows/columns |
| Relationships | Not supported | Supported via Foreign Keys |
| Data Integrity | Limited | ACID compliance |
| Normalization | Not enforced | Supported |
| Examples | File systems, XML | PostgreSQL, MySQL, SQLite |

**Pro Tip:** Emphasize that all modern databases (PostgreSQL, MySQL) are RDBMS.

---

### Q3: What are the types of databases?
- **Relational (SQL)**: PostgreSQL, MySQL, SQLite
- **NoSQL Document**: MongoDB, CouchDB
- **NoSQL Key-Value**: Redis, DynamoDB
- **NoSQL Graph**: Neo4j
- **Time-Series**: InfluxDB, TimescaleDB

---

### Q4: What is SQL and what are its sublanguages?
```
SQL (Structured Query Language)
├── DDL (Data Definition Language): CREATE, ALTER, DROP, TRUNCATE
├── DML (Data Manipulation Language): SELECT, INSERT, UPDATE, DELETE
├── DCL (Data Control Language): GRANT, REVOKE
└── TCL (Transaction Control Language): COMMIT, ROLLBACK, SAVEPOINT
```

---

## Category 2: Keys & Constraints

### Q5: What is a Primary Key?
**Answer:** A column (or combination) that uniquely identifies each row in a table. Properties:
- Must be unique
- Cannot be NULL
- Only one per table
- Automatically indexed

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL
);
```

---

### Q6: What is a Foreign Key?
**Answer:** A column that references the Primary Key of another table, establishing a relationship.

```sql
-- Parent table
CREATE TABLE author (id SERIAL PRIMARY KEY, name VARCHAR(100));

-- Child table with Foreign Key
CREATE TABLE book (
    id SERIAL PRIMARY KEY,
    title VARCHAR(200),
    author_id INTEGER REFERENCES author(id) ON DELETE CASCADE
);
```

---

### Q7: What is the difference between Primary Key and Unique Key?
| Primary Key | Unique Key |
|-------------|------------|
| Only one per table | Multiple allowed |
| Cannot be NULL | Can have one NULL |
| Creates clustered index | Creates non-clustered index |
| Identifies the row | Ensures uniqueness |

---

### Q8: What are database constraints? Name the types.
| Constraint | Purpose |
|------------|---------|
| PRIMARY KEY | Unique identifier |
| FOREIGN KEY | Referential integrity |
| UNIQUE | No duplicates |
| NOT NULL | No NULL values |
| CHECK | Validate values |
| DEFAULT | Default value if not provided |

---

## Category 3: Normalization

### Q9: What is Normalization? Why is it important?
**Answer:** Normalization is the process of organizing data to reduce redundancy and improve data integrity.

**Benefits:**
- Eliminates data redundancy
- Prevents update, insert, delete anomalies
- Ensures data consistency
- Saves storage space

---

### Q10: Explain the Normal Forms (1NF, 2NF, 3NF, BCNF)

**1NF (First Normal Form):**
- Each cell contains a single value (atomic)
- Each column has a unique name
- No repeating groups

```
❌ Bad: tags = "python, django, flask"
✅ Good: Separate tags table with one tag per row
```

**2NF (Second Normal Form):**
- Must be in 1NF
- No partial dependencies (non-key columns depend on entire primary key)

**3NF (Third Normal Form):**
- Must be in 2NF
- No transitive dependencies (non-key columns don't depend on other non-key columns)

**BCNF (Boyce-Codd Normal Form):**
- Must be in 3NF
- Every determinant is a candidate key

---

### Q11: What is Denormalization?
**Answer:** Intentionally adding redundancy to improve read performance at the cost of write performance.

**Use When:**
- Read-heavy applications
- Complex JOINs are too slow
- Data rarely changes

---

## Category 4: SQL Concepts

### Q12: What is a Subquery?
**Answer:** A query nested inside another query. Types:
- **Scalar**: Returns single value
- **Row**: Returns single row
- **Table**: Returns multiple rows/columns
- **Correlated**: References outer query

```sql
-- Scalar subquery
SELECT * FROM book WHERE price > (SELECT AVG(price) FROM book);

-- Correlated subquery
SELECT * FROM author a WHERE EXISTS (
    SELECT 1 FROM book b WHERE b.author_id = a.id AND b.price > 100
);
```

---

### Q13: What is the difference between Correlated and Non-correlated Subqueries?
| Non-correlated | Correlated |
|----------------|------------|
| Executes once | Executes for each outer row |
| Independent of outer query | References outer query |
| Generally faster | Can be slower |

---

### Q14: What is a View?
**Answer:** A virtual table based on a SQL query. It doesn't store data but provides a convenient way to access complex queries.

```sql
CREATE VIEW active_books AS
SELECT * FROM book WHERE is_available = TRUE;

SELECT * FROM active_books;
```

---

### Q15: What is a Stored Procedure?
**Answer:** Precompiled SQL code that can be executed multiple times. Benefits: reduced network traffic, code reusability, security.

```sql
CREATE PROCEDURE update_stock(book_id INT, quantity INT)
LANGUAGE plpgsql
AS $$
BEGIN
    UPDATE book SET stock = stock - quantity WHERE id = book_id;
END;
$$;

CALL update_stock(1, 5);
```

---

### Q16: What is a Trigger?
**Answer:** A special stored procedure that automatically executes when certain events occur (INSERT, UPDATE, DELETE).

```sql
CREATE TRIGGER update_timestamp
BEFORE UPDATE ON book
FOR EACH ROW
EXECUTE FUNCTION update_modified_column();
```

---

## Category 5: Joins

### Q17: Explain the different types of JOINs
```
┌─────────────────────────────────────────────────────────────┐
│                        JOIN TYPES                            │
├─────────────────────────────────────────────────────────────┤
│ INNER JOIN:  Only matching rows from both tables            │
│ LEFT JOIN:   All rows from left + matching from right       │
│ RIGHT JOIN:  All rows from right + matching from left       │
│ FULL JOIN:   All rows from both tables                      │
│ CROSS JOIN:  Cartesian product (every combination)          │
│ SELF JOIN:   Table joined with itself                       │
└─────────────────────────────────────────────────────────────┘
```

---

### Q18: What is a Self-Join?
**Answer:** A join where a table is joined with itself. Used for hierarchical data.

```sql
-- Find employees and their managers
SELECT e.name as employee, m.name as manager
FROM employee e
LEFT JOIN employee m ON e.manager_id = m.id;
```

---

### Q19: What is a Cross Join?
**Answer:** Returns the Cartesian product of both tables (every row from A combined with every row from B).

```sql
-- If A has 3 rows and B has 4 rows, result has 12 rows
SELECT * FROM color CROSS JOIN size;
```

---

## Category 6: Indexing & Performance

### Q20: What is an Index?
**Answer:** A data structure that improves the speed of data retrieval. Like a book's index - helps find data without scanning every row.

---

### Q21: What is the difference between Clustered and Non-clustered Index?
| Clustered | Non-clustered |
|-----------|---------------|
| Physically reorders data | Logical ordering only |
| One per table | Multiple per table |
| Faster for range queries | Faster for exact lookups |
| Primary Key by default | Created explicitly |

---

### Q22: When should you NOT use an index?
- Small tables
- Columns rarely used in WHERE
- Frequently updated columns
- Low cardinality columns (few unique values)
- Tables with heavy write operations

---

### Q23: What is EXPLAIN ANALYZE?
**Answer:** Shows the query execution plan, helping identify performance issues.

```sql
EXPLAIN ANALYZE SELECT * FROM book WHERE price < 50;
-- Shows: execution time, rows examined, index usage
```

---

### Q24: What is the N+1 Query Problem?
**Answer:** Executing 1 query to fetch N items, then N additional queries for related data.

```python
# ❌ N+1 Problem
books = Book.objects.all()  # 1 query
for book in books:
    print(book.author.name)  # N queries!

# ✅ Solution
books = Book.objects.select_related('author')  # 1 query with JOIN
```

---

## Category 7: Transactions & ACID

### Q25: What are ACID properties?
| Property | Meaning |
|----------|---------|
| **A**tomicity | All operations succeed or all fail |
| **C**onsistency | Database moves from valid state to valid state |
| **I**solation | Concurrent transactions don't interfere |
| **D**urability | Committed data survives system failures |

---

### Q26: What is a Transaction?
**Answer:** A sequence of operations treated as a single logical unit. Either all succeed (COMMIT) or all fail (ROLLBACK).

```sql
BEGIN;
UPDATE account SET balance = balance - 100 WHERE id = 1;
UPDATE account SET balance = balance + 100 WHERE id = 2;
COMMIT;  -- Or ROLLBACK if error
```

---

### Q27: What is a Deadlock?
**Answer:** When two or more transactions are waiting for each other to release locks, creating a circular dependency.

**Prevention:**
- Consistent lock ordering
- Lock timeout
- Keep transactions short

---

### Q28: What are Isolation Levels?
| Level | Dirty Read | Non-repeatable Read | Phantom Read |
|-------|------------|---------------------|--------------|
| Read Uncommitted | ✅ Yes | ✅ Yes | ✅ Yes |
| Read Committed | ❌ No | ✅ Yes | ✅ Yes |
| Repeatable Read | ❌ No | ❌ No | ✅ Yes |
| Serializable | ❌ No | ❌ No | ❌ No |

---

## Category 8: Django ORM Specific

### Q29: What is an ORM?
**Answer:** Object-Relational Mapping - a technique to interact with databases using programming language objects instead of raw SQL.

**Benefits:**
- No SQL knowledge needed
- Database-agnostic
- Automatic SQL injection prevention
- Easier maintenance

---

### Q30: What is QuerySet in Django?
**Answer:** An object representing a database query. QuerySets are lazy - they don't hit the database until evaluated.

```python
# Query not executed yet
books = Book.objects.filter(price__lt=50)

# Query executed when:
list(books)      # Convert to list
for book in books:  # Iterate
    pass
len(books)       # Count
books[0]         # Index access
```

---

### Q31: What is the difference between filter() and get()?
| filter() | get() |
|----------|-------|
| Returns QuerySet | Returns single object |
| Empty if no match | Raises DoesNotExist |
| Multiple results OK | Raises MultipleObjectsReturned |

---

### Q32: What is the difference between select_related and prefetch_related?
| select_related | prefetch_related |
|----------------|------------------|
| ForeignKey, OneToOne | ManyToMany, Reverse FK |
| Single query with JOIN | Separate queries |
| Loads single related object | Loads multiple related objects |

```python
# select_related: 1 query with JOIN
Book.objects.select_related('author')

# prefetch_related: 2 queries (Books + Authors)
Author.objects.prefetch_related('books')
```

---

### Q33: What are F() expressions?
**Answer:** Reference database column values in queries for atomic operations.

```python
# Atomic increment
Book.objects.filter(id=1).update(views=F('views') + 1)

# Compare fields
Book.objects.filter(stock__lt=F('min_stock'))
```

---

### Q34: What are Q() objects?
**Answer:** Enable complex queries with OR, AND, NOT logic.

```python
from django.db.models import Q

# OR condition
Book.objects.filter(Q(price__lt=20) | Q(rating__gt=4.5))

# NOT condition
Book.objects.filter(~Q(is_available=True))
```

---

### Q35: What is the difference between aggregate() and annotate()?
| aggregate() | annotate() |
|-------------|------------|
| Returns dictionary | Returns QuerySet |
| Single result for entire query | Value for each object |
| Used for totals | Used for per-object calculations |

```python
# aggregate: single total
Book.objects.aggregate(avg_price=Avg('price'))
# {'avg_price': 29.99}

# annotate: per-object
Author.objects.annotate(num_books=Count('books'))
# Each author has 'num_books' attribute
```

---

### Q36: How to prevent SQL injection in Django?
**Answer:** Django ORM automatically escapes parameters. When using raw SQL:

```python
# ❌ VULNERABLE
Book.objects.raw(f"SELECT * FROM book WHERE title = '{user_input}'")

# ✅ SAFE - parameterized query
Book.objects.raw("SELECT * FROM book WHERE title = %s", [user_input])
```

---

## Category 9: PostgreSQL Specific

### Q37: Why choose PostgreSQL over MySQL?
| PostgreSQL | MySQL |
|------------|-------|
| Better ACID compliance | Faster reads |
| Advanced data types (JSONB, Arrays) | Simpler to set up |
| Full-text search built-in | Requires plugins |
| Window functions | Limited support |
| Better for complex queries | Better for simple apps |

---

### Q38: What is JSONB in PostgreSQL?
**Answer:** Binary JSON storage with indexing support. Faster than JSON for queries.

```python
# Django
class Product(models.Model):
    metadata = models.JSONField()

# Query nested JSON
Product.objects.filter(metadata__specs__ram=16)
```

---

### Q39: What is MVCC?
**Answer:** Multi-Version Concurrency Control - PostgreSQL's method of handling concurrent transactions. Each transaction sees a snapshot of data, allowing readers and writers to not block each other.

---

## Category 10: Advanced Concepts

### Q40: What is Database Sharding?
**Answer:** Splitting a large database into smaller, faster pieces called shards, distributed across multiple servers.

**Types:**
- Horizontal: Split rows
- Vertical: Split columns/tables

---

### Q41: What is Database Replication?
**Answer:** Copying data from one database server to others for redundancy and performance.

**Types:**
- Master-Slave: One write, multiple read
- Master-Master: Multiple write nodes

---

### Q42: What is Connection Pooling?
**Answer:** Reusing database connections instead of creating new ones for each request. Improves performance.

```python
# Django settings
DATABASES = {
    'default': {
        ...
        'CONN_MAX_AGE': 60,  # Connection lifetime in seconds
    }
}
```

---

### Q43: What is a Materialized View?
**Answer:** A view that stores the query result physically. Must be refreshed to update data.

```sql
CREATE MATERIALIZED VIEW book_stats AS
SELECT author_id, COUNT(*) as book_count, AVG(price) as avg_price
FROM book GROUP BY author_id;

REFRESH MATERIALIZED VIEW book_stats;
```

---

### Q44: What is the difference between DELETE and TRUNCATE?
| DELETE | TRUNCATE |
|--------|----------|
| DML (logged) | DDL (minimal logging) |
| Can use WHERE | Removes all rows |
| Triggers fire | No triggers |
| Can be rolled back | Usually not |
| Slower | Faster |

---

### Q45: What is the difference between UNION and UNION ALL?
| UNION | UNION ALL |
|-------|-----------|
| Removes duplicates | Keeps duplicates |
| Slower (needs sorting) | Faster |

---

### Q46: What is the difference between WHERE and HAVING?
| WHERE | HAVING |
|-------|--------|
| Filters rows | Filters groups |
| Before GROUP BY | After GROUP BY |
| Can't use aggregates | Uses aggregates |

```sql
SELECT author_id, COUNT(*)
FROM book
WHERE price > 10       -- Filter rows first
GROUP BY author_id
HAVING COUNT(*) > 5;   -- Then filter groups
```

---

### Q47: What is a CTE (Common Table Expression)?
**Answer:** A temporary named result set for cleaner complex queries.

```sql
WITH expensive_books AS (
    SELECT * FROM book WHERE price > 100
)
SELECT author_id, COUNT(*) 
FROM expensive_books 
GROUP BY author_id;
```

---

### Q48: What is the difference between EXISTS and IN?
| EXISTS | IN |
|--------|-----|
| Returns TRUE/FALSE | Compares values |
| Stops at first match | Checks all values |
| Better for large subqueries | Better for small lists |

---

### Q49: How would you optimize a slow query?
1. **Use EXPLAIN ANALYZE** to understand the execution plan
2. **Add appropriate indexes** for frequently filtered columns
3. **Avoid SELECT *** - fetch only needed columns
4. **Use LIMIT** for pagination
5. **Optimize JOINs** with proper indexes
6. **Use connection pooling**
7. **Consider caching** for frequently accessed data
8. **Denormalize** if read-heavy

---

### Q50: How to handle database migrations in Django?
```bash
# Create migration files
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Show migration status
python manage.py showmigrations

# Rollback migration
python manage.py migrate app_name migration_number
```

---

# 📋 Quick Reference Cheat Sheet

## Basic CRUD Operations

| Operation | SQL | Django ORM |
|-----------|-----|------------|
| Get all | `SELECT * FROM book` | `Book.objects.all()` |
| Get columns | `SELECT title, price FROM book` | `Book.objects.values('title', 'price')` |
| Get single | `SELECT * FROM book WHERE id = 1` | `Book.objects.get(id=1)` |
| Insert | `INSERT INTO book (title) VALUES ('Test')` | `Book.objects.create(title='Test')` |
| Update | `UPDATE book SET price = 10 WHERE id = 1` | `Book.objects.filter(id=1).update(price=10)` |
| Delete | `DELETE FROM book WHERE id = 1` | `Book.objects.filter(id=1).delete()` |
| Count | `SELECT COUNT(*) FROM book` | `Book.objects.count()` |

## Filtering (WHERE)

| SQL | Django ORM Lookup |
|-----|-------------------|
| `= value` | `field=value` |
| `< value` | `field__lt=value` |
| `> value` | `field__gt=value` |
| `<= value` | `field__lte=value` |
| `>= value` | `field__gte=value` |
| `!= value` | `exclude(field=value)` |
| `BETWEEN a AND b` | `field__range=(a, b)` |
| `IN (1, 2, 3)` | `field__in=[1, 2, 3]` |
| `IS NULL` | `field__isnull=True` |
| `IS NOT NULL` | `field__isnull=False` |

## Text Search (LIKE)

| SQL | Django ORM |
|-----|------------|
| `LIKE 'abc%'` | `field__startswith='abc'` |
| `LIKE '%abc'` | `field__endswith='abc'` |
| `LIKE '%abc%'` | `field__contains='abc'` |
| `ILIKE '%abc%'` | `field__icontains='abc'` |
| `= 'abc'` | `field__exact='abc'` |
| `~* 'pattern'` | `field__iregex='pattern'` |

## Sorting & Limiting

| SQL | Django ORM |
|-----|------------|
| `ORDER BY field ASC` | `.order_by('field')` |
| `ORDER BY field DESC` | `.order_by('-field')` |
| `ORDER BY RANDOM()` | `.order_by('?')` |
| `LIMIT 10` | `[:10]` |
| `LIMIT 10 OFFSET 20` | `[20:30]` |
| Get first | `.first()` |
| Get last | `.last()` |

## Aggregations

| SQL | Django ORM |
|-----|------------|
| `COUNT(*)` | `Count('id')` |
| `SUM(field)` | `Sum('field')` |
| `AVG(field)` | `Avg('field')` |
| `MIN(field)` | `Min('field')` |
| `MAX(field)` | `Max('field')` |

```python
from django.db.models import Count, Sum, Avg, Min, Max

# Single aggregate
Book.objects.aggregate(total=Sum('price'))

# Per-group aggregation (GROUP BY)
Book.objects.values('category').annotate(count=Count('id'))
```

## JOINs

| SQL | Django ORM |
|-----|------------|
| `INNER JOIN` (FK) | `.select_related('field')` |
| `LEFT JOIN` (nullable FK) | `.select_related('field')` with `null=True` |
| Reverse FK / M2M | `.prefetch_related('field')` |
| Custom prefetch | `Prefetch('field', queryset=...)` |

## Complex Conditions

```python
from django.db.models import Q, F

# OR condition
Q(price__lt=20) | Q(rating__gt=4.5)

# AND condition
Q(price__lt=20) & Q(is_available=True)

# NOT condition
~Q(is_available=True)

# Compare two fields
F('stock') < F('min_stock')

# Atomic update
.update(views=F('views') + 1)
```

## Common Patterns

```python
# Avoid N+1 (ForeignKey)
Book.objects.select_related('author', 'category')

# Avoid N+1 (Reverse FK / M2M)
Author.objects.prefetch_related('books')

# Get or Create
obj, created = Model.objects.get_or_create(
    field=value,
    defaults={'other_field': value}
)

# Update or Create
obj, created = Model.objects.update_or_create(
    field=value,
    defaults={'other_field': value}
)

# Bulk operations
Model.objects.bulk_create([obj1, obj2, ...])
Model.objects.bulk_update(objs, ['field1', 'field2'])

# Transaction
from django.db import transaction
with transaction.atomic():
    # Your operations here
```

## PostgreSQL-Specific

```python
# JSONField
Model.objects.filter(data__key='value')
Model.objects.filter(data__nested__key='value')
Model.objects.filter(data__has_key='key')

# ArrayField
Model.objects.filter(tags__contains=['python'])
Model.objects.filter(tags__overlap=['python', 'django'])

# Full-text Search
from django.contrib.postgres.search import SearchVector, SearchQuery
Model.objects.annotate(
    search=SearchVector('title', 'description')
).filter(search=SearchQuery('python'))
```

---

# 🏁 Congratulations!

You've completed the **SQL & Django ORM Masterclass**! 🎉

## What You've Learned:

| Level | Topics |
|-------|--------|
| 📗 **Beginner** | CRUD, Filtering, Sorting, Pagination |
| 📘 **Intermediate** | JOINs, Aggregations, GROUP BY, Subqueries |
| 📕 **Advanced** | Transactions, Indexing, Window Functions, CTEs |
| 🐘 **PostgreSQL** | JSONB, Arrays, Full-Text Search |
| 🎤 **Interview** | 50+ questions with answers |

## Next Steps:

1. **Practice** - Write queries daily
2. **EXPLAIN your queries** - Understand performance
3. **Build projects** - Apply what you learned
4. **Optimize** - Look for N+1 problems
5. **Interview prep** - Review the Q&A section

---

> **Pro Tip:** Bookmark this guide and use the Cheat Sheet as a quick reference while coding!

**Happy Coding!** 🚀



---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
