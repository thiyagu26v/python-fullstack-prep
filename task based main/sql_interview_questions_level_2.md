---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# SQL/PostgreSQL Level 2 Mastery (Advanced & Scenarios)

This document covers 50 advanced SQL and PostgreSQL scenarios, focusing on analytical power, recursion, and database optimization.

---

## **Section 1: Window Functions (Q1-10)**

### **1. Rank employees by salary within each department**

**Input (`employees`):**
| name | dept | salary |
|---|---|---|
| Alice | IT | 7000 |
| Bob | HR | 5000 |
| Charlie | IT | 8000 |

#### **Solution:**
```sql
SELECT name, dept, salary,
       RANK() OVER (                -- Assigns rank, skips numbers if there's a tie (1, 2, 2, 4)
           PARTITION BY dept        -- Reset ranking for each department
           ORDER BY salary DESC     -- Highest salary gets rank 1
       ) as salary_rank
FROM employees;
```

**Output:**
| name | dept | salary | salary_rank |
|---|---|---|---|
| Charlie | IT | 8000 | 1 |
| Alice | IT | 7000 | 2 |
| Bob | HR | 5000 | 1 |

---

### **2. Difference between RANK(), DENSE_RANK(), and ROW_NUMBER()**

**Input (`employees`):**
| name | salary |
|---|---|
| Alice | 5000 |
| Bob | 5000 |
| Charlie | 4000 |

#### **Solution:**
```sql
SELECT name, salary,
       ROW_NUMBER() OVER(ORDER BY salary DESC) as row_num,   -- Unique sequential ID (1, 2, 3, 4)
       RANK()       OVER(ORDER BY salary DESC) as rnk,       -- Skips after ties (1, 2, 2, 4)
       DENSE_RANK() OVER(ORDER BY salary DESC) as dense_rnk  -- No gaps after ties (1, 2, 2, 3)
FROM employees;
```

**Output:**
| name | salary | row_num | rnk | dense_rnk |
|---|---|---|---|---|
| Alice | 5000 | 1 | 1 | 1 |
| Bob | 5000 | 2 | 1 | 1 |
| Charlie | 4000 | 3 | 3 | 2 |

---

### **3. Find the top 3 highest-paid employees in each department**

**Input (`employees`):** (Simplified)
Imagine IT has 5 people with salaries: 10k, 9k, 8k, 7k, 6k.

#### **Solution:**
```sql
WITH RankedEmployees AS (           -- Using a CTE for readability
    SELECT name, dept, salary,
           DENSE_RANK() OVER (PARTITION BY dept ORDER BY salary DESC) as rnk
    FROM employees
)
SELECT * 
FROM RankedEmployees 
WHERE rnk <= 3;                     -- Filter inside the result of the window function
```

**Output:** (First 3 for IT)
| name | dept | salary | rnk |
|---|---|---|---|
| A | IT | 10000 | 1 |
| B | IT | 9000 | 2 |
| C | IT | 8000 | 3 |

---

### **4. Calculate a running total of salary for the whole company**

**Input (`employees`):**
| id | name | salary |
|---|---|---|
| 1 | Alice | 1000 |
| 2 | Bob | 2000 |
| 3 | Charlie | 3000 |

#### **Solution:**
```sql
SELECT name, salary,
       SUM(salary) OVER (           -- Aggregation as a Window Function
           ORDER BY id              -- Sums rows from the start up to the current row
       ) as running_total
FROM employees;
```

**Output:**
| name | salary | running_total |
|---|---|---|
| Alice | 1000 | 1000 |
| Bob | 2000 | 3000 |
| Charlie | 3000 | 6000 |

---

### **5. Find the difference in salary between an employee and the previous employee (LEAD/LAG)**

**Input (`employees`):**
| name | salary |
|---|---|
| Alice | 1000 |
| Bob | 2500 |
| Charlie | 3000 |

