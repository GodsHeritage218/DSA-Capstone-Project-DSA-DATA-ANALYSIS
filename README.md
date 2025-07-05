# DSA-Capstone-Project-DSA-DATA-ANALYSIS
## OVERVIEW OF MY DATA ANALYSIS PROJECT ASSIGNMENT
## Case Study 2: Kultra Mega Stores Inventory
## Which product category had the highest sales?
## SELECT Product_Category, SUM(Sales) AS Total_Sales
FROM orders
GROUP BY Product_Category
ORDER BY Total_Sales DESC
LIMIT 1;
## What are the tops 3 and bottom 3 region in term of sales
Top 3 regions
SELECT Region, SUM(Sales) AS Total_Sales
FROM orders
GROUP BY Region
ORDER BY Total_Sales DESC
LIMIT 3;
Bottom 3 regions
SELECT Region, SUM(Sales) AS Total_Sales
FROM orders
GROUP BY Region
ORDER BY Total_Sales ASC
LIMIT 3;
## What are the total sales of appliances in Ontario
SELECT SUM(Sales) AS Total_Sales_Appliances_Ontario
FROM orders
WHERE Product_Category = 'Appliances' AND State = 'Ontario';
## Advise the management of KMS on what to do to increase the revenue from the bottom
Firstly, i will identify the bottom 10 customers:
SELECT Customer_Name, SUM(Sales) AS Total_Sales
FROM orders
GROUP BY Customer_Name
ORDER BY Total_Sales ASC
LIMIT 10;
## Advice to management
Customer Feedback: Collect insights on why they purchase less (price, availability, service
## KMS incurred the most shipping cost using which shipping method?
SELECT Shipping_Method, SUM(Shipping_Cost) AS Total_Shipping_Cost
FROM orders
GROUP BY Shipping_Method
ORDER BY Total_Shipping_Cost DESC
LIMIT 1;
## Case Scenario II
## Who are the most valuable customers, and what products or services do they typically
purchase?
-- Most valuable customers by total sales
SELECT Customer_Name, SUM(Sales) AS Total_Sales
FROM orders
GROUP BY Customer_Name
ORDER BY Total_Sales DESC
LIMIT 5;
## To get the products they typically purchase:
SELECT Customer_Name, Product_Category, COUNT(*) AS Purchase_Count
FROM orders
WHERE Customer_Name IN 
  SELECT Customer_Name
  FROM orders
  GROUP BY Customer_Name
  ORDER BY SUM(Sales) DESC
  LIMIT 5
GROUP BY Customer_Name, Product_Category
ORDER BY Customer_Name, Purchase_Count DESC;
## Which small business customer had the highest sales?
SELECT Customer_Name, SUM(Sales) AS Total_Sales
FROM orders
WHERE Segment = 'Small Business'
GROUP BY Customer_Name
ORDER BY Total_Sales DESC
LIMIT 1;
## Which Corporate Customer placed the most number of orders in 2009 – 2012?
SELECT Customer_Name, COUNT(DISTINCT Order_ID) AS Number_of_Orders
FROM orders
WHERE Segment = 'Corporate'
  AND YEAR(Order_Date) BETWEEN 2009 AND 2012
GROUP BY Customer_Name
ORDER BY Number_of_Orders DESC
LIMIT 1;
## Which consumer customer was the most profitable one?
SELECT Customer_Name, SUM(Profit) AS Total_Profit
FROM orders
WHERE Segment = 'Consumer'
GROUP BY Customer_Name
ORDER BY Total_Profit DESC
LIMIT 1;
## Which customer returned items, and what segment do they belong to?
Assuming there's a column called Returned with values like 'Yes' or 'No':
SELECT DISTINCT Customer_Name, Segment
FROM orders
WHERE Returned = 'Yes';
## If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer
## Analysis Strategy:
Group by Order_Priority and Shipping_Method to evaluate the alignment of shipping method and urgency:
SELECT Order_Priority, Shipping_Method, COUNT(*) AS Num_Orders, 
       SUM(Shipping_Cost) AS Total_Shipping_Cost
FROM orders
GROUP BY Order_Priority, Shipping_Method
ORDER BY Order_Priority, Shipping_Method;
## Interpretation Advice
Interpretation Advice:
If Express Air is mostly used for Critical or High priority, and Delivery Truck is used for Low priority, then the shipping cost is well aligned.
If Express Air is used frequently for Low priority, it suggests inefficiency.
If Delivery Truck is used for High or Critical, it may cause customer dissatisfaction due to slow delivery.





