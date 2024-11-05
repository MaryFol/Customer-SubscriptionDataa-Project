# Customer-SubscriptionDataa-Project
* This project involves analyzing customer and subscription data for a subscription service to identify key insights. Using SQL and Excel, and PowerBI.
*  I conducted an in-depth analysis of customer behavior, tracked subscription patterns, and examined trends in cancellations and renewals.

  ### The project covers:
* Total customer count by region and subscription type
*  Subscription duration and revenue by product type
*  Identification of top-performing regions and subscription plans
*  Trends in cancellations and active subscriptions over time

The findings were visualized in a Power BI dashboard to provide clear, actionable view of sales performance, enabling better data-driven decision-making.


----
https://1drv.ms/x/c/217a870815163ae5/ETi6USaoUspPrRMvyVF3024B2OjhU6bE0HPwf0hRDVE59Q?e=tnklLk

----------
``` select * from [dbo].[Subscription Data  Excel Project 2]

``` create database Lita_SubscriptionMary

--------Total number of customers from each region-------

```SELECT Region, count(customerID)
AS TotalCustomers
From [dbo].[Subscription Data  Excel Project 2]
GROUP BY Region

---------Most popular subscription type by the number of customers-----

```SELECT TOP 1 SubscriptionType,
COUNT(CustomerID) 
AS TotalSubscribers
FROM [dbo].[Subscription Data  Excel Project 2]
GROUP BY SubscriptionType
ORDER BY TotalSubscribers Desc```

--------Customers who canceled their subscription within 6 months-------

```SELECT CustomerID,CustomerName,SubscriptionType, Region
FROM [dbo].[Subscription Data  Excel Project 2]
WHERE Canceled = 1 
AND DATEDIFF(Month, SubscriptionEnd, SubscriptionStart) <= 180;


---------Average subscription duration for all customers--------------

```SELECT
AVG(DATEDIFF(Month, SubscriptionStart, SubscriptionEnd))
AS AverageDuration 
FROM [dbo].[Subscription Data  Excel Project 2]


---------------Customers with subscriptions longer than 12 months------

```SELECT CustomerID, CustomerName, SubscriptionType, region
FROM [dbo].[Subscription Data  Excel Project 2]
WHERE DATEDIFF(Month, SubscriptionStart, SubscriptionEnd) > 365

-------Calculate total revenue by subscription type-------

```SELECT SubscriptionType,
SUM(CAST(Revenue AS DECIMAL(10,2))) AS TotalRevenue
FROM [dbo].[Subscription Data  Excel Project 2]
WHERE ISNUMERIC(REVENUE) = 1


--------Top 3 regions by subscription cancellations-------

```SELECT TOP 3 Region,
COUNT(CustomerID) AS Cancellations
FROM [dbo].[Subscription Data  Excel Project 2]
WHERE Canceled = 1
GROUP BY Region
ORDER BY Cancellations


-----------Total number of active and canceled subscriptions---------

```SELECT
COUNT(CASE WHEN Canceled = 0 THEN 1 END) 
AS ActiveSubscriptions,
COUNT(CASE WHEN Canceled = 1 THEN 1 END) 
AS CancelledSubscriptions
FROM [dbo].[Subscription Data  Excel Project 2]

---




