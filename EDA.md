#### Question 1: Find the total number of products in each product category

````sql
SELECT
	PC.ProductCategoryKey,
	COUNT(*) AS TotalProducts
FROM DimProduct P
	JOIN DimProductSubcategory PS
		ON P.ProductSubcategoryKey= PS.ProductSubcategoryKey
	JOIN DimProductCategory PC
		ON PC.ProductCategoryKey =PS. ProductCategoryKey
GROUP BY PC.ProductCategoryKey;
````
![image](https://github.com/user-attachments/assets/aecdb488-59a8-4ef4-bb8e-e3e4a8b0d1af)


#### Question 2: Find the top 10 customers with the highest total purchase amount

````sql
SELECT TOP 10 
  CONCAT(C.FirstName, ' ', C.LastName) FullName,
  SUM(S.SalesAmount) AS TotalPurchase
FROM FactInternetSales S
	JOIN DimCustomer C
		ON S.CustomerKey = C.CustomerKey
GROUP BY
    CONCAT(C.FirstName, ' ', C.LastName) 
ORDER BY TotalPurchase DESC;
````
![image](https://github.com/user-attachments/assets/1455f97b-bcdd-4353-8e18-4c95dcf9303d)


#### Question 3: Find the average purchase for each customer

````sql
SELECT 
  CONCAT(C.FirstName, ' ', C.LastName) FullName,
  AVG(S.SalesAmount) AS AVGPurchase
FROM FactInternetSales S
	JOIN DimCustomer C
		ON S.CustomerKey = C.CustomerKey
GROUP BY CONCAT(C.FirstName, ' ', C.LastName);
````
![image](https://github.com/user-attachments/assets/6753a968-2149-4015-828f-7315158dab3e)


#### Question 4: Find the total quantity sold for each product

````sql
SELECT
	DP.ProductKey,
	SUM(FS.OrderQuantity) TotalQuantity
FROM FactInternetSales FS 
	JOIN DimProduct DP
		ON DP.ProductKey = FS.ProductKey
GROUP BY DP.ProductKey;
````
![image](https://github.com/user-attachments/assets/c2af47b1-cc0a-46f6-a838-ca35bba1ec81)


#### Question 5: Find the total sales amount for each territory

````sql
SELECT
	SalesTerritoryKey,
	SUM(SalesAmount) AS Totalsales
FROM [dbo].[FactInternetSales]
GROUP BY SalesTerritoryKey;
````
![image](https://github.com/user-attachments/assets/ac524bac-1ee9-4324-9745-3aaae0ec786d)


#### Question 6: Find the total number of orders placed in each year

````sql
SELECT
	YEAR(OrderDate) AS OrderYear,
	COUNT(*) AS TotalOrders
FROM FactInternetSales 
GROUP BY YEAR(OrderDate)
````
![image](https://github.com/user-attachments/assets/9d546bcb-dd1a-400e-aa0e-7c233840f4bb)


#### Question 7: Find the average sales amount for each year.

````sql
SELECT
	YEAR(OrderDate) AS OrderYear,
	AVG(SalesAmount) AS AverageSalesAmount
FROM [dbo].[FactInternetSales]
GROUP BY YEAR(OrderDate);
````
![image](https://github.com/user-attachments/assets/2aad1d0f-5484-4c88-9f50-02dae0c99e2c)


#### Question 8: Find the top 5 products with the highest total sales amount

````sql
SELECT TOP 5
	DP.EnglishProductName,
	SUM(SF.SalesAmount) AS TotalSalesAmount
FROM  FactInternetSales SF
	JOIN DimProduct DP 
		ON DP.ProductKey = SF.ProductKey
GROUP BY DP.EnglishProductName
ORDER BY TotalSalesAmount DESC;
````
![image](https://github.com/user-attachments/assets/eff2f835-28f7-41e7-bfb0-909658154793)


#### Question 9: Find the total number of employees in each job title

````sql
SELECT
	Title,
	COUNT(*) AS TotalEmployees
FROM [dbo].[DimEmployee]
GROUP BY Title;
````
![image](https://github.com/user-attachments/assets/364fc704-2359-4bcb-bc0f-287c2a18d702)


#### Question 10: Find the total number of products in each colour.

````sql
SELECT
	Color,
	COUNT(*) AS Totalnumber
FROM [dbo].[DimProduct]
GROUP BY Color;
````
![image](https://github.com/user-attachments/assets/df647568-e727-437b-a3c1-deccf48b8a2a)


#### Question 11: Find the top 10 Customers with the highest number of orders

````sql
SELECT TOP 10
	CONCAT(C.FirstName, ' ', C.LastName) FullName,
	COUNT(*) AS TotalOrders
FROM FactInternetSales SF
	JOIN DimCustomer C
		ON C.CustomerKey = SF.CustomerKey
GROUP BY CONCAT(C.FirstName, ' ', C.LastName)
ORDER BY TotalOrders DESC;
````
![image](https://github.com/user-attachments/assets/e565fe63-b3fb-4a0c-b1fe-6cf7921cc2cd)


#### Question 12: Find the total number of products in each subcategory

````sql
SELECT
	P.ProductSubcategoryKey,
	COUNT(P.ProductKey) AS ProductCount
FROM DimProduct P
	JOIN DimProductSubcategory SB
		ON SB.ProductSubcategoryKey = P.ProductSubcategoryKey
GROUP BY P. ProductSubcategoryKey
ORDER BY 2 DESC;
````
![image](https://github.com/user-attachments/assets/90eba1e5-9f75-4423-ac74-b41a3a4152bd)


#### Question 13: Find the top 5 products with the highest profit margin

````sql
SELECT DISTINCT TOP 5
	P.EnglishProductName,
	SalesAmount,
	TotalProductCost,
	SalesAmount - TotalProductCost AS Profit,
	(SalesAmount - TotalProductCost)/ TotalProductCost * 100 AS ProfitMargin
FROM FactInternetSales SF
	JOIN DimProduct P
		ON SF.ProductKey=P.ProductKey
ORDER BY ProfitMargin DESC;
````
![image](https://github.com/user-attachments/assets/9858d5b8-4910-4f28-b3d6-c5e694e2e5e0)


