
# Aggregations and Filters in SQL

Aggregations and filters are used to retrieve, filter and summarize data from database tables.

## 1. Aggregate Functions

Aggregate functions perform calculations on multiple rows and return a single result.

Let's use an `employees` table for examples.

| emp_id | name | department | salary |
|---|---|---|---|
| 1 | Rahul | IT | 50000 |
| 2 | Priya | HR | 40000 |
| 3 | Arjun | IT | 60000 |
| 4 | Ravi | HR | 30000 |

### COUNT()

COUNT() is used to count the number of rows or non-NULL values in a column.

```sql
SELECT COUNT(*)
FROM employees;
```

**Output:** 4

### SUM()

SUM() calculates the total of a numeric column.

```sql
SELECT SUM(salary)
FROM employees;
```

**Output:** 180000

### AVG()

AVG() calculates the average value of a numeric column.

```sql
SELECT AVG(salary)
FROM employees;
```

**Output:** 45000

### MAX()

MAX() returns the highest value in a column.

```sql
SELECT MAX(salary)
FROM employees;
```

**Output:** 60000

### MIN()

MIN() returns the lowest value in a column.

```sql
SELECT MIN(salary)
FROM employees;
```

**Output:** 30000

## 2. GROUP BY

GROUP BY is used to group rows that have the same values in a particular column.

It is commonly used with aggregate functions to calculate results for each group.

**Example:** Find the total salary paid by each department.

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

**Output:**

| department | sum |
|---|---|
| IT | 110000 |
| HR | 70000 |

Here, employees are grouped by department, and the total salary is calculated separately for each department.

## 3. HAVING

HAVING is used to filter grouped results. It is generally used with GROUP BY.

**Example:** Find departments where the total salary is greater than ₹75,000.

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department
HAVING SUM(salary) > 75000;
```

**Output:**

| department | sum |
|---|---|
| IT | 110000 |

## 4. WHERE

WHERE is used to filter individual rows based on a condition.

**Example:** Get employees whose salary is greater than ₹40,000.

```sql
SELECT *
FROM employees
WHERE salary > 40000;
```

WHERE filters rows before grouping and aggregation.

## 5. DISTINCT

DISTINCT is used to remove duplicate values from the result.

**Example:** Get all unique department names.

```sql
SELECT DISTINCT department
FROM employees;
```

**Output:**

| department |
|---|
| IT |
| HR |

## 6. ORDER BY

ORDER BY is used to sort the result in ascending or descending order.

- ASC: Lowest to highest (default).
- DESC: Highest to lowest.

**Example:** Display employees based on salary from highest to lowest.

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

## 7. LIMIT

LIMIT is used to restrict the number of rows returned by a query.

**Example:** Get the top two highest-paid employees.

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 2;
```

## 8. Common SQL Filtering Operators

### Comparison Operators

| Operator | Meaning |
|---|---|
| = | Equal to |
| != or <> | Not equal to |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |

**Example:**

```sql
SELECT *
FROM employees
WHERE salary >= 40000;
```

### AND

AND returns rows only when all given conditions are true.

```sql
SELECT *
FROM employees
WHERE department = 'IT' AND salary > 50000;
```

### OR

OR returns rows when at least one condition is true.

```sql
SELECT *
FROM employees
WHERE department = 'IT' OR department = 'HR';
```

### IN

IN checks whether a value matches any value in a given list.

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR');
```

### BETWEEN

BETWEEN checks whether a value falls within a given range, including both boundaries.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 30000 AND 50000;
```

### LIKE

LIKE is used to search for a particular pattern in a string.

- `%` matches zero or more characters.
- `_` matches exactly one character.

```sql
SELECT *
FROM employees
WHERE name LIKE 'R%';
```

This returns names starting with R.

### IS NULL

IS NULL checks whether a column contains NULL values.

```sql
SELECT *
FROM employees
WHERE department IS NULL;
```

To get rows where a column is not NULL:

```sql
SELECT *
FROM employees
WHERE department IS NOT NULL;
```

## 9. Difference Between WHERE and HAVING

| WHERE | HAVING |
|---|---|
| Filters individual rows. | Filters grouped results. |
| Applied before GROUP BY. | Applied after GROUP BY. |
| Commonly used with conditions on columns. | Commonly used with aggregate functions. |

**Example using both:**

```sql
SELECT department, AVG(salary)
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 45000;
```

Here:
1. WHERE removes employees whose salary is ₹30,000 or less.
2. GROUP BY groups the remaining employees by department.
3. AVG calculates the average salary for each department.
4. HAVING keeps only departments with an average salary greater than ₹45,000.
