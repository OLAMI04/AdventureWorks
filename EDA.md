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




