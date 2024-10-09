---
context: Databases
---


- Ensure reliable processing of database transactions, even in the event of errors, system failures, or other issues.
    - **Atomicity**
        - Ensures that a transaction is treated as a single, indivisible unit.
        - Either all operations in a transaction succeed, or none of them do.
        - If any part fails, the entire transaction is rolled back, leaving the database unchanged.
    - **Consistency**
        - Guarantees that a transaction brings the database from one valid state to another.
        - Ensures all data written to the database adheres to defined rules, constraints, and cascades, meaning it remains in a consistent state before and after the transaction.
        - Maintains referential integrity and data accuracy.
    - **Isolation**
        - Ensures that concurrent transactions do not interfere with each other.
        - Makes it appear as if each transaction is executing in isolation, even when multiple transactions are running simultaneously.
        - Prevents issues like dirty reads, non-repeatable reads, and phantom reads.
    - **Durability**
        - Guarantees that once a transaction is committed, it remains committed even in case of system failure.
        - Ensures changes made by committed transactions are permanent and can be recovered after crashes.
        - Often implemented through transaction logs or write-ahead logging.