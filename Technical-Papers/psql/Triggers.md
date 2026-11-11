# Database Triggers

A trigger is a database operation that automatically runs when a specific event happens in a table.

Triggers are commonly used for auditing, maintaining logs, and automatically updating related data.

## 1. Types of Triggers

- **BEFORE:** Runs before an INSERT, UPDATE, or DELETE.
- **AFTER:** Runs after an INSERT, UPDATE, or DELETE.
- **INSTEAD OF:** Runs instead of an operation (commonly used with views).

## 2. Trigger Events

- INSERT
- UPDATE
- DELETE

## 3. Creating a Trigger in PostgreSQL

First, create a function:

```sql
CREATE OR REPLACE FUNCTION log_changes()
RETURNS TRIGGER AS $$
BEGIN
    RAISE NOTICE 'A row was inserted';
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

Now create a trigger:

```sql
CREATE TRIGGER employee_insert_trigger
AFTER INSERT ON employees
FOR EACH ROW
EXECUTE FUNCTION log_changes();
```

Whenever a new employee is inserted, the trigger automatically executes the function.

## 4. NEW and OLD

- **NEW:** Contains the new row values.
- **OLD:** Contains the previous row values.

Example:

```sql
CREATE OR REPLACE FUNCTION check_salary()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.salary < 0 THEN
        RAISE EXCEPTION 'Salary cannot be negative';
    END IF;

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

This prevents inserting or updating an employee with a negative salary.

## 5. Row-Level and Statement-Level Triggers

- **FOR EACH ROW:** Runs once for every affected row.
- **FOR EACH STATEMENT:** Runs once for the entire SQL statement.

## 6. Managing Triggers

Delete a trigger:

```sql
DROP TRIGGER employee_insert_trigger ON employees;
```

List triggers:

```sql
SELECT *
FROM information_schema.triggers;
```