#### **Solution:**
```sql
SELECT name, salary,
       LAG(salary) OVER (ORDER BY salary) as prev_sal,       -- Gets value from the PREVIOUS row
       salary - LAG(salary) OVER (ORDER BY salary) as diff   -- Direct subtraction
FROM employees;
```

**Output:**
| name | salary | prev_sal | diff |
|---|---|---|---|
| Alice | 1000 | NULL | NULL |
| Bob | 2500 | 1000 | 1500 |
| Charlie | 3000 | 2500 | 500 |

---

### **6. Find the next employee's name for each employee in a sequence**

**Input (`employees`):**
| id | name |
|---|---|
| 1 | Alice |
| 2 | Bob |
| 3 | Charlie |

#### **Solution:**
```sql
SELECT name,
       LEAD(name) OVER (ORDER BY id) as next_person          -- Gets value from the NEXT row
FROM employees;
```

**Output:**
| name | next_person |
|---|---|
| Alice | Bob |
| Bob | Charlie |
| Charlie | NULL |

---

### **7. Find the first and last salary in each department using Window Functions**

**Input (`employees`):**
| name | dept | salary |
|---|---|---|
| A | IT | 100 |
| B | IT | 200 |
| C | IT | 300 |

#### **Solution:**
```sql
SELECT name, dept, 
       FIRST_VALUE(salary) OVER (PARTITION BY dept ORDER BY salary DESC) as highest,
       LAST_VALUE(salary) OVER (
           PARTITION BY dept ORDER BY salary DESC
           ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING -- Define whole window
       ) as lowest
FROM employees;
```

**Output:**
| name | dept | highest | lowest |
|---|---|---|---|
| A | IT | 300 | 100 |
| B | IT | 300 | 100 |
| C | IT | 300 | 100 |

---

### **8. Calculate moving average of sales over the last 3 months**

**Input (`sales_data`):**
| month | sales |
|---|---|
| 1 | 100 |
| 2 | 200 |
| 3 | 300 |
| 4 | 400 |

#### **Solution:**
```sql
SELECT month, sales,
       AVG(sales) OVER (
           ORDER BY month
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW -- Current row + 2 previous = 3 months
       ) as moving_avg
FROM sales_data;
```

**Output:**
| month | sales | moving_avg |
|---|---|---|
| 1 | 100 | 100 |
| 2 | 200 | 150 |
| 3 | 300 | 200 |
| 4 | 400 | 300 |

---

### **9. Use NTILE to divide employees into 4 quartiles based on salary**

**Input (`employees`):** (Suppose 8 employees)

#### **Solution:**
```sql
SELECT name, salary,
       NTILE(4) OVER (ORDER BY salary DESC) as quartile -- Distributes rows into 4 buckets
FROM employees;
```

**Output:** (Bucket numbers from 1 to 4)

---

### **10. Find the percentage contribution of each employee's salary to their department total**

**Input (`employees`):**
| name | dept | salary |
|---|---|---|
| Alice | IT | 100 |
| Bob | IT | 400 |

#### **Solution:**
```sql
SELECT name, dept, salary,
       (salary * 100.0) / SUM(salary) OVER (PARTITION BY dept) as percent_contribution
FROM employees;
```

**Output:**
| name | dept | percent_contribution |
|---|---|---|
| Alice | IT | 20.0 |
| Bob | IT | 80.0 |

---

## **Section 2: CTEs & Advanced Joins (Q11-20)**

### **11. Use a CTE to find employees with high salaries and then filter them**

**Input (`employees`):**
| name | dept | salary |
|---|---|---|
| Boss | IT | 100000 |
| Worker | IT | 30000 |

#### **Solution:**
```sql
WITH HighEarners AS (              -- CTE improves query structure and readability
    SELECT * FROM employees WHERE salary > 90000
)
SELECT name, dept FROM HighEarners WHERE dept = 'IT';
```

**Output:**
| name | dept |
|---|---|
| Boss | IT |

---

### **12. Recursive CTE: Generate a sequence of numbers from 1 to 10**

