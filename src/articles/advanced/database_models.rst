Database Models
###############

:date: 2013-08-27
:slug: Database Models
:summary: Notes on Database Models
:author: Paul Young

Intro
------

A database model is the logical structure of a database that determines in which manner data can be stored, organized and manipulated.  The underlaying data model of a database can be broken three components:

**1. Structures**
- e.g. Rows and Columns, nodes and edges, key-value pairs

**2. Constraints**
- e.g. all rows must have same number of cloumns, child cannot have two parents, a class of values must be of a certain type

**3. Operations**
- e.g. find the value of a key, find the rows where condition x is met, get the next N bytes of data

Common types of database models include:

- Relational model
- Hierarchical database model
- Network model
- Object model
- Document model

Relational Model
----------------
Probably the model that you are most familiar with, and arguably the most widely used database model is the relational model.  Typically, relational databases are visually represented as tables (rows and columns), and all information is represented by data values in relations.

Database Normalization
----------------------
"Database Normilzation is the process of organizing the fields and tables of a relational database to minimize redundancy and dependency. ... The objective is to isolate data so that additions, deletions, and modifications of a field can be made in just one table and then propagated through the rest of the database using the defined relationships." [1]

The criteria for determining a table's degree of normilization is called the normal forms (abbreviated as NF). A higher normal form implies a higher degree of immunity from inconsistencies and anomalies.

**1NF**
- requiring the existence of a key

**2NF**
- requiring that non-key attributes be dependent on a key

**3NF**
- further requiring that non-key attributes be dependent on nothing but the key

**BCNF**
- Every non-trivial functional dependency in the table is a dependency on a superkey

There are a handful more normal forms going all the way up to 6NF.

ACID
----
Another aspect of relational database systems is that a lot of the implemntations have a set of properties known as ACID (Atomicity, Consistency, Isolation, Durability) that garunatees the reliability of database transactions

**Atomicity**
- Each transaction is all or nothing, if one part of the transaction fails, the whole transaction fails.

**Consistency**
- Ensures that the database will remain in a valid state. i.e. no data can be entered that would violate a database constraint

**Isolation**
- This ensures that concurrent or serial transactions result in the same database state.  i.e. you can transact with the database concurrently and it will not impact another transaction

**Durability**
- Once a transaction has been committed, it will remain so, even in the case of power loss or a crash.

SQL
---
Most relational databases use the SQL querying language.  A major advantage of SQL is that it is based upon relational algebra, and uses algebraic optimization (sort of) to optimize queries.

The Rise of NoSQL
-----------------
A major drawback to the relational database model was that the existing implementations did not scale well.  The ACID requirements meant that, for very large applications where multiple machines for storage maybe required, the performance of the database suffers tremendously.  For applications where "eventual consistency" was acceptable, it made more sense to decrease the reliability requirements of the database in order to imporve performance, and allow the application programmer to resolve "disputes" and irregularities.

**Common NoSQL Systems (System, Year, Data Model)**

- MapReduce, 2004, Key-Value
- CouchDB, 2005, Document
- MongoDB, 2007, Document
- Cassandra, 2008, Key-Value
- Megastore, 2011, Tables
- Spanner, 2012, Tables

Advantages of NoSQL
-------------------
 - Scalability - can be run on multiple machines
 - Flexibilily - schema is defined by the programmer/application
 
 Disadvantages of NoSQL
 ----------------------
 - Inconsistency - Because schema is so application dependent, NoSQL may fail in cases where multiuple apps use the same database
 - Lack of Querying Capabilites - Relational databases provide powerful querying capabilites that allow programmers/applications to push the querying workload to the database server, whereas NoSQL databases more often require that the programmer/application do this work on the client side.
 
 Additional Notes
 ----------------
 - The term NoSQL is a little misleading, as "NoSQL" databases are generally different data models.
 - More and more NoSQL databases are becoming more "SQL-Like".  Spanner, Impala, etc.. The ability to enforce consistency and to provide querying capabilites are becoming more common in newer "NoSQL"database systems.
 
 Homework
 --------
 - Install PyMongo/MondgoDB (of some other NoSQL DB if you would prefer)
 - Re-Implemnt your PronDB code to run with PyMongo/MongoDB


[1] http://en.wikipedia.org/wiki/Database_normalization


