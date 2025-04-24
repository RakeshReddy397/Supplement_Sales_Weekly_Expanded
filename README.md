# Supplement_Sales_Weekly_Expanded -- Create database and table
CREATE DATABASE IF NOT EXISTS supplements;
USE supplements;

CREATE TABLE sales (
    Date DATE,
    Product_Name VARCHAR(100),
    Category VARCHAR(50),
    Units_Sold INT,
    Price DECIMAL(10,2),
    Revenue DECIMAL(10,2),
    Discount DECIMAL(4,2),
    Units_Returned INT,
    Location VARCHAR(50),
    Platform VARCHAR(50)
);

-- Sample Queries for Analysis

-- 1. View first 10 records
SELECT * FROM sales LIMIT 10;

-- 2. Total Revenue by Category
SELECT Category, SUM(Revenue) AS Total_Revenue
FROM sales
GROUP BY Category
ORDER BY Total_Revenue DESC;

-- 3. Weekly Total Units Sold
SELECT Date, SUM(Units_Sold) AS Total_Units
FROM sales
GROUP BY Date
ORDER BY Date;

-- 4. Average Price by Product
SELECT Product_Name, AVG(Price) AS Avg_Price
FROM sales
GROUP BY Product_Name
ORDER BY Avg_Price DESC;

-- 5. Top 5 Products by Revenue
SELECT Product_Name, SUM(Revenue) AS Total_Revenue
FROM sales
GROUP BY Product_Name
ORDER BY Total_Revenue DESC
LIMIT 5;

-- 6. Revenue by Location
SELECT Location, SUM(Revenue) AS Total_Revenue
FROM sales
GROUP BY Location
ORDER BY Total_Revenue DESC;

-- 7. Sales Platform Performance
SELECT Platform, SUM(Revenue) AS Platform_Revenue
FROM sales
GROUP BY Platform
ORDER BY Platform_Revenue DESC;

-- 8. Return Rate Analysis
SELECT Product_Name,
       SUM(Units_Returned) AS Total_Returned,
       SUM(Units_Sold) AS Total_Sold,
       (SUM(Units_Returned) / SUM(Units_Sold)) * 100 AS Return_Percentage
FROM sales
GROUP BY Product_Name
ORDER BY Return_Percentage DESC;