#### **Solution:**
```sql
WITH RECURSIVE counter(n) AS (     -- RECURSIVE keyword is required in Postgres
    SELECT 1                       -- Base case (Non-recursive part)
    UNION ALL
    SELECT n + 1 FROM counter WHERE n < 10 -- Recursive part
)
SELECT * FROM counter;
```

**Output:** Rows from 1 to 10.

---

### **13. Recursive CTE: Find the management hierarchy (Boss -> Subordinate)**

**Input (`employees`):**
| id | name | manager_id |
|---|---|---|
| 1 | CEO | NULL |
| 2 | VP | 1 |
| 3 | MGR | 2 |

#### **Solution:**
```sql
WITH RECURSIVE OrgChart AS (
    SELECT id, name, manager_id, 1 as level -- Base case: The CEO (top level)
    FROM employees WHERE manager_id IS NULL
    UNION ALL
    SELECT e.id, e.name, e.manager_id, o.level + 1 -- Recursive: Fetch subordinates
    FROM employees e
    JOIN OrgChart o ON e.manager_id = o.id        -- Join back to previous results
)
SELECT * FROM OrgChart ORDER BY level;
```

**Output:**
| id | name | level |
|---|---|---|
| 1 | CEO | 1 |
| 2 | VP | 2 |
| 3 | MGR | 3 |

---

### **14. Self Join: Find employees who joined before their managers**

**Input (`employees`):**
| id | name | joining_date | manager_id |
|---|---|---|---|
| 1 | Manager | 2023-05-01 | NULL |
| 2 | Senior | 2023-01-01 | 1 |

#### **Solution:**
```sql
SELECT e.name as emp, e.joining_date as emp_date,
       m.name as mgr, m.joining_date as mgr_date
FROM employees e
JOIN employees m ON e.manager_id = m.id
WHERE e.joining_date < m.joining_date; -- Logic applied across joined columns
```

**Output:**
| emp | emp_date | mgr | mgr_date |
|---|---|---|---|
| Senior | 2023-01-01 | Manager | 2023-05-01 |

---

### **15. Find "Active" users who haven't logged in since last month**

**Input (`users`):** (Today is 2023-12-01)
| name | status | last_login |
|---|---|---|
| Active1 | active | 2023-10-01 |

#### **Solution:**
```sql
SELECT * FROM users 
WHERE status = 'active'
  AND last_login < CURRENT_DATE - INTERVAL '1 month'; -- PostgreSQL Date interval syntax
```

---

### **16. Use a LATERAL JOIN to find the top 2 orders for each customer**

**Input (`customers` / `orders`):** Lists of orders per customer.

#### **Solution:**
```sql
SELECT c.name, o.*
FROM customers c
CROSS JOIN LATERAL (               -- LATERAL allows the subquery to reference 'c'
    SELECT * FROM orders 
    WHERE customer_id = c.id 
    ORDER BY order_date DESC 
    LIMIT 2
) o;
```

---

### **17. Anti-Join: Find products that have NEVER been ordered**

**Input (`products` / `orders`):**
| prod | id |
|---|---|
| Phone | 1 |
| Car | 2 |

(Orders only contains prod_id 1)

#### **Solution:**
```sql
SELECT p.name 
FROM products p
LEFT JOIN orders o ON p.id = o.product_id
WHERE o.id IS NULL;                -- Classic Left Join / Null Check pattern
```

**Output:** Car.

---

### **18. Find common records in two tables with different schemas (Set logic)**

#### **Solution:**
```sql
-- INTERSECT only works if columns match; otherwise use JOIN
SELECT name FROM employees
INTERSECT
SELECT name FROM contractors;
```

---

### **19. Find the Median salary of the company (using PERCENTILE_CONT)**

#### **Solution:**
```sql
SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) as median_salary
FROM employees;                    -- Statistical function provided by PostgreSQL
```

---

### **20. Identify "Gaps" in a sequence of IDs**

**Input (`tickets`):**
| id |
|---|
| 1 |
| 2 |
| 4 |

