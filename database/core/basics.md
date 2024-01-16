## What is the 'basics'?

The basics simply means anything beyond the certain entry level concepts of database that we must already know, I do not wish to write what is a database, Why it is used or anything as such because those are definitions, We are here for depth. Definitions means you need an introduction, This is not an introduction but the basics. Fundamentals to be precise.

# A C I D - Atomicity, Consistency, Isolation and Durability

One of the most important concepts to start understanding a Database is the **ACID**. It consist of four simple terms that define the criteria for assessing consistency. Before we dive deep into the ACID properties.

### What is a transaction? 

A transaction is simply a logical unit of work that accesses and modifies the contents of a database usually through read or write operations.

## A - Atomicity

All queries in a transaction must succeed, So atomicity makes sure there is a 100% completion or returns (rollback) to the previous commits. Regardless of failed transaction or a single query failing, The transaction is rolled back.

Eg : Send $100 from Account 1 to Account 2

ID|Account Name|Balance|
|--|------------|-------|
|01|John Hopkins| $1000 |
|02|Don Johnson | $200  |
 

```
SELECT BALANCE FROM ACCOUNT WHERE ID = 1
BALANCE > 100
UPDATE ACCOUNT SET BALANCE = BALANCE - 100 WHERE ID = 1
```

|ID|Account Name|Balance|
|--|------------|-------|
|01|John Hopkins| $900  |
|02|Don Johnson | $200  |
 
This would result in a database crash where the system restarts with $100 subtracted from total balance. The other account has not been credited as well which has resulted in the lack of atomicity, Which means this transaction has to be rolled back to it's original commited state.


