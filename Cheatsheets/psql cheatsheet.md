
> **Two command types**
>
> - **SQL statements** are sent to PostgreSQL and normally end with `;`.
> - **psql meta-commands** are interpreted by the `psql` terminal, begin with `\`, and normally do not end with `;`.
>
> Examples below use `company`, `employees`, and `departments`. Replace names and file paths with your own.

---

## 1. Start, connect, and exit

Run these in your macOS/Linux shell, not inside the `psql` prompt:

| Command | What it does |
|---|---|
| `psql --version` | Shows the installed client version |
| `psql -U postgres` | Connects as role `postgres` |
| `psql -U postgres -d company` | Connects to database `company` |
| `psql -h localhost -p 5432 -U postgres -d company` | Connects using host, port, role, and database |
| `psql -d "postgresql://user:password@localhost:5432/company"` | Connects using a connection URI |
| `createdb -U postgres company` | Creates a database from the shell |
| `dropdb -U postgres company` | Drops a database from the shell |
| `pg_isready` | Checks whether a PostgreSQL server is accepting connections |

Inside `psql`:

```text
\q
```

Quit `psql`.

**Prompt clues**

- `name=#` or `name=>`: ready for a command.
- `name-#`: PostgreSQL is waiting for the rest of a statement, often because a semicolon is missing.
- `name'#`: a quoted string has not been closed.
- `name=#` with `*` in the prompt: inside a transaction block.

To cancel the current incomplete command, press `Ctrl+C`.

---

## 2. Essential psql meta-commands

These are `psql` commands, not SQL statements.

| Command | Purpose |
|---|---|
| `\?` | Help for psql meta-commands |
| `\h` | Help for SQL syntax |
| `\h SELECT` | Help for a specific SQL command |
| `\l` or `\list` | List databases |
| `\c company` | Connect to a database |
| `\conninfo` | Show current connection details |
| `\du` | List roles/users |
| `\dn` | List schemas |
| `\dt` | List tables in the current search path |
| `\dt *.*` | List tables across schemas |
| `\d table_name` | Describe a table, view, or other relation |
| `\d+ table_name` | Detailed relation description |
| `\di` | List indexes |
| `\dv` | List views |
| `\dm` | List materialized views |
| `\ds` | List sequences |
| `\df` | List functions |
| `\dp` | Show table/view access privileges |
| `\dx` | List installed extensions |
| `\! clear` | Run the shell's clear command |
| `\s` | Show command history |
| `\e` | Edit the current query in an editor |
| `\p` | Show the current query buffer |
| `\r` | Reset/clear the query buffer |
| `\g` | Execute the query buffer |
| `\g filename` | Execute query and write output to a file |
| `\o filename` | Send subsequent query output to a file |
| `\o` | Return output to the terminal |
| `\timing` | Toggle query execution timing |
| `\x` | Toggle expanded display |
| `\pset` | Configure output formatting |
| `\q` | Quit psql |

### Useful psql variations

```text
\c company postgres
\dt public.*
\d public.employees
\dt+ public.*
\pset pager off
\pset null '(null)'
\pset border 2
\x auto
\timing on
```

- `\c company postgres` connects to database `company` as role `postgres`.
- `\dt public.*` lists tables in the `public` schema.
- `\pset pager off` prevents output from opening in a pager.
- `\pset null '(null)'` changes how NULL values are displayed.
- `\x auto` lets psql choose expanded display when useful.
- `\timing on` displays execution time after queries.

### Run SQL files and shell commands

```text
\i /absolute/path/to/script.sql
\ir relative/path/to/script.sql
\! ls
\! pwd
```

- `\i` runs a SQL file using the given path.
- `\ir` runs a SQL file relative to the location of the current script.
- `\!` executes a shell command from inside `psql`.

---

## 3. Create, inspect, connect to, and delete databases

```sql
CREATE DATABASE company;

-- Connect using psql, not SQL:
-- \c company

-- List databases in psql:
-- \l

ALTER DATABASE company RENAME TO company_db;

ALTER DATABASE company_db OWNER TO postgres;

DROP DATABASE company_db;

DROP DATABASE IF EXISTS company_db;
```

**Important:** `CREATE DATABASE` and `DROP DATABASE` cannot run inside a transaction block. You cannot drop the database to which you are currently connected. Connect to another database first.

PostgreSQL does not support `CREATE DATABASE IF NOT EXISTS` as a direct SQL clause. Check `\l` first, or use a shell/script that checks before creating it.

---

## 4. Schemas and search path

A schema is a namespace inside a database. It groups tables, views, functions, and other objects.

```sql
CREATE SCHEMA sales;

CREATE SCHEMA IF NOT EXISTS analytics;

SELECT schema_name
FROM information_schema.schemata;

SHOW search_path;

SET search_path TO sales, public;

ALTER SCHEMA sales RENAME TO sales_data;

ALTER SCHEMA sales_data OWNER TO postgres;

DROP SCHEMA sales_data;

DROP SCHEMA IF EXISTS sales_data CASCADE;
```

Use a schema-qualified name to identify an object explicitly:

```sql
SELECT * FROM public.employees;
```

`CASCADE` also drops dependent objects. Use it carefully.

---

## 5. Create tables and choose data types

```sql
CREATE TABLE employees (
    employee_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50),
    email VARCHAR(150) UNIQUE,
    age INT CHECK (age >= 18),
    salary NUMERIC(12, 2) DEFAULT 0,
    department_id INT,
    hired_at DATE DEFAULT CURRENT_DATE,
    is_active BOOLEAN DEFAULT TRUE
);
```

### Common PostgreSQL data types

