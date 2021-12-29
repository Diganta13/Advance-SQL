# Exception Handling in SQL Server by TRY…CATCH 

SQL Server also has an exception model to handle exceptions and errors that occurs in T-SQL statements. 
To handle exception in Sql Server we have TRY..CATCH blocks. We put T-SQL statements in TRY block and 
to handle exception we write code in CATCH block. If there is an error in code within TRY block then 
the control will automatically jump to the corresponding CATCH blocks. In Sql Server, against a Try block, 
we can have only one CATCH block.

# TRY..CATCH Syntax
```SQL
BEGIN TRY
--T-SQL statements
--or T-SQL statement blocks
END TRY
BEGIN CATCH
--T-SQL statements
--or T-SQL statement blocks
END CATCH 
```

# Error Functions used within CATCH block
ERROR_NUMBER()
This returns the error number and its value is the same as for @@ERROR function.

ERROR_LINE()
This returns the line number of T-SQL statement that caused an error.

ERROR_SEVERITY()
This returns the severity level of the error.

ERROR_STATE()
This returns the state number of the error.

ERROR_PROCEDURE()
This returns the name of the stored procedure or trigger where the error occurred.

ERROR_MESSAGE()
This returns the full text of error message. The text includes the values supplied for any substitutable parameters, such as lengths, object names, or times.


# Exception handling example
```SQL
BEGIN TRY
DECLARE @num INT, @msg varchar(200)
---- Divide by zero to generate Error
SET @num = 5/0
PRINT 'This will not execute'
END TRY
BEGIN CATCH
PRINT 'Error occured that is'
set @msg=(SELECT ERROR_MESSAGE())
print @msg;
END CATCH
GO 
```
To see differnet kind of messages
```SQL
BEGIN TRY
DECLARE @num INT
---- Divide by zero to generate Error
SET @num = 5/0
PRINT 'This will not execute'
END TRY
BEGIN CATCH
SELECT ERROR_NUMBER() AS ErrorNumber, ERROR_SEVERITY() AS ErrorSeverity, ERROR_STATE() AS ErrorState, ERROR_PROCEDURE() AS ErrorProcedure, ERROR_LINE() AS ErrorLine, ERROR_MESSAGE() AS ErrorMessage;
END CATCH;
GO 
```
Just run you will understand better.
