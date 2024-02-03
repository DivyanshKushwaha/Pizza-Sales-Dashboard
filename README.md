
# Pizza Sales Dashboard




This dashboard helps a Pizza store understand their customers better. It helps the Pizza store know if their customers are satisfied with their pizza quality. Through different ratings, they get to know their improvement area so thus they can improve their quality by identifying these area. 

Since, the data is of 11 months from January to December of year 2015 so we have a good amount of data to visualize various aspects of our pizza sales data to gain insights and understand key trends.


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



## Steps followed 

### Step 1 
- Importing the dataset in MySQL Database.
- Writing queries for the calculation of requirements to build dashboard and helps to solve the problem statement.

### Step 2

All Metrics are calculated by the help of SQL queries in MySQL : 

  #### 1. Total Revenue
  The sum of the total price of all pizza orders.
  #### SELECT SUM(total_price) AS Total_Revenue FROM pizza_sale;

  
  ![total revenue ](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/9ecf0795-1f4f-4a39-ac7e-06aa6b7f357b)


  #### 2. Average Order Value
  The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
  #### SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sale;


  
![Avg_order value](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/3d09b494-4a5f-460c-8f84-a75e0fcf66da)




  #### 3. Total Pizzas Sold
  The sum of the quantities of all pizzas sold.
  #### SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sale;


  ![total pizza](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/c58eaada-88cb-44c7-9011-7159d13b03f3)


  #### 4. Total Orders 
  The total number of orders placed.
  #### SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sale;

  ![total_orders](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/3bd378ae-a789-474d-88e8-1193f3581952)


  #### 5. Average Pizzas Per Order
  The Average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.
  #### SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id)  AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_per_order FROM pizza_sale;

  ![avg_pizza_per_order](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/cbbfadb3-91f8-44a1-b424-b6b0f8949172)


  
  
### Step 3
- Now calculation of various trends is done in this step to get the visualization in dashboard.
- All calculations is done in MySQL with the help of SQL queries.

#### 1. Daily Trend for Total Orders

Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identity any patterns or fluctuations in order volumes on a daily basis.

#### SELECT DAYNAME(order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders FROM pizza_sale GROUP BY  DAYNAME(order_date);


![order_day](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/f9b41e66-a780-4435-ad6e-6bb03b1012d8)



 #### 2. Monthly Trend for Total Orders

Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.

#### SELECT MONTHNAME(order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders FROM pizza_sale GROUP BY  MONTHNAME(order_date);

![month_wise](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/e1ffdc46-a086-4e93-bd3e-0a8cee03c713)


#### 3. Percentage of Sales by Pizza Category

Create a pie chart that displays the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

#### SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue, CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sale) AS DECIMAL(10,2)) AS percentage FROM pizza_sale GROUP BY pizza_category


![percentage_by_pizza_category](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/27190ced-69b8-46eb-9ba2-63bdc9e3db7e)


#### 4. Percentage of Sales by Pizza Size

Generate a pie chart that represents the percentage of sales attributes to different pizza sizes. This chart will help us understand customer preference for pizza sizes and their impact on sales.

#### SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue, CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sale) AS DECIMAL(10,2)) AS percentage FROM pizza_sale GROUP BY pizza_size ORDER BY pizza_size


![percentage_by_pizza_size](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/de87055d-f9ad-405d-bc02-d8c8ea72ba3b)



#### 5. Percentage of Sales by Pizza Category

Create a funner chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

#### SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold FROM pizza_sale GROUP BY pizza_category ORDER BY Total_Quantity_Sold DESC


![percentage_by_pizza_category](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/d11b3b5e-4fd9-43d2-b1a8-acde5d72f1f7)


#### 6. Top 5 Best sellers by Revenue, Total Quantity and Total Orders 


- By Revenue

 #### SELECT pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Revenue DESC LIMIT 5

![revenue_top_5](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/0775bc1a-0d6f-44c3-8b6f-5ac09d75b998)



- By Total Quantity

 #### SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold FROM pizza_sale GROUP BY  pizza_name ORDER BY Total_Pizza_Sold DESC LIMIT 5

 ![top 5 by quantity](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/55709471-cdf0-4d1d-8b3e-81a8e42b9adb)
8)


- By Total Orders
  #### SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Orders DESC LIMIT 5

![top 5 by total orders](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/d3b765cc-0748-4b01-a064-18e3d7e74a68)



#### 7. Bottom 5 Best sellers by Revenue, Total Quantity and Total Orders 


- By Revenue

 #### SELECT pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Revenue LIMIT 5

 

 ![bottom 5_by revenue](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/52ecfae4-31c3-4d3e-b142-31dc673bb3e6)



- By Total Quantity

 #### SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold FROM pizza_sale GROUP BY  pizza_name ORDER BY Total_Pizza_Sold LIMIT 5

 

![bottom 5_by quantity](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/eb88c225-f69c-42ff-9bea-7d0350628f35)


- By Total Orders
  #### SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sale GROUP BY pizza_name ORDER BY Total_Orders  LIMIT 5

  