| Type | Use |
|---|---|
| `SMALLINT` | Small whole numbers |
| `INTEGER` / `INT` | Whole numbers |
| `BIGINT` | Large whole numbers |
| `NUMERIC(p,s)` / `DECIMAL(p,s)` | Exact decimal values, useful for money |
| `REAL` | 4-byte approximate floating point |
| `DOUBLE PRECISION` | 8-byte approximate floating point |
| `SERIAL` / `BIGSERIAL` | Older sequence-backed auto-increment shorthand |
| `VARCHAR(n)` | Variable-length text with a limit |
| `CHAR(n)` | Fixed-length, blank-padded text |
| `TEXT` | Variable-length text without a declared limit |
| `BOOLEAN` | `TRUE`, `FALSE`, or `NULL` |
| `DATE` | Calendar date |
| `TIME` | Time of day |
| `TIMESTAMP` | Date and time without time zone |
| `TIMESTAMPTZ` | Timestamp with time zone handling |
| `INTERVAL` | Duration |
| `UUID` | Universally unique identifier |
| `JSON` | JSON text, preserving input text representation |
| `JSONB` | Decomposed JSON format, generally better for querying/indexing |
| `BYTEA` | Binary data |
| `INTEGER[]`, `TEXT[]` | Arrays |
| `TSVECTOR` | Full-text search document |
| `TSQUERY` | Full-text search query |

**Identity vs serial**

```sql
-- Recommended modern identity syntax:
id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY

-- Allows explicit values to be supplied:
id INT GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY

-- Older shorthand:
id SERIAL PRIMARY KEY
```

---

## 6. Inspect, alter, rename, truncate, and drop tables

```sql
-- psql inspection:
-- \dt
-- \d employees
-- \d+ employees

-- Add a column:
ALTER TABLE employees
ADD COLUMN phone VARCHAR(20);

-- Add a column only if it is not already present:
ALTER TABLE employees
ADD COLUMN IF NOT EXISTS city VARCHAR(80);

-- Drop a column:
ALTER TABLE employees
DROP COLUMN phone;

-- Rename a column:
ALTER TABLE employees
RENAME COLUMN first_name TO given_name;

-- Change a data type:
ALTER TABLE employees
ALTER COLUMN salary TYPE NUMERIC(14, 2);

-- Set or remove a default:
ALTER TABLE employees
ALTER COLUMN salary SET DEFAULT 10000;

ALTER TABLE employees
ALTER COLUMN salary DROP DEFAULT;

-- Set or remove NOT NULL:
ALTER TABLE employees
ALTER COLUMN given_name SET NOT NULL;

ALTER TABLE employees
ALTER COLUMN given_name DROP NOT NULL;

-- Rename a table:
ALTER TABLE employees RENAME TO staff;

-- Change table owner:
ALTER TABLE staff OWNER TO postgres;

-- Remove all rows but keep the table:
TRUNCATE TABLE staff;

-- Remove a table:
DROP TABLE staff;

DROP TABLE IF EXISTS staff;
```

`TRUNCATE` removes all rows and is usually faster than deleting every row individually. It does not remove the table definition.

---

## 7. Constraints

| Constraint | Meaning |
|---|---|
| `NOT NULL` | A column must have a value |
| `UNIQUE` | Values must be unique |
| `PRIMARY KEY` | Unique row identifier; implies `UNIQUE` and `NOT NULL` |
| `FOREIGN KEY` | Enforces a reference to another table |
| `CHECK` | Requires a Boolean condition to be true or NULL |
| `DEFAULT` | Supplies a value when one is not provided |

### Primary key and foreign key example

```sql
CREATE TABLE departments (
    department_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE employees (
    employee_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    salary NUMERIC(12, 2) CHECK (salary >= 0),
    department_id INT,
    CONSTRAINT fk_employee_department
        FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
```

### Add and remove constraints

```sql
ALTER TABLE employees
ADD CONSTRAINT employees_salary_check CHECK (salary >= 0);

ALTER TABLE employees
ADD CONSTRAINT employees_email_unique UNIQUE (email);

ALTER TABLE employees
ADD CONSTRAINT employees_department_fk
FOREIGN KEY (department_id)
REFERENCES departments(department_id);

ALTER TABLE employees
DROP CONSTRAINT employees_salary_check;
```

### Foreign-key actions

- `ON DELETE CASCADE`: delete referencing rows when the referenced row is deleted.
- `ON DELETE SET NULL`: set the referencing foreign-key column to NULL.
- `ON DELETE SET DEFAULT`: set it to its default value.
- `ON DELETE RESTRICT`: prevent deletion when references exist.
- `ON DELETE NO ACTION`: check the constraint at its normal check time; this is the default.

The same action options are available for `ON UPDATE`.

---

## 8. INSERT data

```sql
-- Insert one row:
INSERT INTO employees (first_name, last_name, email, salary)
VALUES ('Manish', 'Nalumachu', 'manish@example.com', 50000);

-- Insert multiple rows:
INSERT INTO employees (first_name, salary)
VALUES
    ('Asha', 45000),
    ('Rahul', 55000),
    ('Kiran', 60000);

-- Insert using DEFAULT:
INSERT INTO employees (first_name, salary)
VALUES ('Ravi', DEFAULT);

-- Insert rows from another query:
INSERT INTO employees_backup (employee_id, first_name, salary)
SELECT employee_id, first_name, salary
FROM employees;

-- Return inserted values:
INSERT INTO employees (first_name, salary)
VALUES ('Arjun', 40000)
RETURNING employee_id, first_name, salary;

-- Insert or update when a unique/primary-key conflict occurs:
INSERT INTO employees (employee_id, first_name, salary)
VALUES (1, 'Manish', 65000)
ON CONFLICT (employee_id)
DO UPDATE SET
    first_name = EXCLUDED.first_name,
    salary = EXCLUDED.salary;

-- Ignore a conflict:
INSERT INTO employees (employee_id, first_name)
VALUES (1, 'Manish')
ON CONFLICT (employee_id) DO NOTHING;
```

`EXCLUDED.column_name` refers to the value proposed by the `INSERT` statement.

---

## 9. SELECT data

```sql
-- All columns:
SELECT * FROM employees;

-- Selected columns:
SELECT first_name, salary
FROM employees;

-- Give output columns aliases:
SELECT first_name AS employee_name,
       salary AS monthly_salary
FROM employees;

-- Calculated column:
SELECT first_name, salary, salary * 12 AS annual_salary
FROM employees;

-- Unique values:
SELECT DISTINCT department_id
FROM employees;

-- Distinct combinations:
SELECT DISTINCT department_id, age
FROM employees;

-- Limit rows:
SELECT * FROM employees LIMIT 10;

-- Skip rows:
SELECT * FROM employees OFFSET 10;

-- Pagination (always use a deterministic ORDER BY):
SELECT *
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 20;
```

