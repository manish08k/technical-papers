
# Transactions in DBMS

A transaction is a group of one or more database operations treated as a single unit. It ensures that operations are completed successfully or rolled back if something goes wrong.

For example, transferring money between two bank accounts involves deducting money from one account and adding it to another. Both operations should succeed together.

## 1. Transaction Commands

### BEGIN

Starts a new transaction.

```sql
BEGIN;
```

### COMMIT

Saves all changes made during the transaction permanently.

```sql
COMMIT;
```

### ROLLBACK

Cancels all uncommitted changes made during the transaction.

```sql
ROLLBACK;
```

### SAVEPOINT

Creates a point inside a transaction so we can roll back to that point without cancelling the entire transaction.

```sql
SAVEPOINT sp1;
```

## 2. Transaction Example

Suppose Account A has ₹5,000 and Account B has ₹2,000. We want to transfer ₹1,000 from A to B.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

After the transaction:

- Account A = ₹4,000
- Account B = ₹3,000

If something goes wrong before committing, we can use `ROLLBACK` to cancel the changes.

## 3. SAVEPOINT Example

We can use SAVEPOINT when we want to undo only some operations instead of the entire transaction.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

SAVEPOINT sp1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

ROLLBACK TO SAVEPOINT sp1;

COMMIT;
```

Here, the second update is undone, but the first update remains. The transaction is then committed.

## 4. Transaction Properties

Transactions follow ACID properties:

- **Atomicity:** All operations succeed or none do.
- **Consistency:** Database rules are maintained.
- **Isolation:** Concurrent transactions should not interfere incorrectly.
- **Durability:** Committed changes remain saved.