#### **Solution:**
```sql
SELECT id + 1 as gap_start
FROM tickets t
WHERE NOT EXISTS (
    SELECT 1 FROM tickets t2 WHERE t2.id = t.id + 1
) AND id < (SELECT MAX(id) FROM tickets);
```

**Output:** 3.

---

## **Section 3: PostgreSQL Special Features (Q21-30)**

### **21. Store and query JSONB data**

#### **Solution:**
```sql
-- Inserting JSON
INSERT INTO logs (data) VALUES ('{"status": "error", "code": 500}'::jsonb);

-- Querying JSON key
SELECT data->>'status' as status_val -- ->> returns text, -> returns jsonb object
FROM logs 
WHERE data @> '{"status": "error"}';  -- @> checks for inclusion (very fast with GIN index)
```

---

### **22. Working with Postgres Arrays**

**Input (`posts`):**
| tags |
|---|
| {'sql', 'db'} |

#### **Solution:**
```sql
SELECT name, tags[1] as primary_tag -- Arrays are 1-based in Postgres
FROM posts 
WHERE 'sql' = ANY(tags);            -- Checks if 'sql' exists anywhere in the tags array
```

---

### **23. Upsert: INSERT ... ON CONFLICT (The PostgreSQL approach to Merge)**

#### **Solution:**
```sql
INSERT INTO settings (key, value)
VALUES ('theme', 'dark')
ON CONFLICT (key)                   -- Target unique constraint
DO UPDATE SET value = EXCLUDED.value; -- Update if key exists (EXCLUDED holds new value)
```

---

### **24. Generate a series of dates (Projecting missing days)**

#### **Solution:**
```sql
-- Useful for generating a range for reporting even when data is missing for some days
SELECT generate_series(
    '2023-01-01'::date, 
    '2023-01-10'::date, 
    '1 day'::interval
) as day;
```

---

### **25. Use Materialized Views for reporting**

#### **Solution:**
```sql
CREATE MATERIALIZED VIEW sales_summary AS -- Physically stores query result
SELECT prod_id, SUM(price) FROM sales GROUP BY prod_id;

-- To sync with latest data:
REFRESH MATERIALIZED VIEW sales_summary; 
```

### **26. Optimize a "WHERE id IN (...)" query for large datasets**

**Input (`employees` / `temp_ids`):**
| id | name |
|---|---|
| 1 | Alice |
| 2 | Bob |

(Temp IDs contains: 1)

#### **Solution:**
```sql
-- Use JOIN or EXISTS instead of large IN clauses for better planner optimization
SELECT * FROM employees e
WHERE EXISTS (
    SELECT 1 FROM temp_ids t WHERE t.id = e.id
);
```

**Output:** Alice.

---

### **27. Indexing: Create a partial index for active records**

#### **Solution:**
```sql
CREATE INDEX idx_active_users ON users(id)
WHERE is_active = true;         -- Index only rows matching the condition (saves space/time)
```

**Effect:** A smaller, specialized index for active users only.

---

### **28. Using EXPLAIN ANALYZE to debug performance**

#### **Solution:**
```sql
EXPLAIN ANALYZE                 -- ANALYZE actually executes the query to get real timing
SELECT * FROM orders 
JOIN items ON orders.id = items.order_id 
WHERE orders.status = 'shipped'; -- Planner shows: Seq Scan vs Index Scan, Join type, Cost
```

**Output:** Literal execution plan with timings (Actual time vs Cost).

---

### **29. Creating a GIN index for JSONB multi-path search**

#### **Solution:**
```sql
CREATE INDEX idx_data_gin ON logs USING GIN (data); 
-- Allows fast searching for any key-value pair inside the JSONB column
```

---

### **30. Implement "Pagination" using Keysets (Faster than OFFSET)**

**Input (`logs`):** (Paginated)

#### **Solution:**
```sql
-- Faster pagination (no need to skip rows)
SELECT * FROM logs 
WHERE id > 10250                -- Start from the last ID seen on previous page
ORDER BY id ASC 
LIMIT 50;
```

---

## **Section 4: Complex Scenarios & Logic (Q31-40)**