### SELECT clause order

```sql
SELECT [DISTINCT] columns
FROM table
[JOIN another_table ON condition]
[WHERE condition]
[GROUP BY columns]
[HAVING group_condition]
[ORDER BY columns]
[LIMIT number]
[OFFSET number];
```

---

## 10. WHERE conditions and operators

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `<>` or `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |
| `AND` | Both conditions must match |
| `OR` | At least one condition must match |
| `NOT` | Negates a condition |
| `BETWEEN a AND b` | Inclusive range |
| `IN (...)` | Matches any value in a list |
| `NOT IN (...)` | Does not match values in a list |
| `LIKE` | Case-sensitive pattern match |
| `ILIKE` | Case-insensitive pattern match |
| `IS NULL` | Tests for NULL |
| `IS NOT NULL` | Tests for non-NULL |
| `EXISTS` | Tests whether a subquery returns rows |
| `ANY` / `SOME` | Compares with at least one value from a set |
| `ALL` | Compares with every value from a set |

```sql
SELECT * FROM employees WHERE salary > 50000;

SELECT * FROM employees WHERE age >= 21 AND is_active = TRUE;

SELECT * FROM employees WHERE department_id = 2 OR department_id = 3;

SELECT * FROM employees WHERE salary BETWEEN 30000 AND 60000;

SELECT * FROM employees WHERE department_id IN (1, 2, 3);

SELECT * FROM employees WHERE department_id NOT IN (1, 2);

SELECT * FROM employees WHERE first_name LIKE 'M%';

SELECT * FROM employees WHERE first_name ILIKE '%an%';

SELECT * FROM employees WHERE email IS NULL;

SELECT * FROM employees WHERE email IS NOT NULL;
```

**LIKE wildcards**

- `%` matches zero or more characters: `'M%'`, `'%an%'`.
- `_` matches exactly one character: `'M_n'`.

**NULL warning:** Do not write `column = NULL` or `column <> NULL`. Use `IS NULL` or `IS NOT NULL`. `NOT IN` can produce surprising results if its list/subquery contains NULL; `NOT EXISTS` is often safer.

---

## 11. ORDER BY, LIMIT, and OFFSET

```sql
-- Ascending:
SELECT * FROM employees ORDER BY salary ASC;

-- Descending:
SELECT * FROM employees ORDER BY salary DESC;

-- Multiple sort keys:
SELECT * FROM employees
ORDER BY department_id ASC, salary DESC;

-- NULL placement:
SELECT * FROM employees ORDER BY email ASC NULLS LAST;

-- Top five:
SELECT * FROM employees ORDER BY salary DESC LIMIT 5;

-- Skip the first ten:
SELECT * FROM employees ORDER BY employee_id LIMIT 10 OFFSET 10;
```

`ASC` is ascending and is the default. `DESC` is descending. PostgreSQL's default NULL placement is `NULLS LAST` for ascending and `NULLS FIRST` for descending.

---

## 12. UPDATE and DELETE

```sql
-- Update one row:
UPDATE employees
SET salary = 60000
WHERE employee_id = 1;

-- Update multiple columns:
UPDATE employees
SET salary = 65000,
    is_active = TRUE
WHERE employee_id = 1;

-- Update using an expression:
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = 2;

-- Update and return changed rows:
UPDATE employees
SET salary = salary + 1000
WHERE department_id = 2
RETURNING *;

-- Delete selected rows:
DELETE FROM employees
WHERE employee_id = 1;

-- Delete and return deleted rows:
DELETE FROM employees
WHERE is_active = FALSE
RETURNING *;

-- Delete all rows:
DELETE FROM employees;
```

**Always check the `WHERE` clause before running `UPDATE` or `DELETE`.** Without `WHERE`, every row is affected.

---

## 13. Aggregate functions

| Function | Purpose |
|---|---|
| `COUNT(*)` | Counts rows |
| `COUNT(column)` | Counts non-NULL values in a column |
| `COUNT(DISTINCT column)` | Counts distinct non-NULL values |
| `SUM(column)` | Adds non-NULL values |
| `AVG(column)` | Average of non-NULL values |
| `MIN(column)` | Smallest value |
| `MAX(column)` | Largest value |
| `STRING_AGG(value, delimiter)` | Joins values into a string |
| `ARRAY_AGG(value)` | Collects values into an array |
| `BOOL_AND(value)` | True if all non-NULL inputs are true |
| `BOOL_OR(value)` | True if any non-NULL input is true |

```sql
SELECT COUNT(*) FROM employees;

SELECT COUNT(email) FROM employees;

SELECT COUNT(DISTINCT department_id) FROM employees;

SELECT SUM(salary), AVG(salary), MIN(salary), MAX(salary)
FROM employees;

SELECT department_id, STRING_AGG(first_name, ', ')
FROM employees
GROUP BY department_id;
```

---

## 14. GROUP BY and HAVING

`GROUP BY` makes groups of rows. `HAVING` filters those groups after aggregation.

```sql
-- Count employees in each department:
SELECT department_id, COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;

-- Average salary per department:
SELECT department_id, AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;

-- Keep only groups with more than five employees:
SELECT department_id, COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;

-- Group by more than one column:
SELECT department_id, is_active, COUNT(*)
FROM employees
GROUP BY department_id, is_active;
```

---

## 15. JOINs

Assume `employees.department_id` references `departments.department_id`.

### INNER JOIN

Only rows with matching values in both tables.

```sql
SELECT e.first_name, d.department_name
FROM employees AS e
INNER JOIN departments AS d
    ON e.department_id = d.department_id;
```

### LEFT JOIN / LEFT OUTER JOIN

All rows from the left table, plus matching rows from the right table. Unmatched right-side columns are NULL.

```sql
SELECT e.first_name, d.department_name
FROM employees AS e
LEFT JOIN departments AS d
    ON e.department_id = d.department_id;
