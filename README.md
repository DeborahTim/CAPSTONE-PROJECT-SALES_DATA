# SALES DATA
## PROJECT TITLE: Unique Hub Sales Performance Analysis
### Project Overview
This project seeks to evaluate and improve the organization’s sales strategies by systematically analyzing sales data. Through the tracking and analysis of key performance indicators (KPIs), we aim to understand patterns, identify strengths and weaknesses, and refine our sales operations. By leveraging the provided data, I will extract insights that will drive targeted strategies for increased revenue, enhanced customer engagement, and optimized resource management. The Sales Performance Analysis will be an invaluable initiative, equipping our sales teams with insights and tools to improve efficiency and drive sustainable growth.

Building on the data and capstone project document previously shared, I will analyze the sales performance of a retail store, using an exploratory approach to uncover key insights such as:

- Top Selling Products
- Regional Performances
- Monthly Sales Trend and By telling a compelling story and building an interactive dashboard.
  
### DATA DESCRIPTION:
This dataset includes the following Columns:

- Order Number
- Customer Id
- Products
- Region
- Order Date
- Quantity
- Unit Price
  
### DASH BOARD REVIEW:
1. Customer Id
products: Items sold in the store
2. Region: The other regional branches of the store ( North, South, East West)
3. Order Date: Date order was palced
4. Quantity: The number of units of the product ordered in each transaction
5. Unit Price: The aquisition cost per unit of the product
   
### Data Sources
The primary source of Data used here is the Sales Data provided by the Sales department of the company. The Data given is table having an array of columns like OrderID, Customer Id, Product, Region, OrderDate, Quantity Sold and UnitPrice image

### Tools used
- Microsoft Excel for Data cleaning transformation and preliminary analysis [Download Here](http://www.Microsoft.com)
- Structured Query Language(SQL) for Data exctraction and for query [Download Here](https://dev.mysql.com/downloads/mysql/)
- Microsoft PowerBI for visualization and Dashboard creation [Download Here](https://powerbi.microsoft.com/desktop/)
- Github for portfolio building [Download Here](https://desktop.github.com/)
  
### Data cleaning and preparations
1. Data Cleaning: I removed duplicates and standardized date formats.

2. Pivot Tables: I created pivot tables to analyze sales by product, region, and period,Total Revenue By Product

3. Visualization:I used charts to visualize The most Popular

### Exploratory Data Analysis
This analysis will involve a deep exploration of the data to answer key questions that are essential for effective decision-making. These include:

Determining the total sales for each product category

Counting the number of sales transactions in each region

Identifying the highest-selling product based on total sales value

Calculating the total revenue for each product

Summing monthly sales totals for the current year

Finding the top 5 customers by total purchase amount

Calculating each region’s percentage contribution to total sales

Identifying products with no sales in the last quarter

### Insight Generation 
Regional Sales (Revenue) Insights

South Region: Leading in total sales, the South region brings in $4,675,000, indicating both high transaction volumes and larger average sales values, positioning it as the top-performing region.

East Region: The East region follows with a strong performance, generating $2,450,000 in total sales, which makes up about 23.14% of overall revenue. This highlights a competitive and active market in this region.

North Region: With total sales of $1,950,000, the North region contributes 18.42% of the overall revenue, reflecting consistent customer engagement and a reliable demand for the store's offerings.

West Region: The West region shows steady competitive activity, closely aligning with the North's performance. It records $1,512,500 in total sales, accounting for 14.29% of total revenue, and suggests a stable purchasing trend in this area.

### Query for the sales data
```
SELECT *FROM [dbo].[LITA Capstone Dataset_SalesData]
```
```
SELECT Product, 
   SUM([Revenue]) AS TotalRevenue
FROM [LITA Capstone Dataset_SalesData]
GROUP BY Product;
```

```
SELECT 
DATENAME(MONTH, OrderDate) AS SalesMonth, 
SUM([Quantity_Sold]) AS TotalSales
FROM 
[dbo].[LITA Capstone Dataset_SalesData]
WHERE 
YEAR(OrderDate) = YEAR(GETDATE()) 
GROUP BY 
DATENAME(MONTH, OrderDate), MONTH(OrderDate)
ORDER BY 
MONTH(OrderDate);  
```

```
SELECT TOP 5 [CustomerName] , 
   SUM([Revenue]) AS TotalPurchaseAmount
FROM [dbo].[LITA Capstone Dataset_CustomerData]
GROUP BY [CustomerName]
ORDER BY TotalPurchaseAmount DESC;
```

```
SELECT Region, 
   SUM([Quantity_Sold]) AS TotalSales, 
   ROUND((SUM([Quantity_Sold]) * 100 / (SELECT SUM([Quantity_Sold])
   FROM [dbo].[LITA Capstone Dataset_SalesData])), 2) AS SalesPercentage
FROM [dbo].[LITA Capstone Dataset_SalesData]
GROUP BY Region;
```

```
SELECT Product
FROM [dbo].[LITA Capstone Dataset_SalesData]
WHERE Product NOT IN (
SELECT DISTINCT Product
FROM [dbo].[LITA Capstone Dataset_SalesData]
WHERE OrderDate >= DATEADD(QUARTER, -1, GETDATE()) 
)
GROUP BY Product;
```




