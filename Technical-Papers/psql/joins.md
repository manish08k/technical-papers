
# SQL Joins

Joins are used to combine data from two or more tables based on a related column between them.

For example, suppose we have two tables: `employees` and `departments`.

**Employees table**

| emp_id | name | dept_id |
|---|---|---|
| 1 | Rahul | 101 |
| 2 | Priya | 102 |
| 3 | Arjun | 103 |
| 4 | Ravi | NULL |

**Departments table**

| dept_id | dept_name |
|---|---|
| 101 | IT |
| 102 | HR |
| 104 | Finance |

## 1. INNER JOIN

INNER JOIN returns only the rows that have matching values in both tables.

**Example:**

```sql
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```

**Output:**

| name | dept_name |
|---|---|
| Rahul | IT |
| Priya | HR |

Arjun is not included because department 103 does not exist in the departments table. Ravi is also excluded because his department ID is NULL.

## 2. LEFT JOIN

LEFT JOIN returns all rows from the left table and matching rows from the right table. If there is no match, the right table columns contain NULL.

**Example:**

```sql
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;
```

**Output:**

| name | dept_name |
|---|---|
| Rahul | IT |
| Priya | HR |
| Arjun | NULL |
| Ravi | NULL |

Here, all employees are included, even if they don't belong to a matching department.

## 3. RIGHT JOIN

RIGHT JOIN returns all rows from the right table and matching rows from the left table. If there is no match, the left table columns contain NULL.

**Example:**

```sql
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d
ON e.dept_id = d.dept_id;
```

**Output:**

| name | dept_name |
|---|---|
| Rahul | IT |
| Priya | HR |
| NULL | Finance |

Finance is included even though no employee belongs to that department.

## 4. FULL OUTER JOIN

FULL OUTER JOIN returns all rows from both tables. Matching rows are combined, and unmatched rows contain NULL for the missing side.

**Example:**

```sql
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d
ON e.dept_id = d.dept_id;
```

**Output:**

| name | dept_name |
|---|---|
| Rahul | IT |
| Priya | HR |
| Arjun | NULL |
| Ravi | NULL |
| NULL | Finance |

It includes matching and non-matching records from both tables.

## 5. CROSS JOIN

CROSS JOIN returns every possible combination of rows from both tables.

If the first table has 4 rows and the second table has 3 rows, the result will contain 12 rows.

**Example:**

```sql
SELECT e.name, d.dept_name
FROM employees e
CROSS JOIN departments d;
```

Each employee will be combined with every department.

## 6. SELF JOIN

A SELF JOIN is used when we need to join a table with itself. It is useful when rows in the same table are related to each other.

**Example:**

Suppose an employees table contains employee details and their manager IDs.

| emp_id | name | manager_id |
|---|---|---|
| 1 | Rahul | NULL |
| 2 | Priya | 1 |
| 3 | Arjun | 1 |
| 4 | Ravi | 2 |

To display employees along with their manager names:

```sql
SELECT 
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

Here, the same table is used twice with different aliases (`e` and `m`) to get employee and manager details.
