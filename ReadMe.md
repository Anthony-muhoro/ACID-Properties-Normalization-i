# ACID Properties & Normalization

---

## ACID Properties

ACID stands for **Atomicity, Consistency, Isolation, Durability**. These are key properties that guarantee reliable processing of database transactions.

### 1. Atomicity

Atomicity ensures that all commands within a transaction are executed successfully. If any command fails, the entire transaction is canceled and rolled back to its previous state using the `ROLLBACK` command.

**Example:**

Transferring money from one bank account involves multiple steps:

- Debit amount X from Account A
- Credit amount X to Account B

Atomicity ensures either all debit and credit operations succeed or all fail. If the debit succeeds but the credit fails, the entire transaction is rolled back to avoid partial updates and maintain data consistency.

---

### 2. Consistency

Consistency ensures that once a transaction is successfully committed, only valid data according to database rules is saved. It protects the data from corruption due to crashes or invalid transactions.

**Example:**

A transaction crediting 5000 to a bank account with a current balance of 3000 and an overdraft limit of 1000 would be invalid because it exceeds the allowed limit. Such transactions are blocked to maintain consistency.

---

### 3. Isolation

Isolation guarantees that transactions execute independently without interference. One transaction's uncommitted changes are invisible to others, preventing concurrency issues.

**Example:**

If Transaction T1 updates a row, Transaction T2 must wait until T1 commits or rolls back before reading that row. Isolation avoids problems like:

- **Dirty reads:** Reading uncommitted data
- **Lost updates:** Overwriting uncommitted changes from other transactions
- **Non-repeatable reads:** Same query returning different results in one transaction

---

### 4. Durability

Durability ensures that once a transaction is committed, its changes are permanent, even in case of hardware failure, power loss, or crashes.

**Example:**

If a transaction updates a customer's address, durability guarantees the updated address is saved and not lost, thanks to storage mechanisms like logs, backups, and persistent storage.

---

## Normalization

Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves decomposing tables into smaller, well-structured tables according to rules called **normal forms**.

### Objectives of Normalization

- Eliminate redundant data
- Ensure logical data dependencies

---

### Normal Forms

Normalization progresses through stages:

1. **First Normal Form (1NF)**
2. **Second Normal Form (2NF)**
3. **Third Normal Form (3NF)**
4. **Boyce-Codd Normal Form (BCNF)**

---

## 1NF - First Normal Form

1NF requires that:

- Each cell contains a single atomic value.
- Each record is unique (no duplicate rows).

**Example Table:**

| Salutation | Full Name | Address | Skills       |
|------------|------------|---------|--------------|
| Mr.        | John Doe   | Address1| Java, Python |
| Ms.        | Jane Smith | Address2| SQL          |

*Note:* Skills column should be split into atomic values to satisfy 1NF.

---

## 2NF - Second Normal Form

To be in 2NF, a table must:

- Be in 1NF.
- Have no partial dependency of any column on a part of the primary key (only on the whole key).

This means all non-key attributes must depend on the entire primary key.

---

## 3NF - Third Normal Form

To be in 3NF, a table must:

- Be in 2NF.
- Have no transitive dependencies (non-key attributes depending on other non-key attributes).

*Transitive dependency* example: A change in one non-key column causes another non-key column to change.

---

## BCNF - Boyce-Codd Normal Form

BCNF is a stricter version of 3NF, sometimes called 3.5NF.

For a table to be in BCNF:

- It must be in 3NF.
- For every functional dependency (X  → Y), \(X\) must be a super key.

This resolves anomalies related to multiple overlapping candidate keys.

---

# Summary

ACID properties ensure transactional reliability and data integrity during operations, while normalization improves database design by reducing redundancy and improving consistency.

Together, they are fundamental concepts in designing robust, efficient, and reliable database systems.