### **31. Gaps and Islands: Find sequences of consecutive login days**

**Input (`logins`):**
| user_id | login_date |
|---|---|
| 1 | 2023-01-01 |
| 1 | 2023-01-02 |
| 1 | 2023-01-04 |

#### **Solution:**
```sql
WITH DayGroups AS (
    SELECT user_id, login_date,
           login_date - (ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY login_date) * INTERVAL '1 day') as grp
    FROM logins
)
SELECT user_id, MIN(login_date), MAX(login_date), COUNT(*) as streak
FROM DayGroups
GROUP BY user_id, grp;           -- Logic: Date - RowNumber remains identical for consecutive blocks
```

**Output:**
| user_id | start | end | streak |
|---|---|---|---|
| 1 | 2023-01-01 | 2023-01-02 | 2 |
| 1 | 2023-01-04 | 2023-01-04 | 1 |

---

### **32. Find the "First Value" of a column without using FIRST_VALUE window function**

**Input (`employees`):**
| name | dept | salary |
|---|---|---|
| Low | IT | 1000 |
| High | IT | 9000 |

#### **Solution:**
```sql
SELECT DISTINCT ON (dept)       -- PostgreSQL specific: Returns the first row for each group
       dept, name, salary
FROM employees 
ORDER BY dept, salary DESC;     -- Order defines which row is "first"
```

**Output:**
| dept | name | salary |
|---|---|---|
| IT | High | 9000 |

---

### **33. Calculate YoY (Year-over-Year) growth**

**Input (`sales`):**
| yr | revenue |
|---|---|
| 2022 | 100 |
| 2023 | 150 |

#### **Solution:**
```sql
WITH YearlySales AS (
    SELECT EXTRACT(YEAR FROM sale_date) as yr, SUM(amount) as revenue
    FROM sales GROUP BY 1
)
SELECT yr, revenue,
       LAG(revenue) OVER (ORDER BY yr) as prev_yr_rev,
       ((revenue - LAG(revenue) OVER (ORDER BY yr)) / LAG(revenue) OVER (ORDER BY yr)) * 100 as growth
FROM YearlySales;
```

**Output:**
| yr | revenue | growth |
|---|---|---|
| 2023 | 150 | 50.0% |

---

### **34. Pivot data: Convert rows of (Month, Sales) to columns (Jan, Feb, ...)**

**Input (`sales`):** (Months 1 and 2)

#### **Solution:**
```sql
-- Manual Pivot using Filter/CASE (PostgreSQL approach)
SELECT 
  SUM(amount) FILTER (WHERE EXTRACT(MONTH FROM date) = 1) as Jan,
  SUM(amount) FILTER (WHERE EXTRACT(MONTH FROM date) = 2) as Feb
FROM sales;                     -- FILTER (WHERE ...) is more readable/faster than CASE
```

**Output:**
| Jan | Feb |
|---|---|
| 500 | 700 |

---

### **35. Find users who performed action A but NEVER action B**

**Input (`activity`):**
| user_id | action |
|---|---|
| 1 | A |
| 1 | B |
| 2 | A |

#### **Solution:**
```sql
SELECT user_id FROM activity WHERE action = 'A'
EXCEPT                          -- Set difference
SELECT user_id FROM activity WHERE action = 'B';
```

**Output:** 2.

---

### **36. Moving Averages: Weighted average of last 3 prices**

**Input (`stock_prices`):**
| price |
|---|
| 10 |
| 20 |
| 30 |

#### **Solution:**
```sql
SELECT date, price,
       (price*3 + LAG(price,1)*2 + LAG(price,2)*1) / 6.0 OVER (...) as weighted_avg
FROM stock_prices;
```

---

### **37. Handling dynamic column names in results (Crosstab extension)**

#### **Solution:**
```sql
-- Requires: CREATE EXTENSION tablefunc;
SELECT * FROM crosstab(         -- Specialized PIVOT function
  'SELECT name, category, value FROM source_data ORDER BY 1,2'
) AS result(name text, cat1 int, cat2 int);
```

