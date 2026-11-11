
# Indexes in DBMS

An index is used to retrieve data faster from a database. Instead of checking every row in a table, the database uses an index to find the required records more efficiently.

It works like an index in a book. Instead of reading every page to find a topic, we use the index to locate it quickly.

## 1. Why do we need Indexes?

Suppose an employees table has 1 lakh records, and we want to find an employee with ID 500.

Without an index, the database may need to scan the entire table to find the record.

With an index, it can locate the record much faster.

**Example:**

```sql
SELECT *
FROM employees
WHERE emp_id = 500;
```

## 2. Creating an Index

We use `CREATE INDEX` to create an index on a column.

```sql
CREATE INDEX idx_emp_name
ON employees(name);
```

Now searching employees by name can be faster.

## 3. Types of Indexes

### Primary Index

A primary key automatically creates a unique index in databases like PostgreSQL.

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

### Unique Index

A unique index prevents duplicate values in the indexed column.

```sql
CREATE UNIQUE INDEX idx_email
ON employees(email);
```

### Composite Index

A composite index is created on two or more columns.

```sql
CREATE INDEX idx_dept_salary
ON employees(department, salary);
```

The order of columns matters.

For an index on `(department, salary)`:

- Queries filtering by `department` can use the index.
- Queries filtering by both `department` and `salary` can use the index.
- Queries filtering only by `salary` generally cannot use the index as efficiently.

### Clustered Index

A clustered index organizes table records according to the indexed key. The implementation depends on the database.

### Non-Clustered Index

A non-clustered index stores index information separately from the actual table data and keeps references to the corresponding rows.

## 4. Dropping an Index

We use `DROP INDEX` to remove an index.

```sql
DROP INDEX idx_emp_name;
```

This removes the index but does not delete the table data.
