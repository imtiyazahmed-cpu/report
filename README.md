# Pizza Sales Report

## DASHBOARD LINK: https://swanseauniversity-my.sharepoint.com/:u:/r/personal/2354677_swansea_ac_uk/Documents/NEW%20REPORT.pbix?csf=1&web=1&e=EuQdp9
## PROBLEM STATEMENT 
1.⁠ ⁠Total Revenue: The sum of the total price of all pizza orders.

2.⁠ ⁠Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.

3.⁠ ⁠Total Pizzas Sold: The sum of the quantities of all pizzas sold.

4.⁠ ⁠Total Orders: The total number of orders placed.

5.⁠ ⁠Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.



## CHART REQUIRMENTS 
1.Daily Trend for Total Orders:
Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identity any patterns or fluctuations in order volumes on a daily basis.

2.Monthly Trend for Total Orders:
Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.

3.Percentage of Sales by Pizza Category:
Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

4.⁠ ⁠Percentage of Sales by Pizza Size:
Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.

5.⁠ ⁠Total Pizzas Sold by Pizza Category:
Create a funnel chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

6.⁠ ⁠Top 5 Best Sellers by Revenue, Total Quantity and Total Orders
Create a bar chart highlighting the top 5 best-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will help us identify the most popular pizza options.

7.⁠ ⁠Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders
Create a bar chart showcasing the bottom 5 worst-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will enable us to identity underperforming or less popular pizza options.


## STEP FOLLOWED 

1)	Total revenue:
                 
        SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales

   "https://github.com/user-attachments/assets/1248688a-7f97-45c0-bcda-ad9e138e40d3"


2) 	Average order values:
             
        SELECT SUM(total_price) / COUNT(DISTINCT order_id) as Avg_Order_value from pizza_sales

"https://github.com/user-attachments/assets/c15fca7c-25c0-4b0f-b28c-88f977ef0de0" />




 
3)	 Total pizza sold:
    SELECT SUM(quantity) as total_pizza_sold from pizza_sales.
"https://github.com/user-attachments/assets/f1b991f4-f1ca-433f-9576-8e69a651a80c"

        

4)	Total orders:

        SELECT COUNT(DISTINCT order_id) as total_orders from pizza_sales.

"https://github.com/user-attachments/assets/346342a5-0e0a-437b-94cb-4df12745eeb3" 
 

5)	Avg pizza per order:

        SELECT SUM(quantity) / COUNT(DISTINCT order_id) as avg_pizza_per_order from pizza_sales

"https://github.com/user-attachments/assets/3560a384-38aa-40f9-8d5f-653649f33e81"
 


6)	Avg pizza sales:

        SELECT CAST (CAST(SUM(quantity)AS DECIMAL(10,2)) /
        CAST (COUNT(DISTINCT order_id) AS DECIMAL (10,2)) AS DECIMAL(10,2)) AS   AVG_pizza_per_order from pizza_sales

![WhatsApp Image 2024-12-30 at 04 57 25](https://github.com/user-attachments/assets/1b57dc55-1380-41c1-847d-1da978412fb1)


## ORDER VALUES

1)	Total order: Daily trend for total orders

        SELECT DATENAME(DW, order_date) as order_day,  COUNT (DISTINCT order_id) AS Total_orders
        from pizza_sales
        GROUP BY DATENAME(DW, order_date)
 
 ![WhatsApp Image 2024-12-30 at 05 09 02](https://github.com/user-attachments/assets/22c43912-af74-4b26-a0fa-39bb5ab787da)


2)	Total order per month and highest: hourly trend  for total order 

        SELECT DATENAME(MONTH, order_date) AS month_name, COUNT(DISTINCT order_id) AS total_orders
        FROM pizza_sales
        GROUP BY DATENAME(MONTH, order_date)
        ORDER BY Total_orders DESC

DESC represents the highest no of order according to months 

![WhatsApp Image 2024-12-30 at 05 17 55](https://github.com/user-attachments/assets/4e70162b-998f-443f-9284-374e73fa0385)
 





3)	Total pizza sales of different catagories and PCT:

        SELECT pizza_category, sum(total_price) as total_sales,  sum(total_price) * 100 / (SELECT sum(total_price) from pizza_sales) AS PCT
        from pizza_sales AS total_SALES
        WHERE MONTH(order_date)=1  
        GROUP BY pizza_category


 ![WhatsApp Image 2024-12-31 at 17 33 10](https://github.com/user-attachments/assets/70143430-b869-4745-b02f-39b01acc2fd0)


 "https://github.com/user-attachments/assets/79d20bb6-1a34-4fb0-8574-84375b6b5a05" />



4) % of Sales by Pizza Size:

       SELECT pizza_Size, CAST(SUM(total_price) AS DECIMAL (10,  2)) as total revenue,
       CAST (SUM(total_price) * 100 / (SELECT SUM(total_price)   from pizza_sales)
       AS DECIMAL (10,2)) AS PCT
       FROM pizza_sales
       GROUP BY pizza_size
       ORDER BY pizza_size

    
"https://github.com/user-attachments/assets/b2cf6a43-1fc4-4a6d-bcf0-40d466555e3a" />
             

5)	Top 5 pizza revenue:

         SELECT TOP 5 pizza_name, SUM(TOTAL_PRICE) AS total_Revenue FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY total_revenue DESC for top 5 and ASC for bottom 5


![WhatsApp Image 2025-01-09 at 01 49 17](https://github.com/user-attachments/assets/765c82b0-25a0-4701-b852-4269222472bd)
             
6) Bottom 5 Pizza Revenue:  

       SELECT Top 5 pizza_name, SUM(total_price) AS  total_revenue Revenue
       FROM pizza_sales
       GROUP BY pizza_name
       ORDER BY Total_Revenue ASC
 

![WhatsApp Image 2025-01-09 at 01 50 32](https://github.com/user-attachments/assets/ed1fae0e-9e37-453a-936c-b3f385c78b08)


          

7)	Top 5 pizza by quantity:

                SELECT TOP 5 pizza_name, SUM(quantity) AS total_quantity FROM pizza_sales
        GROUP BY pizza_name ORDER BY total_quantity DESC and ASC for bottom 5



 ![WhatsApp Image 2025-01-09 at 01 53 30](https://github.com/user-attachments/assets/3aa75d12-f97e-4748-9d15-84e858571f20)


8)	Total orders:
        
         SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS total_orders FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY total_orders DESC

![WhatsApp Image 2025-01-09 at 01 54 50](https://github.com/user-attachments/assets/9a2aa23f-f6aa-4f7b-a9c1-799a76ffeaa4)

              


  

          
