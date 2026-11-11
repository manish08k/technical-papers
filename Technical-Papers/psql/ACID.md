
# ACID Properties in DBMS

ACID stands for Atomicity, Consistency, Isolation and Durability. These four properties ensure that database transactions work correctly and safely.

## 1. Atomicity

Atomicity means a transaction should either complete fully or not happen at all. If one operation fails, all changes made in that transaction should be rolled back.

**Example:**

Suppose you transfer ₹1,000 from Account A to Account B.

- ₹1,000 is deducted from Account A.
- ₹1,000 should be added to Account B.

If the second operation fails, the first operation should also be cancelled.

**Without Atomicity:** Money might get deducted from Account A without reaching Account B.

## 2. Consistency

Consistency means the database should always follow its defined rules and constraints. Every successful transaction should take the database from one valid state to another valid state.

**Example:**

Suppose a bank account has ₹2,000 and the database has a rule that the balance cannot be negative.

If someone tries to withdraw ₹3,000, the database should reject the operation.

**Without Consistency:** Invalid data might be stored, such as a negative account balance, causing incorrect records and calculations.

## 3. Isolation

Isolation means multiple transactions running at the same time should not interfere with each other. Each transaction should work correctly without causing unexpected results because of another transaction.

**Example:**

Suppose a movie theatre has only one seat left. Two users try to book that seat at the same time.

The database should allow only one booking.

**Without Isolation:** Both users might get confirmation for the same seat, causing duplicate bookings.

## 4. Durability

Durability means once a transaction is successfully committed, its changes should remain saved even if the system crashes or loses power.

**Example:**

Suppose you transfer ₹1,000 through a banking application and receive a successful confirmation.

Even if the application crashes immediately afterward, the transaction should remain saved in the database.

**Without Durability:** The database might lose a transaction that was already confirmed, resulting in missing or incorrect records.
