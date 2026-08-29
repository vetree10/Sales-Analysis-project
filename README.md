# Sales-Analysis-project
Did an analysis on business sales for a company between december 2010 and december 2011


"Missing Customer IDs"
SELECT COUNT(*) AS Missing_CustomerIDs
FROM Sales_Final
WHERE CustomerID IS NULL;

"Find Duplicate Transactions"
SELECT 
    InvoiceNo,
    StockCode,
    Description,
    Quantity,
    InvoiceDate,
    UnitPrice,
    CustomerID,
    Country,
    COUNT(*) AS Duplicate_Count
FROM Sales_Final
GROUP BY 
    InvoiceNo,
    StockCode,
    Description,
    Quantity,
    InvoiceDate,
    UnitPrice,
    CustomerID,
    Country
HAVING COUNT(*) > 1;

"Total Revenue"
SELECT 
    SUM(Quantity * UnitPrice) AS Total_Revenue
FROM Sales_Final
WHERE TransactionType = 'Sale'
  AND UnitPrice > 0;

"Revenue Bu Country"
  SELECT 
    Country,
    SUM(Quantity * UnitPrice) AS Revenue
FROM Sales_Final
WHERE TransactionType = 'Sale'
  AND UnitPrice > 0
  AND Country IS NOT NULL
GROUP BY Country
ORDER BY Revenue DESC;

"Top 10 Products by Revenue"
SELECT 
    Description,
    SUM(Quantity * UnitPrice) AS Revenue
FROM Sales_Final
WHERE TransactionType = 'Sale'
  AND UnitPrice > 0
  AND Description IS NOT NULL
GROUP BY Description
ORDER BY Revenue DESC
LIMIT 10;

"Top 10 Customers by Revenue"
SELECT 
    CustomerID,
    SUM(Quantity * UnitPrice) AS Revenue
FROM Sales_Final
WHERE TransactionType = 'Sale'
  AND CustomerID IS NOT NULL
  AND UnitPrice > 0
GROUP BY CustomerID
ORDER BY Revenue DESC
LIMIT 10;

"Average Revenue By country"
SELECT
    Country,
    AVG(Quantity * UnitPrice) AS Average_Revenue
FROM Sales_Final
WHERE TransactionType = 'Sale'
  AND UnitPrice > 0
  AND Country IS NOT NULL
GROUP BY Country
ORDER BY Average_Revenue DESC;
