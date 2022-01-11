# Pagination with SQL in SQL SERVER

Pagination is a process that is used to divide a large data into smaller discrete pages, and this process is also known as paging. 
Pagination is commonly used by web applications and can be seen on Google. When we search for something on Google, it shows the 
results on the separated page; this is the main idea of the pagination.

Here I have given a simple sql script for pagination with OFFSET and FETCH option. It's very easy and you can apply your pagination modifing script as your purpose.

```SQL
DECLARE @PageNumber AS INT
DECLARE @RowsOfPage AS INT
SET @PageNumber=1
SET @RowsOfPage=4

SELECT [Ticket ID], Email, City, @PageNumber as page
FROM Table_02
ORDER BY [Ticket ID]

OFFSET (@PageNumber-1)*@RowsOfPage ROWS
FETCH NEXT @RowsOfPage ROWS ONLY
```
