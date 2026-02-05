
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

- indexes automatically directly created when you create a Primary Key 
![[Pasted image 20260102174329.png]]
- he was talk in example about multicolumn primary key and it's more useful to but it like this 
 -----> primary key (a , b)
1 - primary key will be declared not nullable 
2 - a unique index will be created for the primary key 
3 - you have to have a primary key in your table because the problem occur because of avoide creating one that mysql will create one automatically for you and keep track it with itself

--------------------------------------------
**3 - secondary key**

- is any key or index is not a primary key
1 - every leaf node contains the value indexed 
2 - every secondary index contains a pointer back to primary index 
3 - every single leaf node inthe secondary key has the primary key appended because it has to go back to main data structure to get a rest of the row because index is a copy of part of your data not all of it 

--------------------------------------
**4 - data type**
- is totaly up to for the primary key 
- second one -----> you should prefer unsigned bigInt in almost every case 
 first reason : you run out of the room with it 
 second reason : the risk not worth the benefit 

- not recommend to use UUID or GUID because of big size and it makes index so heavy - distroy the order of B-tree - more slowly in search and joins 
----------------------------  
**6 - where to add indexes** 

1.Query should drive index
2.We need to write a good query to get effective indexes for every query 
3.query to know the indexes of the table : 

```
show indexes from People
```
4.Query to  add indexes 
```
alter Table People add index(birthday)
```
5."explain" before the query it's mean you ask sql to explain a little bit about what actually happen in back stage 
6.when we useing irder by with indexes so we using it for sorting 
7.also with group by it could be used for aggregate function 
8.it could be also used for unbounded and bounded ranges 

---------------------------------
**7.Index Selectivity**

* if we have 2 indexes in one query now sql will involve the cardinality and selectivity related to distinct "How many values are there"
* you should keep in touch the distinct during using indexes 
* "Show indexes" ---> is the sql command which appear the cardinality of the indes to know the most have unique values and use it as index 
* "selectivity" ---> mean the amount of different or unique values for every row of the column 
* MySQL prefer to make index on column 
   1.distinct 
   2.high selectivity 
-----------------------------------------------
**8 - prefix indexes**

* Why adding a index not on entire column is more useful?
* Ans : it makes the index alot smaller and that make it more faster
```
alter table people add index(first_name(4))
```
* some times you have a column of alot of string so applying an index for it will be consume the RAM and slowing insert and update 
* "prefix index" ---> means to make index just for the first 6 or 7 Characters of the column to make it as index 
* related to selectivity and cardinality 
  1-if this 5 characters is unique enough in column so it's good prefix
  2-if this 5 characters is not unique enough in column so it's not good prefix
* advantage of prefix index
  1-less of storage 
  2-Faster for search
  3-very useful for tokens /UUID
* disadvantage of prefix index
  1-not useful for "order by" / "Group by"
  2-not good for weak selectivity 
* when to use ? 
  1- long string 
  2-where condition 
  3- not sorting needed

-------------------------------------------------
**9 - composite indexes**

* if you want to delete an index : 
  ```
  alter table people drop index birthday
  ```
* in this video he was talking about create a index which is composite and contains multi keys and keys in the columns 
* composite index is important an needed concept but need to care about the specific rules to use it
* the way to create it with the following line : 
  ```
  alter table people add index multi(first_name , last_name , birthday)
  ```
* there is a specific rules to use the composite index :
  **left side to right side no skip a column**
* second rule : 
  **it stops at the first range**
* Key_length is the SQL using the composite key and how much it using of it and the number appears in this key_length is how much bytes used depend on how much key is used from the composite index
* the meaning of "it stops at the first range " is when you need to search about a range of
ex. birthday and you put it in the first execution it will stop after that and ignore everything after : 
     -birthday > 1989-08-09 ✔
     first_name = "ahmed"  X
     last_name = "younes" X
* the range happens because index is b-tree when you make equal select not range it's more specific search and when you make range it make sql search in alot of data 

-------------------------------------------
**10 - covering index**

* Describe a situation in which an index covers the entire set of needs for a single query 
* it's mean the query find everything it needs without searching in the original table which give more accuracy 
* usually MySQL search first for index then start to find the row which have a condition then search for table to find the rest select 
* but in covering index it create the index with some changes to make on column for filteration then the other for the searching
  -create Index idx_Country_name_email  
  -on users (Country , name , email )
* so it's not need to make any search on original table 
* you can know the SQL using covering Index when you : 
  -explain select ,,,,,,,,
  -Answer have : Using Index -------> "Search in Index only"
  -Using where ---------> search in table and index 
* When to use ? 
  1- alot of non unique queries 
  2- Select more than Insert 
  3- Column is less
  4- Strong Performance
* When not to use ? 
  1- alot of column 
  2- data is usually changes
  3- Query not usually used
- الجدول = كتاب كبير 
- الIndex = الفهرس 
- ال covering Index = الفهرس و فيه الكلام نفسه 
--------------------------------------
**11- Functional Indexes**

* imsgine you are searching for people which born in feb only like this : 
  ```
  Select * from People 
  where Month(birthday) = 2
  ```
  here , Sql will go through every row to check and it makes the query very slow because in data it  stored with full date not only month
* Function-Based index is the solution, it's a type of reference not store the values of columns with itself , but it store the result of the summition you determine before 
* SQL calculate the answer of every row for the function and store it in separated reference and when you search about you go directly to this reference ( not table ) and print   
  ```
  Alter table People ADD index idx_month_birth ((Month(birthday)));
  ```
  - Multiple Arrow is important to make SQL understand this is func 

**When to use ?**
 1 - one element of full date "Month only / day only / year only "
 2 - Searching with small character 
 3 - summition ex. "Price + taxes"
 