
# Transaction Management and Concurrency Control in DBMS

Transaction management ensures that multiple database operations are executed correctly. Concurrency control prevents problems when multiple transactions access or modify the same data at the same time.

## 1. Concurrency Control

Concurrency control manages multiple transactions running simultaneously without causing incorrect results.

**Example:**

Suppose a bank account has ₹5,000.

- Transaction A wants to withdraw ₹1,000.
- Transaction B wants to withdraw ₹2,000.

Both transactions access the same account. The database must make sure their operations don't overwrite each other or produce an incorrect balance.

## 2. Locks in DBMS

A lock controls access to data when multiple transactions try to use the same record.

There are two main types of locks.

### Shared Lock (S Lock)

A shared lock allows multiple transactions to read the same data at the same time, but they cannot modify it while the shared locks are held.

**Example:** Two users can view the same bank account balance simultaneously.

### Exclusive Lock (X Lock)

An exclusive lock allows only one transaction to modify the data. Other transactions cannot read or modify that data while the exclusive lock is held.

**Example:** If one user is updating an account balance, another user must wait before accessing that record in a conflicting way.

## 3. Two-Phase Locking (2PL)

Two-Phase Locking is a protocol used to control concurrent transactions and ensure conflict serializability.

It has two phases:

### Growing Phase

A transaction can acquire locks but cannot release any locks.

### Shrinking Phase

A transaction can release locks but cannot acquire new locks.

**Example:**

A transaction needs to update two accounts.

1. Acquire a lock on Account A.
2. Acquire a lock on Account B.
3. Perform the updates.
4. Release the locks.

Once the transaction releases its first lock, it cannot acquire any new locks under basic 2PL.

## 4. Strict Two-Phase Locking

Strict 2PL is a variation of 2PL in which exclusive locks are held until the transaction commits or rolls back.

This prevents other transactions from reading or modifying uncommitted changes.

It helps avoid dirty reads and cascading rollbacks.

## 5. Deadlock

A deadlock happens when two or more transactions wait for each other to release locks, and none of them can continue.

**Example:**

- Transaction A locks Account 1 and waits for Account 2.
- Transaction B locks Account 2 and waits for Account 1.

Both transactions keep waiting for each other.

The database needs to detect the deadlock and resolve it, usually by aborting one transaction.

## 6. Serializability

Serializability means concurrent transactions should produce the same result as if they had executed one after another in some order.

**Example:**

Suppose two transactions update the same bank account.

Instead of allowing their operations to interfere with each other, the database should ensure that the final result is equivalent to a valid sequential execution.

Two common types are:

- **Conflict Serializability:** A schedule is equivalent to a serial schedule based on the order of conflicting operations.
- **View Serializability:** A schedule is equivalent to a serial schedule based on which transactions read values and perform the final writes.

## 7. Problems in Concurrent Transactions

### Dirty Read

One transaction reads data that another transaction has modified but not committed.

If the other transaction rolls back, the first transaction has read invalid data.

### Lost Update

Two transactions update the same data, and one update overwrites the other.

### Non-Repeatable Read

A transaction reads the same row twice but gets different values because another transaction updated and committed the row in between.

### Phantom Read

A transaction runs the same query twice but gets different sets of rows because another transaction inserted or deleted matching rows.

## 8. Isolation Levels

Isolation levels control how much one transaction can see the changes made by other transactions.

| Isolation Level | Description |
|---|---|
| Read Uncommitted | Allows reading uncommitted changes. |
| Read Committed | Reads only committed data. |
| Repeatable Read | Prevents non-repeatable reads. |
| Serializable | Provides the strongest isolation, making transactions behave as if they execute sequentially. |

## 9. Optimistic and Pessimistic Locking

### Pessimistic Locking

Assumes conflicts may happen, so it locks data before modifying it.

Example: Locking a bank account before updating its balance.

### Optimistic Locking

Assumes conflicts are less likely. Transactions proceed without locking the data initially and check for conflicts before committing.

Example: Checking a version number before updating a user's profile. If another transaction has already changed it, the update is rejected or retried.
