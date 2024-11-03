# Lita-Capstone-Project-1
## Project Work for incubator hub data analysis training 

### Project title: Retail Stores Sales Analysis 

### Project Objectives 
This project aims to generate insights into the sales performance of a retail store for 2023 to Q3 of 2024. 
This is achievable through a comprehensive analysis of sales data recieved - to identify 
1. monthly sales trends,
2. regional performance,
3. top selling products
4. Calculate matrixes such as
   average sales per product
   total revenue by region
   total sales per month 
5. identify areas of improvement in sales processes.
6. Develop recommendations to improve sales performance and customer engagement.

### Scope:
This project will focus on Analysing sales data from
**Q1 2023  to Q3 2024**. Covering: 
- Sales transactions
- Product categories (Shirt, Shoes, Hat, Socks Jacket and Gloves)
- Store locations (Nouth, East, West and South)
### Methodology
1. **Data Collection**: A documented Excel file - LITA Capstone Dataset.xlsx
2. **Data Cleaning and preprocessing**: ensure data accuracy and consistency use analysis tools (Excel and Power BI), through the following steps
   - Data loading and inspection
   - Handing Missing Variables: Creating Essential column like a column for revenue using product function in excel 
   - Data Cleaning and formatting 
4. **Data Ananlysis**: Apply data vitualisation techniques using analysis tools (Excel and Power BI)
5. **Data Querying**: querying data to extract key insights using SQL (Structutred Query Language) with the aid of of SQL Server.
6. **Findings and Recommendation**: a pdf file containing recommendations documentation   


### Expected Outcomes:
1. A comprehensive sales analysis report highlighting trends and opputunities.
2. Data-Driven recommendations to improve revenue and sales trends 

### Deliverables:
#### Data Analysis
**Some Basic lines of Code - excel functions, SQL quesries and Some DAX expression used during analysis**
**Excel functions**
~~~
=SUMIFS($H$2:$H$50001,$D$2:$D$50001,$D$2,$C$2:$C$50001,$C2)

=AVERAGEIF(C$2:C$50001,C2,H$2:H$50001)
~~~

**SQL QUERIES**
~~~
create database Capstone_project_one;
~~~

~~~
SELECT * FROM [dbo].[LITA_SALES_DATA_PROJECT];

~~~

----- Retrieve total sales for each product categories---

~~~
------ created an addition column for total sales--------
ALTER TABLE [dbo].[LITA_SALES_DATA_PROJECT]
ADD TOTAL_SALES AS (Quantity*UnitPrize)

SELECT * FROM [dbo].[LITA_SALES_DATA_PROJECT];

~~~

------total number of sales transaction in each region----

~~~
SELECT 
Region,
COUNT(Order_ID) AS total_transaction
FROM [dbo].[LITA_SALES_DATA_PROJECT]
GROUP BY 
Region
ORDER BY
total_transaction DESC;
~~~

-----highest selling product-------
~~~
SELECT TOP 1
Product, 
SUM(TOTAL_SALES) AS total_sales
FROM [dbo].[LITA_SALES_DATA_PROJECT]
GROUP BY
Product
ORDER BY
total_sales DESC;
~~~

------total revenue per product------
~~~
SELECT 
Product, 
SUM(TOTAL_SALES) AS total_Revenue
FROM [dbo].[LITA_SALES_DATA_PROJECT]
GROUP BY
Product
ORDER BY
total_Revenue DESC;
~~~

-------- monthly sales for the current year-----
~~~
SELECT 
MONTH(Order_Date) AS monthly_sales,
SUM(TOTAL_SALES) AS total_sales
FROM 
[dbo].[LITA_SALES_DATA_PROJECT]
WHERE 
YEAR(Order_Date) = YEAR(GETDATE())
GROUP BY
MONTH(Order_Date)
ORDER BY
Monthly_sales;
~~~

------- top 5 customers by total purchase amount------
~~~
SELECT TOP 5
Customer_ID,
SUM(TOTAL_SALES) AS total_purchase
FROM
[dbo].[LITA_SALES_DATA_PROJECT]
GROUP BY
Customer_ID
ORDER BY
total_purchase DESC;
~~~

-------- % of total sales contributed by each region------
~~~
SELECT
Region,
SUM(TOTAL_SALES) AS regional_sales,
CONVERT (INT,ROUND((SUM(TOTAL_SALES) * 1.0 / (SELECT SUM(TOTAL_SALES) FROM [dbo].[LITA_SALES_DATA_PROJECT])) * 100, 0)) AS
percentage_sales
FROM 
[dbo].[LITA_SALES_DATA_PROJECT]
GROUP BY
Region
ORDER BY
percentage_sales DESC;
~~~

------- product with no sales at all in the last quater ------
~~~
SELECT 
p.Product,
Count(*) AS Count
FROM 
[dbo].[LITA_SALES_DATA_PROJECT] p
WHERE
p.Product NOT IN (
SELECT
Product FROM
[dbo].[LITA_SALES_DATA_PROJECT] 
WHERE
Order_Date >= DATEADD(quarter, DATEDIFF(quarter, 0, GETDATE())-1,0)
AND Order_Date < DATEADD(quarter, DATEDIFF(quarter,0,GETDATE()),0)
)
GROUP BY
p.Product
~~~


#### Key Findings:
**Data Visualisations**
1. Excel
- Calaculated Tables

  
![Capture 3](https://github.com/user-attachments/assets/a99e0ff6-f71a-4d7b-9722-349664ee6c08)

![Capture 2](https://github.com/user-attachments/assets/460af12d-6f47-49ff-b7c7-dcbde71dcf8b)

![Capture](https://github.com/user-attachments/assets/abb9ae4f-bd4a-4f66-8a2f-aa6a92ded463)



- Pivot Tables

  
![pivot 1](https://github.com/user-attachments/assets/7c531a5c-eda0-49c6-91c2-6dcb99e2d9c0)

![Pivot 2](https://github.com/user-attachments/assets/3b758d11-7d6d-4971-bd5d-4e7b9d7962c7)

![Pivot 3](https://github.com/user-attachments/assets/31d1e2c6-0f24-4324-94f1-1b462f423967)

![pivot 4](https://github.com/user-attachments/assets/3f2e43ed-4180-452f-9bcb-dbe2dd220518)

![pivot 5](https://github.com/user-attachments/assets/878f69e5-94c5-480e-a02b-cc3bc59e728b)

 




  
### Timeline:

- Data analysis: 
- Findings and recommendations:
- Report and presentation preparation: 


### Project Team:

- Data Analyst: Ikupoluyi Justina 


