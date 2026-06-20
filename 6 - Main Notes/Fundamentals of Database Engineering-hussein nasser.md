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