
# Pizza Sales Dashboard




This dashboard helps a Pizza store understand their customers better. It helps the Pizza store know if their customers are satisfied with their pizza quality. Through different ratings, they get to know their improvement area so thus they can improve their quality by identifying these area. 

Since, the data is of January to December of year 2015 so we have a good amount of data to visualize various aspects of our pizza sales data to gain insights and understand key trends.


## Problem Statement

The owner of pizza store wants to create a dashboard in which various trends of orders can be visualized. These trends can be monthly, daily or depends on pizaa name, pizza size or pizza category. 

Now owner wants to calculate some metrics :
- Total Revenue
- Average Order Value
- Total Pizzas Sold
- Total Orders
- Average Pizzas Per Order


Also owner wants to know some trends based on metrics :
- Daily trend for Total Orders
- Monthly trend for Total Orders
- Percentage of Sales by Pizza Category
- Percentage of Sales by Pizza Size
- Pizzas sold by Pizza Category
- Top 5 and Bottom 5 Pizzas by Revenue, Quantity and Total Orders




## About the Dataset

This pizza sales dataset contains 12 relevant features:

- pizza_id: Unique key identifier that ties the pizza ordered to its details, like size and price.

- order_id: Unique identifier for each order placed by a table

- pizza_name_id : Unique identifier for each pizza placed within each order (pizzas of the same type and size are kept in the same row, and the quantity increases)


- quantity: Quantity ordered for each pizza of the same type and size

- order_date: Date the order was placed (entered into the system prior to cooking & serving)

- order_time: Time the order was placed (entered into the system prior to cooking & serving)

- unit_price: Price of the pizza in USD

- total_price: unit_price * quantity

- pizza_size: Size of the pizza (Small, Medium, Large, X Large, or XX Large)

- pizza_category: Unique key identifier that ties the pizza ordered to its details, like size and price

- pizza_ingredients: ingredients used in the pizza as shown in the menu (they all include Mozzarella Cheese, even if not specified; and they all include Tomato Sauce, unless another sauce is specified)

- pizza_name: Name of the pizza as shown in the menu.

## Software Tools Used
- MySQL
- Power BI 

## Dashboard (Power BI Service)

### Page 1
![dashboard1](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/5709ebd4-911e-4dfd-a880-2616be7768fb)


### Page 2
![dashboard2](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/cbf2d192-8af8-4509-849a-74ccc2c7e0ac)

## Steps followed 

### Step 1 
- Importing the dataset in MySQL Database with table data import wizard.
- Writing queries for the calculation of requirements to build dashboard and helps to solve the problem statement.

### Step 2

All Metrics are calculated by the help of SQL queries in MySQL : 

  #### 1. Total Revenue
  The sum of the total price of all pizza orders.

    SELECT SUM(total_price) AS Total_Revenue FROM pizza_sale;

  
  ![total revenue ](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/9ecf0795-1f4f-4a39-ac7e-06aa6b7f357b)


  #### 2. Average Order Value
  The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
  
    SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sale;


  
![Avg_order value](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/3d09b494-4a5f-460c-8f84-a75e0fcf66da)




  #### 3. Total Pizzas Sold
  The sum of the quantities of all pizzas sold.
  
    SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sale;


  ![total pizza](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/c58eaada-88cb-44c7-9011-7159d13b03f3)


  #### 4. Total Orders 
  The total number of orders placed.
  
    SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sale;

  ![total_orders](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/3bd378ae-a789-474d-88e8-1193f3581952)


  #### 5. Average Pizzas Per Order
  The Average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.
  
    SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id)  AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_per_order FROM pizza_sale;

  ![avg_pizza_per_order](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/cbbfadb3-91f8-44a1-b424-b6b0f8949172)


  
  
### Step 3
- Now calculation of various trends is done in this step to get the visualization in dashboard.
- All calculations is done in MySQL with the help of SQL queries.

#### 1. Daily Trend for Total Orders

Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identity any patterns or fluctuations in order volumes on a daily basis.


    SELECT DAYNAME(order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders FROM pizza_sale GROUP BY  DAYNAME(order_date);


![order_day](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/f9b41e66-a780-4435-ad6e-6bb03b1012d8)



 #### 2. Monthly Trend for Total Orders

Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.


    SELECT MONTHNAME(order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders FROM pizza_sale GROUP BY  MONTHNAME(order_date);

![month_wise](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/e1ffdc46-a086-4e93-bd3e-0a8cee03c713)


#### 3. Percentage of Sales by Pizza Category

Create a pie chart that displays the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.


    SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue, CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sale) AS DECIMAL(10,2)) AS percentage FROM pizza_sale GROUP BY pizza_category


![percentage_by_pizza_category](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/27190ced-69b8-46eb-9ba2-63bdc9e3db7e)


#### 4. Percentage of Sales by Pizza Size

Generate a pie chart that represents the percentage of sales attributes to different pizza sizes. This chart will help us understand customer preference for pizza sizes and their impact on sales.


    SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue, CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sale) AS DECIMAL(10,2)) AS percentage FROM pizza_sale GROUP BY pizza_size ORDER BY pizza_size


![percentage_by_pizza_size](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/de87055d-f9ad-405d-bc02-d8c8ea72ba3b)



#### 5. Percentage of Sales by Pizza Category

Create a funner chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

    SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold FROM pizza_sale GROUP BY pizza_category ORDER BY Total_Quantity_Sold DESC


