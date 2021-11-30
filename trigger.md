# Trigger in SQL
Triggers can be defined to run instead of or after DML (Data Manipulation Language) actions such as INSERT, UPDATE, and DELETE. 
Triggers help the database designer ensure certain actions, such as maintaining an audit file, are completed regardless of which 
program or user makes changes to the data.

Here I have shown a basic trigger for update a table-

--Create table and insert some data on it
```SQL

CREATE TABLE Employee_Test  
(  
Emp_ID INT Identity,  
Emp_name Varchar(100),  
Emp_Sal Decimal (10,2)  
) 

INSERT INTO Employee_Test VALUES ('Anees',1000);  
INSERT INTO Employee_Test VALUES ('Rick',1200);  
INSERT INTO Employee_Test VALUES ('John',1100);  
INSERT INTO Employee_Test VALUES ('Stephen',1300);  
INSERT INTO Employee_Test VALUES ('Maria',1400); 

Select * from Employee_Test

--Create trigger 
 
CREATE TRIGGER trgAfterInsertAgain ON Employee_Test
FOR INSERT  
AS  
declare @empid int;  
declare @empname varchar(100);  
declare @empsal decimal(10,2);  
declare @audit_action varchar(100);  
select @empid=i.Emp_ID from inserted i;   
select @empname=i.Emp_Name from inserted i;   
select @empsal=i.Emp_Sal from inserted i;   
set @audit_action='Inserted Record -- After Insert Trigger.';  
  
insert into Employee_Test_Audit  
(Emp_ID,Emp_Name,Emp_Sal,Audit_Action,Audit_Timestamp)   
values(@empid,@empname,@empsal,@audit_action,getdate());  
  
PRINT 'AFTER INSERT trigger fired.'  
GO

--Then insert data again on employee_test table
insert into Employee_Test values('Shamim',2300);
-- Check Employee_Test_Audit table
SQL Select * from Employee_Test_Audit```
