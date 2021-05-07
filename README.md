	**** Fall 2021 Data Science Intern Challenge ****

Question 1: 
There are two major discrepancies in the data which are leading to an error when calculating AOV naively. First, store 42 has orders that are in bulk, where each transaction consists of 2000 shoe purchases, accounting for a 704000 order value. To counter such issues, a better metric would be use the Average Product Value (APV), which returns the average value of the product for each transaction. The value for such a metric in this dataset would be $387.74. The second discrepancy is caused by store 78, which is selling each shoe at $25,725 (i.e. APV of $25,725). When compared to other stores, such a high price for a shoe is a significant outlier, and could be explained due to two reasons. Either the store sells an extremely high-end shoe, or there is some error in the system, where the price is not showing up accurately. To resolve such an issue, specific details about the store are required, and moving forward, a control chart type of mechanism can be used to identify and point out such discrepancies in a timely manner. 

Question 2:

(a) SELECT Count(ShipperID) FROM [Orders] where ShipperID == 1
	
	Answer = 54


(b) SELECT Employees.LastName FROM Employees INNER JOIN(SELECT EmployeeID, COUNT(OrderID) FROM Orders GROUP BY EmployeeID ORDER BY COUNT(OrderID) DESC LIMIT 1) HighestOrders ON Employees.EmployeeID = HighestOrders.EmployeeID

	Answer = Peacock 

(c) SELECT Products.ProductName FROM Products INNER JOIN (SELECT x.ProductID,SUM(x.Quantity) FROM Customers INNER JOIN (SELECT OrderDetails.ProductID,OrderDetails.Quantity,Orders.CustomerID FROM OrderDetails INNER JOIN Orders ON OrderDetails.OrderID == Orders.OrderID) x ON 				 
    Customers.CustomerID == x.CustomerID AND Customers.Country like 'Germany' GROUP BY ProductID ORDER BY SUM(x.Quantity) DESC LIMIT 1) y ON Products.ProductID == y.ProductID

	Answer = Boston Crab Meat
