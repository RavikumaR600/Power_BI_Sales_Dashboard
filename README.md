# Power_BI_Sales_Dashboard

Dashboard Link :https://app.powerbi.com/view?r=eyJrIjoiNTZlOTM1NzAtZjU3ZS00N2Y4LWExMjgtYzYxNTg2YjZmMDQzIiwidCI6IjA2ODE1ZDQwLTJiMDktNDg0Yi05M2IzLTBmOGQxOWJlZmRhOSJ9

**#PROBLEM STATEMENT**

KPI's REQUIREMENT

We need to analyze key indicators for our pizza sales data to gain insights into our business performance. Specifically, we want to calculate the following metrics:

1. Total Revenue: The sum of the total price of all pizza orders.

2. Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.

3. Total Pizzas Sold: The sum of the quantities of all pizzas sold.

4. Total Orders: The total number of orders placed.

5. Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

CHARTS REQUIREMENT
We would like to visualize various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:

1. Daily Trend for Total Orders:
Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.

2.Monthly Trend for Total Orders:
Create a line chart that illustrates the Monthly trend of total orders throughout the month. This chart will allow us to identify peak months or periods of high order activity.
3.Hourly Trend for Total Orders:
Create a line chart that illustrates the Monthly trend of total orders throughout the day. This chart will allow us to identify peak months or periods of high order activity.

4.Percentage of Sales by Pizza Category:
Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

5.Percentage of Sales by Pizza Size:
Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.

6.Total Pizzas Sold by Pizza Category:
Create a funnel chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

7.Top 5 Best Sellers by Revenue, Total Quantity and Total Orders
Create a bar chart highlighting the top 5 best-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will help us identify the most popular pizza options.

8. Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders
Create a bar chart showcasing the bottom 5 worst-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will enable us to identify underperforming or less popular pizza options.

PIZZA SALES SQL QUERRIES for KPI’S

1.	Total Revenue:

select SUM(total_price) as Total_Revenue from pizza_sales
 
2.	Average Order Value:

SELECT SUM(total_price)/ COUNT(DISTINCT order_id) AS Average_Order_Value FROM pizza_sales
 
3.	Total Pizza’s Sold:

SELECT SUM(quantity) AS Total_Pizza_Sold FROM pizza_sales

4.	Total Order:

SELECT COUNT(DISTINCT(order_id)) AS Total_orders FROM pizza_sales

5.	Average Pizza Order:

SELECT CAST(CAST (SUM(quantity) AS decimal(10,2))/ CAST (COUNT(DISTINCT order_id)AS decimal(10,2))AS decimal(10,2)) AS Average_Pizza_Ordered FROM pizza_sales

Daily Trend for Total Orders:
SELECT DATENAME(DW,order_date) AS Order_Day,
COUNT(DISTINCT(order_id)) AS Total_Orders FROM pizza_sales
GROUP BY DATENAME(DW,order_date)
ORDER BY Total_orders desc; 

Monthly Trend for Total Orders:

SELECT DATENAME(MONTH,order_date) AS Order_Month,
COUNT(DISTINCT(order_id)) AS Total_Orders FROM pizza_sales
GROUP BY DATENAME(MONTH,order_date) ORDER BY Total_orders desc;

Hourly Trend for Total Orders:

SELECT DATENAME(HOUR,order_time) AS Order_Time,
COUNT(DISTINCT(order_id)) AS Total_Orders FROM pizza_sales
GROUP BY DATENAME(HOUR,order_time) ORDER BY Total_orders desc;
 
Percentage of Sales by Pizza Category:

SELECT pizza_category, 
SUM(total_price) AS Total_sales, 
CAST(SUM(total_price)*100/
(SELECT SUM (total_price)FROM pizza_sales)AS decimal(10,2)) AS Sales_Percentage
FROM pizza_sales
GROUP BY pizza_category
ORDER BY Sales_Percentage desc;

Percentage of Sales by Pizza Size:

SELECT pizza_size, 
CAST(SUM(total_price)AS decimal(10,2)) AS Total_sales, 
CAST(SUM(total_price)*100/
(SELECT SUM (total_price)FROM pizza_sales) AS decimal(10,2))AS Sales_Percentage
FROM pizza_sales
GROUP BY pizza_size
ORDER BY Sales_Percentage desc;

Total Pizzas Sold by Pizza Category:

SELECT pizza_category, SUM(quantity) AS Total_Pizza_sold FROM pizza_sales
GROUP BY pizza_category;

Top 5 Best Sellers by Revenue, Total Quantity and Total Orders

Top 5 by Revenue/Sales

SELECT TOP 5 pizza_name AS Pizza_Name, 
CAST(SUM(total_price) AS decimal(10,2))AS Total_Sales FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Sales DESC;

Top 5 by Quantity

SELECT TOP 5 pizza_name AS Pizza_Name, 
SUM(quantity) AS Total_Quantity FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity DESC;

Top 5 by total orders

SELECT TOP 5 pizza_name AS Pizza_Name, COUNT(DISTINCT order_id) AS Total_order FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_order DESC; 

Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders

Wrost 5 by Revenue/Sales

SELECT TOP 5 pizza_name AS Pizza_Name, 
CAST(SUM(total_price) AS decimal(10,2))AS Total_Sales FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Sales ASC;

Wrost 5 by total quantity

SELECT TOP 5 pizza_name AS Pizza_Name, 
SUM(quantity) AS Total_Quantity FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity ASC;
 
Wrost 5 by total orders

SELECT TOP 5 pizza_name AS Pizza_Name, 
COUNT(DISTINCT order_id) AS Total_order FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_order ASC;
 