---

### **38. Find the most recent order for every customer efficiently**

**Input (`orders`):**
| cust_id | date |
|---|---|
| 1 | 2023-01-01 |
| 1 | 2023-05-01 |

#### **Solution:**
```sql
SELECT * FROM (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) as r
    FROM orders
) as t WHERE r = 1;
```

**Output:** Order from 2023-05-01 for customer 1.

---

### **39. Use `string_agg` to create a comma-separated list of values**

**Input (`employees`):**
| dept | name |
|---|---|
| IT | Alice |
| IT | Bob |

#### **Solution:**
```sql
-- Combine names into one string per department
SELECT dept, string_agg(name, ', ' ORDER BY name) as employee_list
FROM employees GROUP BY dept;
```

**Output:**
| dept | employee_list |
|---|---|
| IT | Alice, Bob |

---

### **40. Identify the "Longest Streak" of increasing sales**

#### **Solution:**
```sql
WITH Trending AS (
    SELECT id, price,
           CASE WHEN price > LAG(price) OVER (ORDER BY id) THEN 1 ELSE 0 END as is_up
    FROM sales
)
-- Then apply Gaps and Islands logic on 'is_up' column to find max consecutive 1s.
```

---

## **Section 5: Database Internals & Management (Q41-50)**

### **41. Understanding MVCC: Why do deleted rows take up space?**

**Answer:** PostgreSQL uses Multi-Version Concurrency Control. Deleted rows (dead tuples) are only marked as dead, not removed, to avoid blocking other transactions. They are cleaned up by `VACUUM`.

---

### **42. When should you use `VACUUM FULL` vs `VACUUM`?**

- **VACUUM**: Reclaims space for reuse within the table; doesn't block reads/writes.
- **VACUUM FULL**: Compacts data and returns space to the OS; blocks EVERYTHING (exclusive lock).

---

### **43. How to find duplicate records without an ID column?**

**Input (`employees`):** (Duplicates of 'Alice')

#### **Solution:**
```sql
SELECT ctid, * FROM employees   -- 'ctid' is a hidden system column for physical row location
WHERE ctid NOT IN (
    SELECT MIN(ctid) FROM employees GROUP BY name, email
);
```

---

### **44. Difference between `TRUNCATE` and `DELETE` internals**

- **DELETE**: Row by row; generates individual WAL logs; can be rolled back; slow.
- **TRUNCATE**: Resets the data file; minimal logging; extremely fast; ignores row-level triggers.

---

### **45. Use `pg_sleep()` for testing connection timeouts**

#### **Solution:**
```sql
SELECT pg_sleep(5);             -- Pauses current session for 5 seconds
```

---

### **46. Check active connections to the database**

#### **Solution:**
```sql
SELECT pid, usename, state, query 
FROM pg_stat_activity;          -- System view for current server state
```

---

### **47. Find the size of a specific table in the database**

#### **Solution:**
```sql
SELECT pg_size_pretty(pg_total_relation_size('employees')); -- Includes indexes
```

---

### **48. Use `DISTINCT ON` to get unique items by first column**

**Input (`order_history`):** (States: Pending, then Shipped)

#### **Solution:**
```sql
-- Get latest order status for each order_id
SELECT DISTINCT ON (order_id) order_id, status, updated_at
FROM order_history
ORDER BY order_id, updated_at DESC;
```

**Output:** Latest status 'Shipped' per order_id.

---

### **49. What is a "Covering Index" (Using INCLUDE)?**

#### **Solution:**
```sql
CREATE INDEX idx_user_search ON users(username) -- Create index on search column
INCLUDE (email, status);        -- Store extra columns in leaf nodes for index-only scans
```

---

### **50. How to stop a long-running query safely?**

#### **Solution:**
```sql
SELECT pg_terminate_backend(pid) -- Stronger than pg_cancel_query
FROM pg_stat_activity 
WHERE query LIKE '%SELECT * FROM massive_table%';
```



---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
