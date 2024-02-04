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

That is simply atomicity, Just like atoms tied together or simply killed.

## C - Consistency
Consistency can be understood as after a successful write, update or delete of a Record, any read request immediately receives the latest value of the Record.

Consistency is a broad term and applies to many areas like data, reads and writes in a database.

Consistency is usuaully defined by the user. The Database admin is usually the one having the idea for the amount of consistency guaranteed in the current architechture.

## I - Isolation
Each transaction happens in a distinct order without any transaction occuring in tandem. This simply means that any read or write performed on the database will not be impacted by other read or writes of a seperate transaction occuring on the same database.

### Read phenomena 
There can be three different read phenomena when a transaction retrieves data that another transaction might have updated.

#### Dirty reads 
Dirty read is when one transaction directly affects results of a read of another transaction. The transaction may not be commited giving completely dirty results in other transaction based on current changes. 


#### Non-repeatable reads
Non-repeatable reads is similar to dirty reads but the transaction is usually commited which makes it inconsistent yet not dirty since the parallel transaction that can cause change in value is usually commited.

#### Phantom reads
Phantom reads occur when a transaction retrieves rows twice and rows are inserted or removed from that set by another transaction that is commited in between.

### Isolation Levels
- **Read uncommited** - No isolation, Any change from outside is visible to the transaction commited or not.
- **Read commited** - Each query in a transaction only sees commited changes by other transactions
- **Repeatable read** - The transaction will make sure that when a query reads a row that row will remain unchanged while it's running
- **Snapshot** - Each query in a transaction only sees changes that have been commited to the start of the transaction. 
- **Serializable** - Transactions are run as if they serialized one after the other.

### Isolation Implementation
Different database approach isolation differently. There is basically the use of locks to avoid lost updates. The locks are simply meaning not allowing any other transaction to act on it. There are optimistic and pessimistic approaches towards the implementation of isolation on databases.

## D - Durability
Changes made by commited transactions must be persisted in a durable non-volatile storage.

There are different Durability techniques like Write ahead log, Asynchronous Snapshot, Append only file.


