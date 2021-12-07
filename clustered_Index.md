# Indexing in SQL
Indexing is a procedure that returns your requested data faster from the defined table. Without indexing, 
the SQL server has to scan the whole table for your data. By indexing, SQL server do the exact same thing 
when you searched for a content in a book by checking the index page. In the same way table’s index allows 
us to locate the exact data without scanning the whole table. There are two types of indexing in SQL.

1. Clustered index
2. Non-clustered index

**Clustered Index**
```SQL
CREATE TABLE Employee_clustered
(
 [Id] int Primary Key,
 [Name] nvarchar(50),
 [Salary] int,
 [Gender] nvarchar(10),
 [City] nvarchar(50)
)

--By this query SQL automatically generates clustered index by ID


Create Clustered Index Employee_Gender_Salary
ON Employee_clustered(Gender DESC, Salary ASC)

By this query you can create new index on your desired columns.


execute sp_helpindex Employee_clustered```

By this you can check your indexes.





