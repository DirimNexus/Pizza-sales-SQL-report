# Pizza-sales-report


## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Data summary](#Data_summary)
- [Queries and insights](#Queries_and_insights)
- [Excel dashboard](#Excel_dashboard)
- [Recommendations](#Recommendations)


## Introduction

The Pizza Sales  Report provides valuable insights and analysis into the sales performance of our pizza offerings. 
By querying the database, this report offers a comprehensive overview of key metrics, trends, and patterns related to pizza sales. 
This information aids in making informed decisions about inventory management, pricing strategies, 
and marketing initiatives to optimize our pizza sales.


# Key features in this project.
Report Highlights:
Sales Overview: Gain a holistic view of total pizza sales,
including revenue, quantities sold, and average order value.

Top Selling Pizzas: Identify the most popular pizza flavors and styles, 
helping us understand customer preferences

Time-based Analysis: Analyze sales trends based on different time periods such as daily, 
weekly, and monthly, to spot seasonality and demand patterns.


# Queries and insights.

A)	KPI’s

1)Total Revenue:

SELECT SUM(total_price) AS Total_Revenue 

FROM pizza_sales


   2)Average order value:

 SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Avg_Order_value

 FROM pizza_sales


   3)Total Pizza Sold:

     SELECT SUM(quantity) AS Total_Pizza_Sold 

     FROM pizza_sales


   4)Total Orders:

     SELECT COUNT(DISTINCT order_id) AS Total_Orders 

    FROM pizza_sales

      
   5)Average Pizzas per Order:

   SELECT CAST( CAST(SUM(quantity) AS DECIMAL(12,2)) / CAST(COUNT (DISTINCT order_id)  AS   DECIMAL (10,2)) AS DECIMAL (10,2)) AS Avg_Pizza_Per_Orders 

   FROM pizza_sales


B)	Daily Trend for Total Orders:

SELECT DATENAME( DW, order_date) AS Order_Day, COUNT(DISTINCT order_id) AS Total_Orders

FROM pizza_sales

GROUP BY DATENAME( DW, order_date)

C)	Monthly Trend for Total Orders:

SELECT DATENAME( MONTH, order_date) AS Order_Month, COUNT(DISTINCT order_id) AS Total_Orders

FROM pizza_sales

GROUP BY DATENAME( MONTH, order_date)

  ORDER BY Total_Orders desc


D)	% of Sales by Pizza Category:

SELECT pizza_category,CAST( SUM(total_price) AS DECIMAL(10,2)) AS Total_Sales, 

CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL (10,2)) as PCT 

FROM pizza_sales GROUP BY pizza_category



E)	% of Sales by Pizza Size:

SELECT pizza_size,CAST( SUM(total_price) AS DECIMAL(10,2)) AS Total_Sales, 

CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL (10,2)) AS PCT 

FROM pizza_sales 

GROUP BY pizza_size 

ORDER BY PCT DESC



F)	Total Pizzas Sold by Pizza Category:

SELECT pizza_category, SUM( quantity) AS Total_Quantity_Sold

FROM pizza_sales

GROUP BY pizza_category

ORDER BY Total_Quantity_Sold DESC


G)	Top 5 Best Sellers by Revenue :

SELECT TOP 5 pizza_name,SUM(total_price) AS Total_Revenue

FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Revenue DESC



H)	 Bottom 5 Sellers by Revenue:

SELECT TOP 5 pizza_name,SUM(total_price) AS Total_Revenue

FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Revenue ASC


I)	Top 5 Sellers by Quantity:

SELECT TOP 5 pizza_name,SUM(quantity) AS Total_Pizza_Sold

FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Pizza_Sold DESC


J)	Bottom 5 Sellers by Quantity  :

SELECT TOP 5 pizza_name,SUM(quantity) AS Total_Pizza_Sold

FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Pizza_Sold ASC



 

     

K)	Top 5 Sellers by Total Orders:

SELECT TOP 5 pizza_name,COUNT(DISTINCT order_id) AS Total_Orders

  FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Orders DESC



 





L)	Bottom 5 Sellers by Total Orders:

SELECT TOP 5 pizza_name,COUNT(DISTINCT order_id) AS Total_Orders

FROM pizza_sales

GROUP BY pizza_name

ORDER BY Total_Orders ASC



 





NOTE:

If you want to apply the pizza_category or pizza_size filters to the above queries, you can use a WHERE clause. Follow some of the examples below 

SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders

FROM pizza_sales

WHERE pizza_category = 'Classic'

GROUP BY pizza_name

ORDER BY Total_Orders ASC

Which gives you the output below:

 




# Pizza-sales-SQL-report
