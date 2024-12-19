# PIZZA_HUT ORDERS ANALYSIS USING SQL

### DATASETS:

Pizzas:https://1drv.ms/x/c/afc4a61c311d62e8/Ec-ASmio7hhPhLY1eAjdhfEB1NmXZTBXqPtQGTuz0U0XrQ?e=xYD0Zw

Pizza_types:https://1drv.ms/x/c/afc4a61c311d62e8/EfJRBzf8dH1CmNn4Ffx9eNYB-SD1KD7rqRO4DKsmLhB5Pg?e=pRd0b1

Orders:https://1drv.ms/x/c/afc4a61c311d62e8/EXexvil57gNBqsOX_oD30vwB8vRSEVSRSMA3Tb6F5eM8BA?e=hDciee

Orders_details:https://1drv.ms/x/c/afc4a61c311d62e8/EQb9ayR2u5xOqdVhxR1HOhgBZ0k9WQZ6ONBQ-W8_Bf01rg?e=25G6gH

---
## Problem Statement  

This project analyzes Pizza Hut's order data to uncover insights regarding total orders, revenue, popular pizza sizes, and category-wise performance. These insights assist in understanding customer preferences and improving operational efficiency.


---

### QUESTIONS ANS ANSWERS


**QUESTION**: Retrieve the Total Number of Orders Placed
            
    SELECT COUNT(order_id) AS 'Total Orders'  
    FROM orders;  




**QUESTION**: Calculate the Total Revenue Generated from Pizza Sales
    
    SELECT  
    ROUND(SUM(orders_details.quantity * pizzas.price), 2) AS total_sales  
    FROM orders_details  
    JOIN pizzas  
    ON pizzas.pizza_id = orders_details.pizza_id;  


**QUESTION**:  Identify the Highest-Priced Pizza

    SELECT pizza_types.name, pizzas.price  
    FROM pizzas  
    JOIN pizza_types  
    ON pizzas.pizza_type_id = pizza_types.pizza_type_id  
    ORDER BY pizzas.price DESC LIMIT 1;  


**QUESTION**:Identify the Most Common Pizza Size Ordered

    SELECT quantity, COUNT(order_detail_id)  
    FROM orders_details  
    GROUP BY quantity;  

    SELECT pizzas.size, COUNT(orders_details.order_detail_id)  
    FROM pizzas  
    JOIN orders_details  
    ON pizzas.pizza_id = orders_details.pizza_id  
    GROUP BY pizzas.size  
    LIMIT 1;  

**QUESTION**: List the Top 5 Most Ordered Pizza Types Along with Their Quantities

    SELECT pizza_types.name, orders_details.quantity  
    FROM pizza_types  
    JOIN pizzas  
    ON pizza_types.pizza_type_id = pizzas.pizza_type_id  
    JOIN orders_details  
    ON orders_details.pizza_id = pizzas.pizza_id;  



**QUESTION**: Find the Total Quantity of Each Pizza Category Ordered

    SELECT pizza_types.category,  
    SUM(orders_details.quantity) AS 'Quantity'  
    FROM pizza_types  
    JOIN pizzas  
    ON pizza_types.pizza_type_id = pizzas.pizza_type_id  
    JOIN orders_details  
    ON orders_details.pizza_id = pizzas.pizza_id  
    GROUP BY pizza_types.category  
    ORDER BY Quantity DESC;  


**QUESTION**: Determine the Distribution of Orders by Hour of the Day

    SELECT HOUR(order_time) AS hour,  
    COUNT(order_id) AS order_count  
    FROM orders  
    GROUP BY HOUR(order_time);  


**QUESTION**: Find the Category-Wise Distribution of Pizzas

    SELECT category, COUNT(name)  
    FROM pizza_types  
    GROUP BY category;  


**QUESTION**:  Group Orders by Date and Calculate the Average Number of Pizzas Ordered Per Day

    SELECT orders.order_date,  
    SUM(orders_details.quantity)  
    FROM orders  
    JOIN orders_details  
    ON orders.order_id = orders_details.order_id  
    GROUP BY orders.order_date;  



### [7] TOOLS USED

SQL Server Management Studio (SSMS)

SQL for querying and analysis


---
### FUTURE ACTIONS

This project can be extended by integrating the results into a dashboard using tools like Power BI for enhanced visualization and real-time decision-making.