```

### RIGHT JOIN / RIGHT OUTER JOIN

All rows from the right table, plus matching rows from the left table.

```sql
SELECT e.first_name, d.department_name
FROM employees AS e
RIGHT JOIN departments AS d
    ON e.department_id = d.department_id;
```

### FULL JOIN / FULL OUTER JOIN

All rows from both tables; unmatched columns are NULL.

```sql
SELECT e.first_name, d.department_name
FROM employees AS e
FULL OUTER JOIN departments AS d
    ON e.department_id = d.department_id;
```

### CROSS JOIN

Every row from the first table paired with every row from the second table.

```sql
SELECT e.first_name, d.department_name
FROM employees AS e
CROSS JOIN departments AS d;
```

### SELF JOIN

Join a table to itself, for example employee-to-manager.

```sql
SELECT e.first_name AS employee,
       m.first_name AS manager
FROM employees AS e
LEFT JOIN employees AS m
    ON e.manager_id = m.employee_id;
```

### NATURAL JOIN

Automatically joins columns with the same names. It can become unsafe if table structures change; explicit `JOIN ... ON` is usually clearer.

```sql
SELECT *
FROM employees
NATURAL JOIN departments;
```

### Join reminders

- `ON` specifies how rows match.
- `USING (column_name)` can be used when both tables share the same join-column name.
- Use table aliases (`e`, `d`) to make queries shorter.
- A condition on the right-side table in `WHERE` can remove NULL-extended rows and make a `LEFT JOIN` behave like an inner join. If you need to preserve unmatched left rows, consider placing that condition in the `ON` clause.

---

## 16. Subqueries

A subquery is a query nested inside another query.

```sql
-- Employees earning more than the overall average:
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

-- Highest salary:
SELECT MAX(salary)
FROM employees;

-- Second-highest distinct salary:
SELECT MAX(salary)
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);

-- Rows whose department exists in departments:
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
);

-- Departments that have at least one employee:
SELECT *
FROM departments AS d
WHERE EXISTS (
    SELECT 1
    FROM employees AS e
    WHERE e.department_id = d.department_id
);

-- Departments with no employees:
SELECT *
FROM departments AS d
WHERE NOT EXISTS (
    SELECT 1
    FROM employees AS e
    WHERE e.department_id = d.department_id
);

-- Compare against every value returned:
SELECT *
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE department_id = 2
);
```

A scalar subquery must return at most one row. `IN`, `EXISTS`, `ANY`, and `ALL` are useful for multi-row subqueries.

---

## 17. CTEs (WITH queries)

A Common Table Expression gives a query result a name for use within one statement.

```sql
WITH high_paid AS (
    SELECT *
    FROM employees
    WHERE salary > 50000
)
SELECT *
FROM high_paid;
```

### Multiple CTEs

```sql
WITH department_counts AS (
    SELECT department_id, COUNT(*) AS total
    FROM employees
    GROUP BY department_id
),
large_departments AS (
    SELECT *
    FROM department_counts
    WHERE total > 5
)
SELECT *
FROM large_departments;
```

### Recursive CTE

Useful for hierarchies and tree-like data.

```sql
WITH RECURSIVE numbers(n) AS (
    SELECT 1
    UNION ALL
    SELECT n + 1
    FROM numbers
    WHERE n < 10
)
SELECT *
FROM numbers;
```

---

## 18. Window functions

Window functions calculate values across related rows without collapsing the rows into one result per group.

| Function | Purpose |
|---|---|
| `ROW_NUMBER()` | Unique sequential number |
| `RANK()` | Ranking with gaps after ties |
| `DENSE_RANK()` | Ranking without gaps after ties |
| `NTILE(n)` | Divides ordered rows into n buckets |
| `LAG()` | Reads a preceding row's value |
| `LEAD()` | Reads a following row's value |
| `FIRST_VALUE()` | First value in the window frame |
| `LAST_VALUE()` | Last value in the window frame |
| `NTH_VALUE()` | Nth value in the window frame |
| `SUM() OVER (...)` | Running/windowed sum |
| `AVG() OVER (...)` | Windowed average |
| `COUNT() OVER (...)` | Windowed count |

### ROW_NUMBER, RANK, and DENSE_RANK

```sql
SELECT first_name, salary,
       ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num,
       RANK() OVER (ORDER BY salary DESC) AS salary_rank,
       DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_salary_rank
FROM employees;
```

If salaries are `90000, 80000, 80000, 70000`:

- `ROW_NUMBER`: `1, 2, 3, 4`
- `RANK`: `1, 2, 2, 4`
- `DENSE_RANK`: `1, 2, 2, 3`

### PARTITION BY

Ranks employees separately within each department.

```sql
SELECT first_name, department_id, salary,
       DENSE_RANK() OVER (
           PARTITION BY department_id
           ORDER BY salary DESC
       ) AS department_rank
FROM employees;
```

### LAG and LEAD

```sql
SELECT first_name, salary,
       LAG(salary) OVER (ORDER BY employee_id) AS previous_salary,
       LEAD(salary) OVER (ORDER BY employee_id) AS next_salary
