
# Locking Mechanism in DBMS

## 1. What is Locking?

Locking is a mechanism used by a DBMS to control access to data when multiple transactions try to access or modify the same data simultaneously.

It prevents problems such as lost updates and dirty reads.

Example:

Two transactions are trying to update the same bank account balance.

- Transaction T1 withdraws ₹500.
- Transaction T2 deposits ₹1,000.

Without proper locking, both transactions might read the same old balance and overwrite each other's changes.

Locking controls when each transaction can access the data.

## 2. Types of Locks

### Shared Lock (S Lock)

- Used when a transaction wants to read data.
- Multiple transactions can hold shared locks on the same data.
- Other transactions cannot acquire an exclusive lock while a shared lock exists.

Example:

```sql
BEGIN;
SELECT * FROM accounts WHERE id = 1 FOR SHARE;
```

Multiple transactions can read the same row while holding compatible shared locks.

### Exclusive Lock (X Lock)

- Used when a transaction wants to modify data.
- Only one transaction can hold an exclusive lock on a particular row.
- Other transactions cannot acquire shared or exclusive locks on that row until the lock is released.

Example:

```sql
BEGIN;
SELECT * FROM accounts WHERE id = 1 FOR UPDATE;

UPDATE accounts
SET balance = balance - 500
WHERE id = 1;

COMMIT;
```

## 3. Lock Compatibility

| Lock  | Shared (S) | Exclusive (X) |
|-------|------------|---------------|
| Shared (S) | Yes | No |
| Exclusive (X) | No | No |

- S + S: Allowed.
- S + X: Not allowed.
- X + S: Not allowed.
- X + X: Not allowed.

## 4. Lock Granularity

Lock granularity determines how much data is locked.

### Database-level locking
Locks the entire database.

### Table-level locking
Locks an entire table.

### Page-level locking
Locks a block of rows stored together on a database page.

### Row-level locking
Locks only a particular row.

Example:

```sql
BEGIN;

SELECT *
FROM accounts
WHERE id = 1
FOR UPDATE;

COMMIT;
```

Only the selected row is locked against conflicting operations.

## 5. Two-Phase Locking (2PL)

Two-Phase Locking is a concurrency control protocol that ensures conflict serializability.

It has two phases:

### Growing Phase
- A transaction can acquire locks.
- It cannot release any locks.

### Shrinking Phase
- A transaction can release locks.
- It cannot acquire new locks.

Example:

```text
T1:
    Acquire S(A)
    Acquire X(B)
    Read A
    Update B
    Release S(A)
    Release X(B)
```

Once T1 releases its first lock, it cannot acquire another lock.

## 6. Strict Two-Phase Locking (Strict 2PL)

Strict 2PL holds all exclusive locks until the transaction commits or rolls back.

Example:

```text
T1:
    Acquire X(A)
    Update A
    Commit
    Release X(A)
```

It prevents other transactions from reading or modifying uncommitted changes protected by those exclusive locks.

## 7. Deadlock

A deadlock occurs when two or more transactions wait for each other to release locks.

Example:

```text
T1:
    Locks A
    Waits for B

T2:
    Locks B
    Waits for A
```

Neither transaction can proceed.

### Deadlock handling

- Detection: Detect cycles in the wait-for graph.
- Prevention: Use rules to prevent circular waiting.
- Timeout: Abort a transaction if it waits too long.
- Recovery: Roll back one transaction to release its locks.

## 8. Lock Escalation

Lock escalation occurs when a database replaces many smaller locks with a larger lock.

Example:

A transaction locks thousands of rows individually. The database may replace those locks with a table-level lock.

This reduces lock-management overhead but can reduce concurrency.

## 9. Locking in PostgreSQL

PostgreSQL supports several locking mechanisms.

### FOR UPDATE

Locks selected rows against conflicting updates and locking operations.

```sql
BEGIN;

SELECT *
FROM accounts
WHERE id = 1
FOR UPDATE;

UPDATE accounts
SET balance = balance - 500
WHERE id = 1;

COMMIT;
```

### FOR SHARE

Acquires a shared row lock.

```sql
BEGIN;

SELECT *
FROM accounts
WHERE id = 1
FOR SHARE;

COMMIT;
```

### Table Lock

```sql
BEGIN;

LOCK TABLE accounts IN ACCESS EXCLUSIVE MODE;

COMMIT;
```

PostgreSQL also uses Multi-Version Concurrency Control (MVCC), allowing ordinary readers and writers to work concurrently in many situations without blocking each other.
