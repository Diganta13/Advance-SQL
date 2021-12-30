# Hierarchical Query with CTE
First I like to say what is CTE?
A CTE can be thought of as a temporary result set and are similar to a derived table in that it is not stored as an object and lasts only for the duration of the query. A CTE 
is generally considered to be more readable than a derived table and does not require the extra effort of declaring a Temp Table while providing the same benefits to the user. 
However; a CTE is more powerful than a derived table as it can also be self-referencing, or even referenced multiple times in the same query.

The basic syntax structure for a CTE is shown below:
``` SQL
WITH MyCTE
AS ( SELECT EmpID, FirstName, LastName, ManagerID
FROM Employee
WHERE ManagerID IS NULL )
SELECT *
FROM MyCTE 
```

# Building a Recursive CTE
In the following examples, you will learn how to harness the power of a recursive CTE query by fulfilling a common business requirement, 
retrieving hierarchical data. By the time the final query is complete you will be able to easily determine how many levels from the top executive each employee is.

A recursive CTE requires four elements in order to work properly.

-Anchor query (runs once and the results ‘seed’ the Recursive query)
-Recursive query (runs multiple times and is the criteria for the remaining results)
-UNION ALL statement to bind the Anchor and Recursive queries together.
-INNER JOIN statement to bind the Recursive query to the results of the CTE.

``` SQL
WITH MyCTE
AS ( SELECT EmpID, FirstName, LastName, ManagerID
FROM Employee
WHERE ManagerID IS NULL
UNION ALL
SELECT EmpID, FirstName, LastName, ManagerID
FROM Employee
INNER JOIN MyCTE ON Employee.ManagerID = MyCTE.EmpID
WHERE Employee.ManagerID IS NOT NULL )
SELECT *
FROM MyCTE
```

# Identify the Anchor and Recursive Query
Anyone who does not have a boss is considered to be at the top level of the company and everyone who does have a boss either works for the person(s) 
at the top level (upper management), or the people that work for them (mid-management thru base employees).

For example, a CEO is at the top level and thus has a ManagerID of null. Likewise, everyone below the CEO will have a ManagerID. 
This is demonstrated in the two queries below:

``` SQL
SELECT EmpID, FirstName, LastName, ManagerID
FROM Employee
WHERE ManagerID IS NULL


SELECT EmpID, FirstName, LastName, ManagerID
FROM Employee
WHERE ManagerID IS NOT NULL
```
