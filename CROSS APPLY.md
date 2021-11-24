# CROSS APPLY technique for query optimization

Use Northwind database for this.

Before cross apply. Please check execution plan by pressing "CTRL + L" for better understanding.
``` SQL 
 Select cust.CompanyName, 
	   (Select top 1 OrderID
	    from orders o
		where o.CustomerID = cust.customerid
		order by OrderID desc
	   )[Last Order],
	   (Select top 1 Freight
	    from orders o
		where o.CustomerID = cust.customerid
		order by OrderID desc
	   )[Last freight],
	   (Select top 1 ShipName
	    from orders o
		where o.CustomerID = cust.customerid
		order by OrderID desc
	   )[Last shipname]

from Customers cust

Order by cust.CompanyName
```
After applying CROSS APPLY
```SQL
Select cust.companyname, CAPoperator.*
from customers cust

cross apply(
	Select TOP 1 orderid as [LAST ORDER],
				 freight as [LAST FREIGHT],
				 shipname as [LAST SHIPNAME]
	from orders o
		where o.CustomerID = cust.customerid
		order by OrderID desc
	) CAPoperator

order by cust.CompanyName ```