FROM employees;
```

### Running total

```sql
SELECT employee_id, salary,
       SUM(salary) OVER (
           ORDER BY employee_id
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS running_total
FROM employees;
```

### Window frame reminder

`PARTITION BY` divides rows into groups. `ORDER BY` defines their order. The frame clause defines which rows are included for frame-sensitive functions. For `LAST_VALUE`, specify an appropriate frame when you want the last value of the entire partition:

```sql
LAST_VALUE(salary) OVER (
    PARTITION BY department_id
    ORDER BY salary
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
)
```

---

## 19. String functions and operators

| Function/operator | Purpose |
|---|---|
| `LOWER(text)` | Lowercase |
| `UPPER(text)` | Uppercase |
| `INITCAP(text)` | Capitalize words |
| `LENGTH(text)` | Character length |
| `CHAR_LENGTH(text)` | Character length |
| `OCTET_LENGTH(text)` | Byte length |
| `TRIM(text)` | Remove surrounding spaces/characters |
| `LTRIM(text)` | Remove leading characters |
| `RTRIM(text)` | Remove trailing characters |
| `BTRIM(text)` | Trim both ends |
| `REPLACE(text, from, to)` | Replace occurrences |
| `CONCAT(a, b, ...)` | Concatenate values |
| `CONCAT_WS(sep, ...)` | Concatenate using a separator |
| `SUBSTRING(text FROM start FOR count)` | Extract part of text |
| `LEFT(text, n)` | First n characters |
| `RIGHT(text, n)` | Last n characters |
| `POSITION(sub IN text)` | Find substring position |
| `STRPOS(text, sub)` | Find substring position |
| `REVERSE(text)` | Reverse text |
| `SPLIT_PART(text, delimiter, n)` | Get nth delimited part |
| `STRING_AGG(value, delimiter)` | Aggregate strings |
| `text || text` | Concatenate strings |

```sql
SELECT UPPER(first_name) FROM employees;
SELECT LOWER(first_name) FROM employees;
SELECT LENGTH(first_name) FROM employees;
SELECT TRIM(first_name) FROM employees;
SELECT REPLACE(first_name, 'a', 'x') FROM employees;
SELECT CONCAT(first_name, ' ', last_name) FROM employees;
SELECT CONCAT_WS(' ', first_name, last_name) FROM employees;
SELECT SUBSTRING(first_name FROM 1 FOR 3) FROM employees;
SELECT LEFT(first_name, 2), RIGHT(first_name, 2) FROM employees;
SELECT POSITION('a' IN first_name) FROM employees;
SELECT SPLIT_PART('one-two-three', '-', 2);
SELECT first_name || ' ' || last_name FROM employees;
```

---

## 20. Date and time functions

| Function/value | Purpose |
|---|---|
| `CURRENT_DATE` | Current date |
| `CURRENT_TIME` | Current time |
| `CURRENT_TIMESTAMP` | Current timestamp with time zone |
| `NOW()` | Transaction-start timestamp |
| `LOCALTIME` | Current time without time zone |
| `LOCALTIMESTAMP` | Current timestamp without time zone |
| `EXTRACT(field FROM value)` | Extract a date/time field |
| `DATE_PART(field, value)` | Extract a date/time field |
| `DATE_TRUNC(field, value)` | Truncate to a unit |
| `AGE(end, start)` | Calculate an interval |
| `TO_CHAR(value, format)` | Format date/time or number |
| `TO_DATE(text, format)` | Parse text as date |
| `TO_TIMESTAMP(text, format)` | Parse text as timestamp |
| `MAKE_DATE(y, m, d)` | Construct a date |
| `MAKE_INTERVAL(...)` | Construct an interval |

```sql
SELECT NOW();
SELECT CURRENT_DATE;
SELECT CURRENT_TIME;
SELECT CURRENT_TIMESTAMP;

SELECT EXTRACT(YEAR FROM CURRENT_DATE);
SELECT EXTRACT(MONTH FROM CURRENT_DATE);
SELECT DATE_PART('day', CURRENT_DATE);

SELECT DATE_TRUNC('month', NOW());
SELECT AGE(DATE '2026-11-10', DATE '2004-05-10');

SELECT CURRENT_DATE + INTERVAL '7 days';
SELECT CURRENT_DATE - INTERVAL '1 month';

SELECT TO_CHAR(NOW(), 'DD-MM-YYYY HH24:MI:SS');
SELECT TO_DATE('10-11-2026', 'DD-MM-YYYY');
SELECT MAKE_DATE(2026, 11, 10);
```

Common format patterns:

- `YYYY`: four-digit year
- `MM`: month
- `DD`: day
- `HH24`: hour from 00 to 23
- `MI`: minute
- `SS`: second
- `Day`: day name

**Time-zone commands**

```sql
SHOW TIME ZONE;

SET TIME ZONE 'Asia/Kolkata';

SELECT CURRENT_TIMESTAMP;
```

`TIMESTAMPTZ` stores an instant and displays it using the session time zone; it does not preserve the original named time zone supplied by the user.

---

## 21. Numeric and mathematical functions

| Function | Purpose |
|---|---|
| `ABS(n)` | Absolute value |
| `ROUND(n, digits)` | Round |
| `CEIL(n)` / `CEILING(n)` | Round upward |
| `FLOOR(n)` | Round downward |
| `TRUNC(n, digits)` | Truncate |
| `POWER(a, b)` | Exponent |
| `SQRT(n)` | Square root |
| `MOD(a, b)` | Remainder |
| `DIV(a, b)` | Integer quotient |
| `SIGN(n)` | Sign of number |
| `RANDOM()` | Random number from 0 to less than 1 |
| `GREATEST(a, b, ...)` | Greatest argument |
| `LEAST(a, b, ...)` | Least argument |
| `PI()` | Pi constant |

```sql
SELECT ABS(-20);
SELECT ROUND(25.678, 2);
SELECT CEIL(4.2);
SELECT FLOOR(4.9);
SELECT TRUNC(25.678, 2);
SELECT POWER(2, 3);
SELECT SQRT(25);
SELECT MOD(10, 3);
SELECT GREATEST(10, 20, 30);
SELECT LEAST(10, 20, 30);
SELECT RANDOM();
```

---

## 22. Conditional expressions and NULL handling

### CASE

```sql
SELECT first_name, salary,
       CASE
           WHEN salary >= 60000 THEN 'High'
           WHEN salary >= 40000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_level
FROM employees;
```

### COALESCE

Returns the first non-NULL argument.

```sql
SELECT COALESCE(email, 'No email')
FROM employees;
```

### NULLIF

Returns NULL if its two arguments are equal.

```sql
SELECT NULLIF(10, 10);
```

### GREATEST and LEAST

```sql
SELECT GREATEST(10, 20, 30);
SELECT LEAST(10, 20, 30);
```

### CAST

```sql
SELECT CAST('123' AS INTEGER);
SELECT '123'::INTEGER;
```

### Boolean tests

```sql
SELECT *
FROM employees
WHERE is_active IS TRUE;

SELECT *
FROM employees
WHERE is_active IS FALSE;

SELECT *
FROM employees
WHERE is_active IS UNKNOWN;
```

---

## 23. Set operations

The queries combined by set operators must return the same number of columns with compatible data types.

```sql
-- Combine and remove duplicates:
SELECT first_name FROM employees
UNION
SELECT first_name FROM contractors;

-- Combine and keep duplicates:
SELECT first_name FROM employees
UNION ALL
SELECT first_name FROM contractors;

-- Rows common to both:
SELECT first_name FROM employees
INTERSECT
SELECT first_name FROM contractors;

-- Rows in the first query but not the second:
SELECT first_name FROM employees
EXCEPT
SELECT first_name FROM contractors;
```

| Operator | Result |
|---|---|
| `UNION` | Combines and removes duplicates |
| `UNION ALL` | Combines and keeps duplicates |
| `INTERSECT` | Keeps common rows |
| `EXCEPT` | Keeps rows from the first query not in the second |

---

## 24. Indexes

Indexes can speed up data retrieval, but use extra storage and can slow down writes. PostgreSQL creates indexes automatically for primary-key and unique constraints.

```sql
-- Standard B-tree index (the default):
CREATE INDEX idx_employees_name
ON employees (first_name);

-- Unique index:
CREATE UNIQUE INDEX idx_employees_email
ON employees (email);

-- Multi-column index:
CREATE INDEX idx_employees_department_salary
ON employees (department_id, salary);

-- Partial index:
CREATE INDEX idx_active_employees
ON employees (department_id)
WHERE is_active = TRUE;

-- Expression index:
CREATE INDEX idx_lower_email
ON employees (LOWER(email));

-- Drop index:
DROP INDEX idx_employees_name;

-- psql index listing:
-- \di
```

### Index methods

| Method | Typical use |
|---|---|
| B-tree | Equality, ranges, sorting; default |
| Hash | Equality comparisons |
| GIN | Composite values such as JSONB, arrays, and full-text search |
| GiST | Geometric data, ranges, and specialized operators |
| BRIN | Very large tables where values correlate with physical row order |

### Examine query plans

```sql
EXPLAIN
SELECT *
FROM employees
WHERE department_id = 2;

EXPLAIN ANALYZE
SELECT *
FROM employees
WHERE department_id = 2;

EXPLAIN (ANALYZE, BUFFERS)
SELECT *
FROM employees
WHERE department_id = 2;
```

`EXPLAIN` shows the planned execution. `EXPLAIN ANALYZE` actually executes the query and reports measured execution details.

---

## 25. Views and materialized views

A normal view stores a query definition, not a separate copy of its result.

```sql
CREATE VIEW active_employees AS
SELECT *
FROM employees
WHERE is_active = TRUE;

SELECT * FROM active_employees;

CREATE OR REPLACE VIEW active_employees AS
SELECT employee_id, first_name, salary
FROM employees
WHERE is_active = TRUE;

DROP VIEW active_employees;
```

A materialized view stores query results and must be refreshed to reflect later changes.

```sql
CREATE MATERIALIZED VIEW department_salary AS
SELECT department_id, AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;

REFRESH MATERIALIZED VIEW department_salary;

DROP MATERIALIZED VIEW department_salary;
```

---

## 26. Sequences and generated IDs

```sql
CREATE SEQUENCE employee_number_seq;

SELECT nextval('employee_number_seq');

SELECT currval('employee_number_seq');

SELECT last_value FROM employee_number_seq;

ALTER SEQUENCE employee_number_seq RESTART WITH 1;

DROP SEQUENCE employee_number_seq;
```

- `nextval()` advances the sequence and returns a value.
- `currval()` returns the value most recently obtained from that sequence in the current session.
- `setval()` sets the sequence value.

```sql
SELECT setval('employee_number_seq', 100);
SELECT setval('employee_number_seq', 100, TRUE);
SELECT setval('employee_number_seq', 100, FALSE);
```

---

## 27. Transactions and savepoints

A transaction groups statements into one logical unit.

```sql
BEGIN;

UPDATE employees
SET salary = salary + 1000
WHERE employee_id = 1;

COMMIT;
```

Undo changes before commit:

```sql
BEGIN;

DELETE FROM employees
WHERE employee_id = 1;

ROLLBACK;
```

Savepoint:

```sql
BEGIN;

UPDATE employees
SET salary = salary + 1000
WHERE employee_id = 1;

SAVEPOINT before_delete;

DELETE FROM employees
WHERE employee_id = 2;

ROLLBACK TO SAVEPOINT before_delete;

COMMIT;
```

| Command | Purpose |
|---|---|
| `BEGIN` / `START TRANSACTION` | Start transaction |
| `COMMIT` | Make transaction changes permanent |
| `ROLLBACK` | Undo uncommitted changes |
| `SAVEPOINT name` | Create a rollback point |
| `ROLLBACK TO SAVEPOINT name` | Undo changes after a savepoint |
| `RELEASE SAVEPOINT name` | Remove a savepoint |
| `SET TRANSACTION` | Set transaction characteristics |

### Transaction isolation

```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
COMMIT;
```

Isolation levels:

- `READ COMMITTED` — PostgreSQL default.
- `REPEATABLE READ` — stable snapshot for the transaction.
- `SERIALIZABLE` — strongest isolation; transactions may need to be retried after serialization failures.

PostgreSQL accepts `READ UNCOMMITTED`, but treats it as `READ COMMITTED`.

---

## 28. Users, roles, and permissions

PostgreSQL uses roles for both users and groups. A role with `LOGIN` can connect.

```sql
-- Create login role:
CREATE ROLE app_user WITH LOGIN PASSWORD 'change_this_password';

-- Create group role:
CREATE ROLE read_only_role;

-- Grant database connection:
GRANT CONNECT ON DATABASE company TO app_user;

-- Grant schema usage:
GRANT USAGE ON SCHEMA public TO app_user;

-- Grant table permissions:
GRANT SELECT ON employees TO app_user;

-- Grant multiple permissions:
GRANT SELECT, INSERT, UPDATE ON employees TO app_user;

-- Grant all privileges on one table:
GRANT ALL PRIVILEGES ON employees TO app_user;

-- Revoke permission:
REVOKE INSERT ON employees FROM app_user;

-- Change password:
ALTER ROLE app_user WITH PASSWORD 'new_password';

-- Allow a role to inherit membership:
GRANT read_only_role TO app_user;

-- Remove role membership:
REVOKE read_only_role FROM app_user;

-- Drop role (only if it owns no objects and has no remaining dependencies):
DROP ROLE app_user;
```

### Default privileges for future tables

Run as the role that will create the future tables, or specify the creator with `FOR ROLE`:

```sql
ALTER DEFAULT PRIVILEGES IN SCHEMA public
GRANT SELECT ON TABLES TO read_only_role;
```

### Sequences permissions

When a role inserts into a table using a sequence, it may also need sequence privileges:

```sql
GRANT USAGE, SELECT ON SEQUENCE employees_employee_id_seq TO app_user;
```

---

## 29. Import and export CSV files

### psql `\copy` (uses the client computer's file access)

```text
\copy employees(first_name, last_name, email, salary) FROM '/absolute/path/employees.csv' WITH (FORMAT csv, HEADER true)
```

Export a table:

```text
\copy employees TO '/absolute/path/employees_export.csv' WITH (FORMAT csv, HEADER true)
```

Export a query:

```text
\copy (SELECT first_name, salary FROM employees WHERE salary > 50000) TO '/absolute/path/high_salary.csv' WITH (FORMAT csv, HEADER true)
```

### SQL `COPY` (uses the database server's file access)

```sql
COPY employees(first_name, last_name, email, salary)
FROM '/server/path/employees.csv'
WITH (FORMAT CSV, HEADER TRUE);

COPY employees
TO '/server/path/employees.csv'
WITH (FORMAT CSV, HEADER TRUE);
```

**Important difference:** `\copy` reads/writes files on the machine running `psql` and is usually easier for local CSV work. SQL `COPY` reads/writes on the database server and requires appropriate server-side file permissions.

---

## 30. Backup and restore

These are shell commands, not commands to type at the `psql` prompt.

```bash
# Plain SQL backup:
pg_dump -U postgres -d company -f company.sql

# Custom-format backup:
pg_dump -U postgres -d company -F c -f company.dump

# Restore a plain SQL backup:
psql -U postgres -d company -f company.sql

# Restore a custom-format backup:
pg_restore -U postgres -d company company.dump

# List contents of a custom-format archive:
pg_restore -l company.dump

# Backup all databases and global objects:
pg_dumpall -U postgres -f all_databases.sql
```

A target database generally needs to exist before restoring into it, unless you use suitable create-database options such as `pg_restore --create` with the appropriate connection setup.

---

## 31. JSON and JSONB

```sql
CREATE TABLE user_profiles (
    id INT PRIMARY KEY,
    details JSONB
);

INSERT INTO user_profiles (id, details)
VALUES (1, '{"name":"Manish","age":22,"city":"Hyderabad"}');

-- Get JSON value:
SELECT details -> 'name'
FROM user_profiles;

-- Get JSON value as text:
SELECT details ->> 'name'
FROM user_profiles;

-- Get nested JSON:
SELECT details -> 'address' -> 'city'
FROM user_profiles;

-- Check whether a top-level key exists:
SELECT *
FROM user_profiles
WHERE details ? 'name';

-- Check whether JSON contains a structure:
SELECT *
FROM user_profiles
WHERE details @> '{"city":"Hyderabad"}';

-- Update JSONB:
UPDATE user_profiles
SET details = jsonb_set(details, '{city}', '"Mumbai"')
WHERE id = 1;
```

Useful JSON operators:

| Operator | Meaning |
|---|---|
| `->` | Get JSON object field or array element |
| `->>` | Get field/element as text |
| `#>` | Get JSON at a path |
| `#>>` | Get text at a path |
| `?` | Does top-level key/string exist? |
| `?|` | Does any listed key exist? |
| `?&` | Do all listed keys exist? |
| `@>` | Does left JSON contain right JSON? |
| `<@` | Is left JSON contained in right JSON? |
| `||` | Concatenate JSONB values |
| `-` | Remove key or array element |
| `#-` | Remove a path |

---

## 32. Arrays

```sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    tags TEXT[]
);

INSERT INTO products
VALUES (1, ARRAY['sql', 'postgres', 'database']);

-- Read array:
SELECT tags FROM products;

-- Access first element (PostgreSQL arrays are 1-based by default):
SELECT tags[1] FROM products;

-- Check whether an array contains a value:
SELECT *
FROM products
WHERE 'sql' = ANY(tags);

-- Append an element:
UPDATE products
SET tags = array_append(tags, 'backend')
WHERE id = 1;

-- Array length:
SELECT array_length(tags, 1)
FROM products;

-- Expand array into rows:
SELECT unnest(tags)
FROM products;
```

---

## 33. Full-text search

```sql
SELECT to_tsvector('english', 'PostgreSQL is a powerful database')
       @@ plainto_tsquery('english', 'powerful database');

SELECT *
FROM articles
WHERE to_tsvector('english', title || ' ' || body)
      @@ plainto_tsquery('english', 'database performance');
```

Useful functions include `to_tsvector`, `to_tsquery`, `plainto_tsquery`, `phraseto_tsquery`, and `websearch_to_tsquery`.

---

## 34. Extensions

Extensions add optional PostgreSQL functionality.

```sql
-- List installed extensions in psql:
-- \dx

-- Install an extension:
CREATE EXTENSION IF NOT EXISTS pgcrypto;

-- Remove an extension:
DROP EXTENSION IF EXISTS pgcrypto;
```

An extension must be available on the server and the role must have sufficient privileges to install it.

---

## 35. Useful information_schema and system catalog queries

```sql
-- List tables in public schema:
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public'
  AND table_type = 'BASE TABLE';

-- List columns of a table:
SELECT column_name, data_type, is_nullable, column_default
FROM information_schema.columns
WHERE table_schema = 'public'
  AND table_name = 'employees'
ORDER BY ordinal_position;

-- List constraints:
SELECT constraint_name, constraint_type
FROM information_schema.table_constraints
WHERE table_schema = 'public'
  AND table_name = 'employees';

-- List current database:
SELECT current_database();

-- Current role:
SELECT current_user;

-- Session user:
SELECT session_user;

-- Current schema:
SELECT current_schema();

-- PostgreSQL version:
SELECT version();

-- Current settings:
SHOW ALL;

-- Search path:
SHOW search_path;
```

---

## 36. Useful PostgreSQL utility commands

### Generate a sequence of values

```sql
SELECT generate_series(1, 10);

SELECT generate_series(
    DATE '2026-01-01',
    DATE '2026-01-10',
    INTERVAL '1 day'
);

SELECT *
FROM generate_series(1, 10) AS n;
```

### Aggregate with FILTER

```sql
SELECT
    COUNT(*) AS total_employees,
    COUNT(*) FILTER (WHERE department_id = 1) AS department_one,
    COUNT(*) FILTER (WHERE salary > 50000) AS high_salary_count
FROM employees;
```

### DISTINCT ON

Returns the first row for each distinct key according to `ORDER BY`.

```sql
SELECT DISTINCT ON (department_id)
       department_id, first_name, salary
FROM employees
ORDER BY department_id, salary DESC, employee_id;
```

### RETURNING

```sql
INSERT INTO employees (first_name, salary)
VALUES ('Asha', 45000)
RETURNING *;

UPDATE employees
SET salary = salary + 500
WHERE employee_id = 1
RETURNING *;

DELETE FROM employees
WHERE employee_id = 1
RETURNING *;
```

### Lock rows

```sql
BEGIN;

SELECT *
FROM employees
WHERE employee_id = 1
FOR UPDATE;

COMMIT;
```

Other row-locking clauses include `FOR NO KEY UPDATE`, `FOR SHARE`, and `FOR KEY SHARE`. `NOWAIT` fails immediately if a conflicting lock cannot be acquired; `SKIP LOCKED` skips locked rows.

---

## 37. Common SQL command categories

| Category | Full form | Main commands |
|---|---|---|
| DDL | Data Definition Language | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| DML | Data Manipulation Language | `INSERT`, `UPDATE`, `DELETE`, `MERGE` |
| DQL | Data Query Language | `SELECT` |
| DCL | Data Control Language | `GRANT`, `REVOKE` |
| TCL | Transaction Control Language | `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

### MERGE (insert/update/delete based on a match)

PostgreSQL supports `MERGE` in current releases:

```sql
MERGE INTO target_employees AS target
USING source_employees AS source
ON target.employee_id = source.employee_id
WHEN MATCHED THEN
    UPDATE SET salary = source.salary
WHEN NOT MATCHED THEN
    INSERT (employee_id, first_name, salary)
    VALUES (source.employee_id, source.first_name, source.salary);
```

The source and target must have compatible columns, and the `ON` condition should identify matches appropriately.

---

## 38. Logical order of SELECT processing

A useful simplified logical order is:

1. `WITH`
2. `FROM` and `JOIN`
3. `WHERE`
4. `GROUP BY` and aggregate calculation
5. `HAVING`
6. `SELECT`
7. `DISTINCT`
8. Set operations (`UNION`, `INTERSECT`, `EXCEPT`) where applicable
9. `ORDER BY`
10. `LIMIT` / `OFFSET` / `FETCH`

This is a logical model, not a promise of the physical execution order chosen by the query planner.

---

## 39. Common mistakes to avoid

1. Forgetting `;` at the end of an SQL statement.
2. Typing `\l`, `\dt`, or `\d` as SQL. They are psql meta-commands.
3. Using `=` with NULL instead of `IS NULL`.
4. Running `UPDATE` or `DELETE` without checking the `WHERE` clause.
5. Using `WHERE` to filter aggregate results; use `HAVING`.
6. Selecting columns that are neither grouped nor aggregated in a grouped query.
7. Forgetting the join condition and accidentally producing a cross join.
8. Assuming `COUNT(column)` counts NULL values; it does not. Use `COUNT(*)` to count rows.
9. Assuming `UNION ALL` removes duplicates; it does not.
10. Assuming `RANK()` and `DENSE_RANK()` behave the same after ties.
11. Using `NOT IN` when the subquery can return NULL; consider `NOT EXISTS`.
12. Assuming `\copy` and SQL `COPY` access files from the same machine.
13. Forgetting that `DROP ... CASCADE` can remove dependent objects.
14. Assuming a normal view stores its query results; materialized views store results.
15. Assuming an index always makes a query faster; check with `EXPLAIN ANALYZE`.

---

## 40. Quick daily-use command sequence

```sql
-- Create database (run from a connection to another database):
CREATE DATABASE practice_db;

-- Connect inside psql:
-- \c practice_db

-- Create a table:
CREATE TABLE students (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT CHECK (age >= 0),
    city VARCHAR(100),
    marks NUMERIC(5, 2)
);

-- Insert data:
INSERT INTO students (name, age, city, marks)
VALUES
    ('Manish', 22, 'Hyderabad', 90.5),
    ('Rahul', 23, 'Mumbai', 85.0),
    ('Asha', 21, 'Pune', 95.0);

-- Read:
SELECT * FROM students;

-- Filter:
SELECT * FROM students
WHERE marks > 85;

-- Sort:
SELECT * FROM students
ORDER BY marks DESC;

-- Group:
SELECT city, COUNT(*), AVG(marks)
FROM students
GROUP BY city;

-- Update:
UPDATE students
SET marks = 92
WHERE name = 'Manish';

-- Delete:
DELETE FROM students
WHERE name = 'Rahul';

-- Inspect in psql:
-- \dt
-- \d students

-- Remove table if needed:
DROP TABLE students;
```

---

## 41. Official references

- PostgreSQL documentation: https://www.postgresql.org/docs/current/
- SQL command reference: https://www.postgresql.org/docs/current/sql-commands.html
- psql reference: https://www.postgresql.org/docs/current/app-psql.html
- SQL functions and operators: https://www.postgresql.org/docs/current/functions.html
- Data types: https://www.postgresql.org/docs/current/datatype.html
- PostgreSQL tutorial: https://www.postgresql.org/docs/current/tutorial.html
"""