![percentage_by_pizza_category](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/d11b3b5e-4fd9-43d2-b1a8-acde5d72f1f7)


#### 6. Top 5 Best sellers by Revenue, Total Quantity and Total Orders 


- By Revenue

      SELECT pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Revenue DESC LIMIT 5

![revenue_top_5](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/0775bc1a-0d6f-44c3-8b6f-5ac09d75b998)



- By Total Quantity

      SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold FROM pizza_sale GROUP BY  pizza_name ORDER BY Total_Pizza_Sold DESC LIMIT 5

 ![top 5 by quantity](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/55709471-cdf0-4d1d-8b3e-81a8e42b9adb)
8)


- By Total Orders

      SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Orders DESC LIMIT 5

![top 5 by total orders](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/d3b765cc-0748-4b01-a064-18e3d7e74a68)



#### 7. Bottom 5 Best sellers by Revenue, Total Quantity and Total Orders 


- By Revenue

      SELECT pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Revenue LIMIT 5

 

 ![bottom 5_by revenue](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/52ecfae4-31c3-4d3e-b142-31dc673bb3e6)



- By Total Quantity

      SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold FROM pizza_sale GROUP BY  pizza_name ORDER BY Total_Pizza_Sold LIMIT 5

 

![bottom 5_by quantity](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/eb88c225-f69c-42ff-9bea-7d0350628f35)


- By Total Orders

      SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Orders  LIMIT 5

  

![bottom 5_by total orders](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/23f4f9df-ad61-4dea-be32-30255d05cefe)



  
  ### Step 3
  - After the Calculation of metrics and trends requirements , we go to the Power BI Desktop Software.
  - We will get the dataset by connecting the Power BI with MySQL server so that we can transform the data and start making dashboard.
  - For the Dashboard, different types of visualization method are used:

  #### 1. Cards 

  - Cards are used to show different requirement values.
  - All metrics are shown in dashboard using cards - Total Revenue, Average Order Value, Total Pizzas Sold, Total Orders, Average Pizzas Per Order
  - All metrics measures are calculated as :

                Total Revenue = SUM('pizza_sales'[total_price])
    
                Average Order Value = [Total Revenue]/[Total Orders]
    
                Total Pizzas Sold = SUM(pizza_sales[quantity])
    
                Average Pizza per Order = [Total Pizzas Sold]/[Total Orders]
    
                Total Orders = DISTINCTCOUNT(pizza_sales[order_id])



![cards](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/5292a4e5-935e-4880-bdfb-cc9432db4d4c)



  #### 2. Trend Charts

  - To visualize various Trend charts, we use rectangle with round corners.
  - All trend charts are visualized in the dashboard -  Daily trend for Total Orders, Monthly trend for Total Orders, Percentage of Sales by Pizza Category, Percentage of Sales by Pizza Size, Pizzas sold by     Pizza Category


![Trends chart](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/d9abf7ad-5f07-4d3a-9d5f-390552aa796c)

  - For the Visualization of the Monthly Trend for Total Orders chart , a new column named 'Order Month' is created using DAX expression:
  
        
        Order Month = UPPER(LEFT(pizza_sales[Month Name],3))


  - For the Visualization of the Daily Trend for Total Orders chart , a new column named 'Order Day' is created using DAX expression:
  
        
        Order Day = UPPER(LEFT(pizza_sales[Day Name],3))

  - For the Visualization of Percentage Sales by Pizza Category Pie Chart and Percentage Sales by Pizza Size, we took Total Revenue as value which was distributed by categories and sizes.
  - For the Viasualization of Total Pizzas sold by Category, we created a line chart between category and Total Pizzas Sold.


  #### 3. Top 5 and Bottom 5 Pizzas by Revenue, Quantity and Total Orders 

  - To Visualize the Top 5 and Bottom 5 pizzas by Revenue, we created a new measure by DAX expression:
  
        Total Revenue = SUM('pizza_sales'[total_price])

  - To Visualize the Top 5 and Bottom 5 pizzas by Quantity, we created Total Pizzas Sold measure by DAX expression:
  
        Total Pizzas Sold = SUM(pizza_sales[quantity])

  - To Visualize the Top 5 and Bottom 5 pizzas by Total Order, a new measure created by DAX expression:
  
        Total Orders = DISTINCTCOUNT(pizza_sales[order_id])

    ###### Snapshot of Top 5 and Bottom 5 Dashboard:

    ![top and bottom](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/4206e038-af7c-4cda-910a-90b745572e8a)




## Insights

### Dataset 

- Total number of rows in the Dataset = 48620
- Total number of columns in the Dataset = 12

### Metrics 
- Total Revenue = 817860 USD
- Average Order Value = 38.31
- Total Pizzas Sold = 49574 
- Average Pizza per Order = 2.32
- Total Orders = 21350 

### Market Trends 

- Highest orders are given on Friday = 3538
- Highest orders are given in July = 1935
- Classic Pizza has generated maximum revenue = 26.91% of Total Revenue
- Large size Pizza created maximum revenue by percentage = 45.89%
- Highest orders are of classic pizza = 14888

### Numbers
- The Thigh Chicken Pizza contributes in making highest revenue = 43434.25 USD
- The Classic Delux Pizza is sold by maximum quantity = 2453
- The Brie Carre Pizza contributes to minimum revenue and sold by minimum quantity as well = 11588.50 USD and 490 pizzas


