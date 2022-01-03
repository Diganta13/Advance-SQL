# How trim() works in SQL Server
In sql server trim works like below. As one example is above Here I have given another example using 
substring on email to extract the domain part.


``` SQL
SELECT email, 
  SUBSTRING( email, CHARINDEX('@', email)+1, LEN(email)-CHARINDEX('@', email) ) domain 
  FROM practice 
  ORDER BY email;
```
![image](https://user-images.githubusercontent.com/39103102/147924856-d1c9b6c7-0080-44c0-af1d-4cf9577756c3.png)
