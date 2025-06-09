# ACID Properties & Normalization

## ACID Properties

- ACID stands for Atomicity Consistency Isolation Durability.

1. Atomicity: It makes sure that all commands that are part of the transaction must be executed successfully. If not, then the whole transaction should be canceled and rolled back to the previous state using the ROLLBACK command.

- For example, transferring money from one bank account involves multiple steps:

Debit amount X from Account A
Credit amount X to Account B
As per atomicity, either all debit and credit operations succeed or they all fail. If the debit succeeds, but the credit fails for any reason, the entire transaction is rolled back. Atomicity ensures there are no partial or incomplete transactions.

Atomicity prevents unwanted data updates from unconcluded transactions. Without it, the debit may persist while the credit fails, causing data inconsistency. By reverting partial transactions, atomicity keeps the database consistent.

2. Consistency: It makes sure that once the transaction is committed successfully then, only the database should change and save the state. It allows you to protect your data from crashes.

- For example, a transaction crediting 5000 to a bank account with a current balance of 3000 is invalid if the account has an overdraft limit of 1000. The transaction violates consistency by exceeding the permissible account limit. Hence, it is blocked and aborted.

Consistency enforcement prevents data corruption and invalid entries. Only transactions abiding by consistency rules are committed to upholding data accuracy. Real-world business constraints are modeled into the database via consistency.

3. Isolation: It makes sure that each transaction is working independently and isolated from other transactions. It also checks whether the commands are transparent to each other or not.

For instance, if Transaction T1 updates a row, Transaction T2 must wait until T1 commits or rolls back. Isolation prevents T2 from reading unreliable data updated by T1 but not committed yet.

Isolation avoids concurrency issues like:

Dirty reads - Reading uncommitted data from other transactions
Lost updates - Overwriting another transaction's uncommitted updates
Non-repeatable reads - Same query yielding different results across transactions
By isolating transactions, consistency is maintained despite concurrent execution and updates. Changes remain isolated until permanent.

4. <h3>Durability</h3>It makes sure that once the transaction is committed, even if the database crashes or fails, it should still be saved in the database.

- if a transaction updates a customer's address, durability ensures the updated address is not lost due to a hard disk failure or power outage. The change will persist with the help of storage devices, backups, and logs.

Durability ensures that transactions, once committed, will survive permanently. Failed hardware, power loss, and even database crashes will not undo committed transactions due to durability support.

## Normalization:

- it is the process of developing clean data. This includes eliminating redundant and unstructured data and making the data appear similar across all records and fields.

- Normalization is carried out in stages known as normal forms:

  1.  First Normal Form (1NF):

  2.  Second Normal Form (2NF):

  3.  Third Normal Form (3NF):

## 1NF - First Normal Form

ensures there are no two same entries in a group. For a table to be in the first normal form, it should satisfy the following rules:

- Each cell should contain a single value
- Each record should be unique

the table

## 2NF - Second Normal Form

In a 2NF table, all the subsets of data that can be placed in multiple rows are placed in separate tables. For a table to be in the second normal form, it should satisfy the following rules:

- It should be in 1F
- The primary key should not be functionally dependant on any subset of candidate key

## 3NF - Third Normal Form

For a table to be in the third normal form, it should satisfy the following rules:

- It should be in 2F
- It should not have any transitive functional dependencies

A transitive functional dependency is when a change in a column (which is not a primary key) may cause any of the other columns to change.

## BCNF - Boyce and Codd Normal Form

Boyce and Codd Normal Form is a higher version of 3NF and is also known as 3.5NF. A BCNF is a 3NF table that does not have multiple overlapping candidate keys. <br>
For a table to be in BCNF, it should satisfy the following rules:<br>

- It should be in 3F
- For each functional dependency ( X → Y ), X should be a super key
