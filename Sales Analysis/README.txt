Superstore Data Analysis

--> Cleaning and Transformation

1) Date Type Change Using Locale
2) Duplicates Remove
3) Calculated Column 
   Delivery Days = [Ship Date]-[Order Date]
4) Measures
   Profit % = (DIVIDE(SUM('Sample - Superstore'[Profit]),SUM('Sample - Superstore'[Sales]))*100)
   
--> Analysis Using Sql
1) find total sales and profit percentage by subcategory ?

WITH cte AS 
(SELECT subcategory, SUM(sales) AS total_sales , SUM(profit) AS total_profit
FROM superstoredata
GROUP BY subcategory
ORDER BY total_sales DESC),

cte1 AS
(SELECT (SUM(profit)/SUM(sales))*100 AS profit_prcnt, subcategory
 FROM superstoredata
 GROUP BY subcategory
 ORDER BY profit_prcnt DESC)
 
SELECT cte.subcategory, cte.total_sales, cte.total_profit, cte1.profit_prcnt
FROM cte JOIN cte1 ON cte.subcategory = cte1.subcategory
GROUP BY cte.subcategory, cte.total_sales, cte.total_profit, cte1.profit_prcnt
ORDER BY cte1.profit_prcnt DESC


2) Describe sales in all regions 

SELECT region , SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt
FROM superstoredata
GROUP BY region
ORDER BY total_sales DESC

3) Find profit making and loss making states 

SELECT state, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt
FROM superstoredata
GROUP BY state
HAVING SUM(profit) > 0
ORDER BY total_sales DESC


SELECT state, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt
FROM superstoredata
GROUP BY state
HAVING SUM(profit) < 0
ORDER BY total_sales DESC

4) Find profit making and loss making products 


SELECT product_name, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt
FROM superstoredata
GROUP BY product_name
HAVING SUM(profit) > 0
ORDER BY total_sales DESC

SELECT product_name, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt
FROM superstoredata
GROUP BY product_name
HAVING SUM(profit) < 0
ORDER BY total_sales DESC

5) Find top buyers from DIfferent regions 


SELECT customer_name, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt,region
FROM superstoredata
WHERE region = 'South'
GROUP BY customer_name, region
ORDER BY total_sales DESC
LIMIT 10 
  
SELECT customer_name, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt,region
FROM superstoredata
WHERE region = 'North'
GROUP BY customer_name, region
ORDER BY total_sales DESC
LIMIT 10 

SELECT customer_name, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt,region
FROM superstoredata
WHERE region = 'East'
GROUP BY customer_name, region
ORDER BY total_sales DESC
LIMIT 10 

SELECT customer_name, SUM(sales) AS total_sales, SUM(profit) as total_profit,
       (SUM(profit)/SUM(sales))*100 as profit_prcnt,region
FROM superstoredata
WHERE region = 'West'
GROUP BY customer_name, region
ORDER BY total_sales DESC
LIMIT 10 
   