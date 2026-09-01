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

**section 3 - Atomicity**
----------

-one of the four acid properties that defins a relational dbms - it could be also with normal database not only the relational 
-All queries in a transaction must succeed. 
● If one query fails, all prior successful queries in the transaction should rollback. 
● If the database went down prior to a commit of a transaction, all the successful queries in the transactions should rollback

example : 
when he tries to send money "100$" from account 1 to account 2, then he selecting the balance to make sure he have money 
he made sure he have enough amount, then he decrease the amount from the account then the database crashed ![[Pasted image 20260901134043.png]]
After we restarted the machine the first account has been debited but the other account has not been credited. ------> lack of atomicity leads to inconsistencies
● This is really bad as we just lost data, and the information is inconsistent 
● An atomic transaction is a transaction that will rollback all queries if one or more queries failed. ● The database should clean this up after restart.