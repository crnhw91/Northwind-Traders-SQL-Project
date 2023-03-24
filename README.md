# Northwind-Traders-SQL-Project

## Scenario

As a method of increasing future sales, the company has decided to give employee bonuses for exemplary performance in sales. Bonuses will be awarded to those employees who are responsible for the five highest order amounts.

**Goal:** Use SQL to identify the employees who are responsible for the five highest order amounts.

**Database:** Northwind Traders Database was used.


<img width="600" alt="Northwind_E-R_Diagram" src="https://user-images.githubusercontent.com/128507587/227566437-f9901583-e2e9-4311-b017-32a2283036dd.png">


Here is the code I used to find the employees who were responsible for the five highest order amounts.

```SQL
Select LastName, FirstName, Orders.OrderID, Products.Productid, --Selected the columns I wanted to see
Quantity, Price, Sum(Quantity * Price) as SalesAmt -- Added a column named SalesAmt to sum the quantity*Price
From employees -- Using the employees table
inner join 
Orders        -- Joined(combined) the orders table to emplyees table
on employees.employeeID = Orders.employeeID
inner join OrderDetails -- Joined(combined) the OrderDetails table to the orders table
on Orders.orderID = OrderDetails.orderID
inner join Products    -- Joined(combined) the products table with the Orderdetails table
on OrderDetails.productid = Products.productid
Group By Orders.OrderID   -- Grouped the orderId's together
Order By SalesAmt DESC    -- Output the highest SalesAmt to the lowest SalesAmt
Limit 5                   -- Output first 5 rows

```

Here is the output

![First code SQL solution output](https://user-images.githubusercontent.com/128507587/227574831-a8fea976-57fe-4c3d-a8ae-59c393e49c70.PNG)

According to the output there are only 3 people who would be getting bonuses. I wasn't sure if the manager wanted to give bonuses to the top five people with the largest sales order or if they just wanted the people who had the 5 highest order amounts. So I made a code to find the top five people just in case.

Here is the code for the top 5 people:

```SQL
Select LastName, FirstName, Orders.OrderID, Products.Productid,
Quantity, Price, Sum(Quantity * Price) as SalesAmt
From employees
inner join 
Orders
on employees.employeeID = Orders.employeeID
inner join OrderDetails
on Orders.orderID = OrderDetails.orderID
inner join Products
on OrderDetails.productid = Products.productid
Group By Orders.OrderID
having orders.orderid in (10372,10424,10417,10324,10351) -- Added this line to specify the top 5 people
Order By SalesAmt DESC
Limit 5
```

Here is the output:

![Second code SQL solution output](https://user-images.githubusercontent.com/128507587/227578668-bccca89a-285c-41d7-a8e7-927de4deb12f.PNG)

## Scenario 2

Your sales manager is assigning customer accounts to new sales representatives, and needs to know how many orders have been placed by each customer.

Here is the code:

```SQL
Select CustomerName, Count(OrderID) as Number_of_Customer_orders -- Wanted to view the customer names and create a column to count the orderid's
From Customers                                 -- This data is from the customers table
inner join Orders
on Customers.CustomerID = Orders.CustomerID   -- Joined(combined the customers table with the Orders table)
Group By Customers.CustomerID                 -- Group the customerid's together
Order by Number_of_Customer_orders DESC       -- Put the number of oreders in descending order

```
Here is the output:

![third code sql solution output](https://user-images.githubusercontent.com/128507587/227581421-6763d87d-3537-41f8-a5a6-f0b9553acf2e.PNG)
