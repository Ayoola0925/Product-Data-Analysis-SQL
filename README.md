### Product-Data-Analysis-SQL



## Table of Contents

- [Introduction](introduction)

- [Project Objectives](project-objectives)

- [Data Overview](data-overview)

- [SQL Queries and Analysis](sql-queries-and-analysis)

  [TOP-SELLING PRODUCTS BY QUANTITY](top-selling-products-by-quantity)

  [PRODUCTS GENERATING HIGHEST REVENUE](products-generating-the-highest-revenue)

  [NUMBER OF UNIQUE PRODUCT SOLD](number-of-unique-products-sold)

  [AVERAGE SELLING PRICE PER PRODUCT CATEGORY](average-selling-price-per-product-category)

  [PRODUCTS NOT SOLD IN LAST SIX MONTHS](products-not-sold-in-the-last-6-months)

 - [Insights and Recommendations](insights-and-recommendation)

- [Conclusion](conclusion)
  

## Introduction
   
This product data highlights SQL-based data analysis for product sales performance. The report explores essential metrics such as the best-selling products, revenue generation, customer spending trends, and product inactivity. Each query demonstrates the ability to extract meaningful insights from structured data.


## Project Objectives

The primary goals of this analysis are:

- To identify top-performing products based on sales volume and revenue.

- To determine the average selling price across product categories.

- To explore customer buying behavior and identify any underperforming products.

- To provide actionable insights that improve inventory and sales strategies.


## Data Overview

This project uses two primary tables:

- Products Table: Contains information about each product, including product ID, name, category, price, and manufacturing costs.

- Orders Table: Tracks customer orders, including order dates, product IDs, and the quantities ordered.
  




## SQL Queries and Analysis


-  TOP-SELLING PRODUCTS BY QUANTITY
  
The following query identifies the top 10 products with the highest total sales quantity.

sql

SELECT p.productID, p.Name, SUM(o.quantity) AS total_quantity_sold
FROM products p
JOIN orders o ON p.ProductID = o.ProductID
GROUP BY p.ProductID, p.Name
ORDER BY total_quantity_sold DESC
LIMIT 10;


![Top selling products](https://github.com/user-attachments/assets/3c43f6a4-d18b-4bde-8fb8-ed1056bcc062)


Explanation

This query uses an inner join to combine the products and orders tables based on matching product IDs.

The SUM() function calculates the total quantity sold for each product.

Results are sorted in descending order by the total quantity sold, and only the top 10 products are displayed.


- PRODUCTS GENERATING HIGHEST REVENUE
  
This query identifies the products that generate the most revenue.

sql

SELECT 
    p.ProductID, 
    p.Name, 
    SUM(o.Quantity * p.Total_price) AS total_revenue
FROM 
    products p
JOIN 
    orders o ON p.ProductID = o.ProductID
GROUP BY 
    p.ProductID, p.Name
ORDER BY 
    total_revenue DESC
LIMIT 10;

![Highest revenue by productID](https://github.com/user-attachments/assets/e8c32781-28b5-43d8-afa4-8a231952b1c6)


Explanation

This query calculates total revenue by multiplying quantity sold by the product’s total price.

The SUM() function aggregates the revenue for each product.

The LIMIT clause ensures only the top 10 highest revenue products are displayed.

-  NUMBER OF UNIQUE PRODUCT SOLD
   
The following query determines how many unique products were sold.

sql

SELECT COUNT(DISTINCT o.productID) AS unique_products_in_stock
FROM orders o;


![Count of unique product sold](https://github.com/user-attachments/assets/cd040db3-79eb-429a-b619-af001d296e4a)

Explanation

The COUNT(DISTINCT) function counts the number of distinct product IDs in the orders table.

This metric helps measure product diversity in sales.


- AVERAGE SELLING PRICE PER PRODUCT CATEGORY
  
This query calculates the average selling price for each product category.

sql

SELECT 
    p.Category, 
    AVG(p.Total_price) AS average_price
FROM 
    products p
GROUP BY 
    p.Category;

![Average selling price](https://github.com/user-attachments/assets/663624da-036a-4320-99a9-155dcaf0e0ba)

    
Explanation

The AVG() function computes the average price of products within each category.

Grouping by category provides insights into pricing trends across different product types.


- PRODUCTS NOT SOLD IN LAST SIX MONTHS
  
The following query identifies products that have not been sold in the past six months.

sql

SELECT ProductID, Name
FROM products
WHERE ProductID NOT IN (
    SELECT DISTINCT ProductID
    FROM orders
    WHERE STR_TO_DATE(OrderDate, '%Y-%m-%d') >= DATE_SUB(CURDATE(), INTERVAL 6 MONTH)
)
LIMIT 1000;


![Product not sold for the past 6months](https://github.com/user-attachments/assets/8dca01aa-b497-4a4d-a840-ef33a3bb53aa)


Explanation
This query checks for products not listed in any order from the past six months using a subquery.

It helps identify slow-moving or outdated inventory that may require promotion or clearance.


## Insights and Recommendations

- Top-Selling Products

Products like:
K-Eco Blast 400,
K-Eco Blast 100,
K-Eco AA  NiMH rechargeable batteries (6-pack),
K-Eco Energy Bulbs 9W  (8-pack),
K-Eco Energy Bulbs 9W (4-pack),
K-Eco 575,
K-Eco 325,
K-Eco 300,
K-Eco Energy Bulbs 23W,
K-Eco 200.
drive significant sales volume. Ensuring these products are well-stocked can prevent lost sales due to stockouts.

- High-Revenue Products

Products with both high revenue and high margins should receive priority marketing efforts to maximize profitability.

- Product Diversity

With a wide range of unique products sold, the company demonstrates a healthy product mix. However, monitoring slow-moving products will help maintain profitability.

- Inactivity Alert

Products not sold in the past six months should either be discounted or bundled with other items to stimulate sales.
Customer Behavior

Further segmentation of customer data could provide deeper insights into buying patterns, enabling personalized offers.



## Conclusion

 This product data demonstrates the effective use of SQL queries to generate actionable business insights. 
 
 From identifying top-performing products to calculating average prices across categories, the analysis equips stakeholders with key data to inform inventory and sales strategies.

By employing advanced SQL techniques such as joins, subqueries, and aggregations, this project showcases an ability to manipulate large datasets to uncover trends.

These insights lay the groundwork for improved decision-making in inventory management, marketing, and overall business strategy.

