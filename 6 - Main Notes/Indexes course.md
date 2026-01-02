
**0 - Introduction to indexes**

(1) Indexes is 100 Times Important than schema 

(2) A separate data Structure ---> separate table of the same data 

(3) Maintain a copy of (Part of ) Your data ---> It takes a part of your data as copy and put it into it's own data structure , so if you have a thousand of indexes it's mean you have thousand of copies

(4) Points back to the row so it can back to the main table 

here we will talk about usage possibility of indexes

(1) As many as you need ----> because it's best tool to create performance applications 

(2) As Few as you can get away with -----> it's not mean "As many as you can" that you can use whatever you want , you need to balancing active and not good to create not needed ones

**Important!!!!!**

Data -----> Schema  "Driven By data"

Queries ------> Indexes 

-------------------------------------------
**1 - B+ Trees**

-  is the underlying data structure behind most indexes in mySQL

"Without index ,mySQL must begin with the first row and then read through the entire table to find the relevent rows"

- when i make a query ask about the row of database it's mean the algorithm  will go directly to tree and ask every leaf and node the index is higher or less than the current 
- ![[Pasted image 20260102171324.png]]

--------------------------------------------------------------------
**2 - Primary Key**

- indexes directly created when you create a Primary Key 