![bottom 5_by total orders](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/23f4f9df-ad61-4dea-be32-30255d05cefe)



  
  ### Step 3
  - After the Calculation of metrics and trends requirements , we go to the Power BI Desktop Software .
  - For the Dashboards, different types of visualization method are used:

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


  ![trends](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/1efb92ea-c326-4140-a12d-7c4b69f2c9d1)

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

    ![top 5](https://github.com/DivyanshKushwaha/Pizza-Sales-Dashboard/assets/121238698/5bd1d086-6d73-4604-af0f-c5038a853aaf)



## Insights



  (g) In-flight Service
  
  (h) In-flight wifi service
  
  (i) Leg Room service
  
  (j) On-board service
  
  (k) Online boarding
  
  (l) Seat comfort
  
  (m) Departure & arrival time convenience
  
In our dataset, Some parameters were assigned value 0, representing those parameters are not applicable for some customers.

All these values have been ignored while calculating average rating for each of the parameters mentioned above.

- Step 12 : In the report view, under the insert tab, two text boxes were added to the canvas, in one of them name of the airlines was mentioned & in the other one company's tagline was written.
- Step 13 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area. 
- Step 14 : Calculated column was created in which, customers were grouped into various age groups.

for creating new column following DAX expression was written;
       
        Age Group = 
        
        if(airline_passenger_satisfaction[Age]<=25, "0-25 (25 included)",
        
        if(airline_passenger_satisfaction[Age]<=50, "25-50 (50 included)",
        
        if(airline_passenger_satisfaction[Age]<=75, "50-75 (75 included)",
        
        "75-100 (100 included)")))
        
Snap of new calculated column ,

![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)

        
- Step 15 : New measure was created to find total count of customers.

Following DAX expression was written for the same,
        
        Count of Customers = COUNT(airline_passenger_satisfaction[ID])
        
A card visual was used to represent count of customers.

![Snap_Count](https://user-images.githubusercontent.com/102996550/174090154-424dc1a4-3ff7-41f8-9617-17a2fb205825.jpg)

        
 - Step 16 : New measure was created to find  % of customers,
 
 Following DAX expression was written to find % of customers,
 
         % Customers = (DIVIDE(airline_passenger_satisfaction[Count of Customers], 129880)*100)
 
 A card visual was used to represent this perecntage.
 
 Snap of % of customers who preferred business class
 
 ![Snap_Percentage](https://user-images.githubusercontent.com/102996550/174090653-da02feb4-4775-4a95-affb-a211ca985d07.jpg)

 
 - Step 17 : New measure was created to calculate total distance travelled by flights & a card visual was used to represent total distance.
 
 Following DAX expression was written to find total distance,
 
         Total Distance Travelled = SUM(airline_passenger_satisfaction[Flight Distance])
    
 A card visual was used to represent this total distance.
 
 
 ![Snap_3](https://user-images.githubusercontent.com/102996550/174091618-bf770d6c-34c6-44d4-9f5e-49583a6d5f68.jpg)
 
 - Step 18 : The report was then published to Power BI Service.
 
 
![Publish_Message](https://user-images.githubusercontent.com/102996550/174094520-3a845196-97e6-4d44-8760-34a64abc3e77.jpg)

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

 
 # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload](https://user-images.githubusercontent.com/102996550/174074051-4f08287a-0568-4fdf-8ac9-6762e0d8fa94.jpg)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 129880

   Number of satisfied Customers (Male) = 28159 (21.68 %)

   Number of satisfied Customers (Female) = 28269 (21.76 %)

   Number of neutral/unsatisfied customers (Male) = 35822 (27.58 %)

   Number of neutral/unsatisfied customers (Female) = 37630 (28.97 %)


           thus, higher number of customers are neutral/unsatisfied.
           
### [2] Average Ratings

    a) Baggage Handling - 3.63/5
    b) Check-in Service - 3.31/5
    c) Cleanliness - 3.29/5
    d) Ease of online booking - 2.88/5
    e) Food & Drink - 3.21/5
    f) In-flight Entertainment - 3.36/5
    g) In-flight service - 3.64/5
    h) In-flight Wifi service - 2.81/5
    i) Leg room service - 3.37/5
    j) On-board service - 3.38/5
    k) Online boarding - 3.33/5
    l) Seat comfort - 3.44/5
    m) Departure & arrival convenience - 3.22/5
  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Average Delay 
  
      a) Average delay in arrival(minutes) - 15.09
      b) Average delay in departure(minutes) - 14.71
Average delay will change if different visual filters will be applied.

 ### [4] Some other insights
 
 ### Class
 
 1.1) 47.87 % customers travelled by Business class.
 
 1.2) 44.89 % customers travelled by Economy class.
 
 1.3) 7.25 % customers travelled by Economy plus class.
 
         thus, maximum customers travelled by Business class.
 
 ### Age Group
 
 2.1)  21.69 % customers belong to '0-25' age group.
 
 2.2)  52.44 % customers belong to '25-50' age group.
 
 2.3)  25.57 % customers belong to '50-75' age group.
 
 2.4)  0.31 % customers belong to '75-100' age group.
 
         thus, maximum customers belong to '25-50' age group.
         
### Customer Type

3.1) 18.31 % customers have customer type 'First time'.

3.2) 81.69 % customers have customer type 'returning'.
       
       thus, more customers have customer type 'returning'.

### Type of travel

4.1) 69.06 % customers have travel type 'Business'.

4.2) 30.94 % customers have travel type 'Personal'.

        thus, more customers have travel type 'Business'.
# Airlines-Dashboard.md.txt
Displaying # Airlines-Dashboard.md.txt.
