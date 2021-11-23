# Over Operator
This SQL code is on NORTHWIND database. download and load it then just run this query.

'''SQL
--Query-01
SELECT row_number() over(ORDER BY prod.productid) rownum, cat.CategoryName ,
                                                          prod.ProductName
FROM Categories cat
INNER JOIN products prod ON cat.CategoryID=prod.CategoryID

--Query-02
SELECT  ROW_NUMBER() over(PARTITION BY cat.categoryid ORDER BY prod.productid) ProductWiseRowNum,
row_number() over(ORDER BY (SELECT 1)) rownum, cat.CategoryName,prod.ProductName
FROM Categories cat
INNER JOIN products prod ON cat.CategoryID=prod.CategoryID

--Query-03
SELECT dense_rank() over(ORDER BY cat.categoryid) CategoryWiseRowNum,
                    cat.CategoryName,
                    ROW_NUMBER() over(PARTITION BY cat.categoryid
                                      ORDER BY prod.productid) ProductWiseRowNum,
                                 prod.ProductName
FROM Categories cat
INNER JOIN products prod ON cat.CategoryID=prod.CategoryID

--Query-04
SELECT prod.ProductName,
       sum(ord.Quantity*ord.UnitPrice) [TotalAmout]
FROM [Order Details] ord
INNER JOIN Products prod ON ord.ProductID=prod.ProductID
GROUP BY prod.ProductName 
'''
