
# CAP Theorem

CAP Theorem explains how a distributed database handles three things: Consistency, Availability and Partition Tolerance.

According to the CAP theorem, when a network failure happens between servers, a distributed system has to choose between Consistency and Availability while maintaining Partition Tolerance.

## 1. Consistency

Consistency means every user should get the latest updated data, no matter which server they access.

**Example:** Suppose you update your bank balance to ₹5,000. When you check your balance from another server, it should also show ₹5,000.

## 2. Availability

Availability means the system should respond to every request, even if some servers are facing problems.

**Example:** If one server of an online shopping application goes down, users should still be able to access the application through another server.

## 3. Partition Tolerance

Partition tolerance means the database should continue operating even when servers cannot communicate with each other because of network failures.

**Example:** Suppose a database has two servers, one in Hyderabad and another in Bengaluru. If the network connection between them breaks, the database should handle that failure instead of completely stopping.

## CAP Theorem Example

Imagine a banking application running on two servers:

- Server A is in Hyderabad.
- Server B is in Bengaluru.

Both servers have the same account data.

Now, suppose the network connection between them breaks. Server A and Server B cannot communicate with each other.

The database has two possible choices:

**CP (Consistency + Partition Tolerance)**

The database prioritizes correct and updated data. If it cannot verify the latest balance because of the network failure, it may reject some requests or wait until communication is restored.

**AP (Availability + Partition Tolerance)**

The database continues accepting requests from both servers, even during the network failure. However, users might temporarily see different or outdated data. The servers can synchronize their data once the connection is restored.

## Summary

| Combination | Description |
|---|---|
| CP | Prioritizes consistency during network failures, even if some requests cannot be served. |
| AP | Prioritizes availability during network failures, even if some data is temporarily outdated. |
| CA | Provides consistency and availability when there is no network partition. |
