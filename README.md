# This file contains the task brief and the answers for them
## The goal is to query the Northwind database to the given specifications
### Queries

Q1 - How many orders in NWDB?

Query: 
```
SELECT Count(*) OrderID FROM Orders;
```
Response: 830

Q2 - How many order that the Ship City is Rio de Janeiro?

Query: 
```
SELECT Count(*) FROM Orders WHERE ShipCity = 'Rio de Janeiro';
```
Response: 34

Q3 - Select all orders that the Ship City is Rio de Janeiro or Reims?

Query: 
```
SELECT * FROM Orders WHERE ShipCity = 'Rio de Janeiro' OR ShipCity = 'Reims';
```
Response: ![First image](/sql_assignment_pic1.png)
![Second image](/sql_assignment_pic2.png)
Q4 - Select all of the entries where the Company name has a z or a Z in the table of Customers

Query: 
```
SELECT * FROM Customers WHERE CompanyName LIKE '%z%';
```
Response: ![Third image](/sql_assignment_pic3.png)

Q5 - We need to update all of our FAX information! This Day and age it is a must! 😅😅😅 Find me the Name of All of the companies that we do not have their FAX numbers! I would also like to know with whom I need to speak with, their contact numbers and what city they are base in.

Query: 
```
SELECT CompanyName, ContactName, Phone, City FROM Customers WHERE Fax IS NULL;
```
Response: ![Fourth image](/sql_assignment_pic4.png)
![Fifth image](/sql_assignment_pic5.png)

Q6 - Ahh there you are! My prize ⭐⭐SPARTANTS⭐⭐! MY MARES AND MY STALLIONS! We need to re-target all of our Customers is Paris! Get me information on these clients.

Query: 
```
SELECT * FROM Customers WHERE City = 'Paris';
```
Response: ![Sixth image](/sql_assignment_pic6.png)

Q7 - WAIT! Where are you going? (...) These clients are hard to sell too! We need more intel.. Can you find out, from these clients from Paris, whom orders the most by quantity? Who are our top 5 clients?

Query: 
```SELECT ContactName, Quantity
FROM Orders INNER JOIN [Order Details] ON Orders.OrderID = [Order Details].[OrderID]
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID
WHERE Orders.ShipCity = 'Paris'
ORDER BY Quantity DESC;
```
Response:

Q8 - OMG What are you? Some kind of SQL Guardian Angel? THIS IS AMAZING! May God pay you handsomely 😸 because I have no cash on me!.. I do have one more request. I need to know more about these these Paris client. Can you find out which ones their deliveries took longer than 10 days? Display the Business/client name, contact name, all their contact details (don't forget the fax!), as well as the number of deliveries that where overdue! Just add a column named: 'Number overdue orders'! simple, thank you!

Query:
```
SELECT Customers.ContactName, Customers.CompanyName, Customers.Phone, Customers.Fax, Customers.PostalCode, DATEDIFF(d, OrderDate, ShippedDate) AS "Length of shipping",
SUM(CASE WHEN DATEDIFF(d, OrderDate, ShippedDate) > 10 THEN 1
ELSE 0
END) AS "Number of overdue deliveries"
FROM Orders INNER JOIN [Order Details] ON Orders.OrderID = [Order Details].[OrderID] INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID
WHERE ShipCity = 'Paris'
GROUP BY Customers.ContactName, Customers.CompanyName, Customers.Phone, Customers.Fax, Customers.PostalCode, Orders.ShippedDate, Orders.OrderDate;
```
Response:
