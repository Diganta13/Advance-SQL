# Stored-Procedure with simple example
Here I have shown a way for creating stored procedures. You would create your own.
It is a simple Stored-Procedure without parameter

``` SQL CREATE PROCEDURE SelectAllCustomers
AS
SELECT * FROM Customers
GO;

--Execute the stored procedure above as follows:
EXEC SelectAllCustomers; ```

Stored Procedure With One Parameter:
The following SQL statement creates a stored procedure that selects Customers from a particular City from the "Customers" table:

``` SQL
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;

-- Execute the stored procedure above as follows:
EXEC SelectAllCustomers @City = 'London'; ```



Stored Procedure With Double Parameter:
The following SQL statement creates a stored procedure that selects Customers from a particular City from the "Customers" table:

``` SQL
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
AS
SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
GO;

-- Execute the stored procedure above as follows:
EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP'; ```



