# Database Isolation Levels

Isolation levels control how transactions interact when multiple transactions run at the same time.

## 1. Concurrency Problems

- **Dirty Read:** Reading data that another transaction has changed but not committed.
- **Non-Repeatable Read:** Reading the same row twice and getting different values because another transaction updated it.
- **Phantom Read:** Running the same query twice and getting different rows because another transaction inserted or deleted matching rows.

## 2. Four Isolation Levels

### Read Uncommitted
- Lowest isolation level.
- Allows dirty reads in databases that support them.
- Other concurrency problems can also occur.
- PostgreSQL treats it as Read Committed.

### Read Committed
- Reads only committed data.
- Prevents dirty reads.
- Non-repeatable reads and phantom reads can occur.
- Default isolation level in PostgreSQL.

```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
COMMIT;
```

### Repeatable Read
- Repeated reads return consistent results.
- Prevents dirty and non-repeatable reads.
- Standard SQL allows phantom reads.
- PostgreSQL also prevents phantom reads at this level.

```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
COMMIT;
```

### Serializable
- Highest isolation level.
- Transactions behave as if they ran one after another.
- Prevents all three standard concurrency problems.
- Transactions may need to be retried if serialization fails.

```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
COMMIT;
```

## 3. Comparison

| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|---|---|---|---|
| Read Uncommitted | Possible | Possible | Possible |
| Read Committed | No | Possible | Possible |
| Repeatable Read | No | No | Possible |
| Serializable | No | No | No |

*Note: PostgreSQL prevents phantom reads in Repeatable Read as well.*

## 4. MVCC (Multi-Version Concurrency Control)

MVCC allows multiple transactions to access different versions of the same data without blocking each other unnecessarily.

PostgreSQL uses MVCC to manage concurrent transactions.
