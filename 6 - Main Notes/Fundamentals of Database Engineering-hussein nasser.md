course content 
1-ACID is the interesting topic to add to course 
2-we have indexing in this course 
3-underrated topic which is database positioning 
4-database sharding, more mainstream and buzzword without any tools, from scratch building 
5-databases replication, scaling of database 

-----------------------------------------------
**Section 2 - ACID**
---------------------------------------
vid 7
- agenda 
  understanding of Transaction, Atomicity, isolation, consistency and Durability
----------
vid8- what is transactions?
is a collection of queries which is treated as a single unit of work to finish some actions and it could be change data or read only as well
- lifespan of transactions 
  1-BEGIN - COMMIT - ROLLBACK
  here he talking about every database technology how it uses these transactions which one is faster and which is the slower and respective 
- Nature of transaction
  1-usually are used to changes and modify data 
  2-however, it's perfectly normal to have a read only transaction
  3- Example, you want to generate a report and you want to get consistent snapshot based at the time of transaction
  4- we will learn more in isolation section
- ![[Pasted image 20260620211520.png]]
- here we have the practical example how we done the transaction 
----------------------

**9-Atomicity**
----------

-one of the four acid properties that defins a relational dbms - it could be also with normal database not only the relational 
-All queries in a transaction must succeed. 
● If one query fails, all prior successful queries in the transaction should rollback. 
● If the database went down prior to a commit of a transaction, all the successful queries in the transactions should rollback

example : 
when he tries to send money "100$" from account 1 to account 2, then he selecting the balance to make sure he have money 
he made sure he have enough amount, then he decrease the amount from the account then the database crashed ![[Pasted image 20260901134043.png]]
After we restarted the machine the first account has been debited but the other account has not been credited. ------> **lack of atomicity leads to inconsistencies**
● This is really bad as we just lost data, and the information is inconsistent 
● An atomic transaction is a transaction that will rollback "it takes more than 1 hour" all queries if one or more queries failed. ● The database should clean this up after restart.
- Atomicity is the idea of the transaction being one unit of work, and that cannot be split

------------------------------------------------
10-Isolation
-----------
we gonna talk about read phenomena which need to understand in this specific topic 


A **dirty read** happens when one transaction reads data that another transaction has changed but not yet saved or committed.
![[Pasted image 20260901144355.png]]
A **non-repeatable read** happens when a transaction reads the same specific row twice and gets different data each time because another transaction changed that row
![[Pasted image 20260901144405.png]]
A **phantom read** happens when a transaction runs the same query twice and gets a different set of rows because another transaction added or deleted rows that fit the query
![[Pasted image 20260901144416.png]]
A **lost update** happens when two transactions read the exact same value and both try to update it, causing one update to overwrite and erase the other.![[Pasted image 20260901144515.png]]

Isolation - Isolation Levels for inflight transactions : 

● Read uncommitted - No Isolation, any change from the outside is visible to the transaction, committed or not.
● Read committed - Each query in a transaction only sees committed changes by other transactions 
● Repeatable Read - The transaction will make sure that when a query reads a row, that row will remain unchanged while its running.
● Snapshot - Each query in a transaction only sees changes that have been committed up to the start of the transaction. It's like a snapshot version of the database at that moment. 
● Serializable - Transactions are run as if they serialized one after the other. 
● Each DBMS implements Isolation level differently
![[Pasted image 20260901160815.png]]
**Database Implementation of Isolation**

● Each DBMS implements Isolation level differently 
● Pessimistic - Row level locks, table locks, page locks to avoid lost updates 
● Optimistic - No locks, just track if things changed and fail the transaction if so 
● Repeatable read “locks” the rows it reads but it could be expensive if you read a lot of rows, postgres implements RR as snapshot. That is why you don’t get phantom reads with postgres in repeatable read 
● Serializable are usually implemented with optimistic concurrency control, you can implement it pessimistically with SELECT FOR UPDATE

--------------------------------------
**11-Consistency**
------
