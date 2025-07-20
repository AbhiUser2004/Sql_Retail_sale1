# Sql_Retail_sale1

--SIMPLE CLEANING 
SELECT * FROM retail_sales
LIMIT 10;

SELECT  COUNT(*)
FROM retail_sales;

SELECT * FROM retail_sales
WHERE gender IS NULL
OR 
age IS NULL
OR
category IS NULL
OR
quantity IS NULL
OR
price_per_unit IS NULL
OR
cogs IS NULL
OR
total_sale IS NULL

--
DELETE FROM retail_sales
WHERE gender IS NULL
OR 
age IS NULL
OR
category IS NULL
OR
quantity IS NULL
OR
price_per_unit IS NULL
OR
cogs IS NULL
OR
total_sale IS NULL;

--DATA EXPLOREATION

--Q1.HOW MANY SALES DO WE HAVE
SELECT COUNT(total_sale) AS total
FROM retail_sales;
--Q2.HOW MANY UNIQUE CUSTOMERS DO WE HAVE 
SELECT COUNT(DISTINCT customer_id) AS total_customers
FROM retail_sales;
--Q3.HOW MANY UNIQUE CATEGORIES DO WE HAVE 
SELECT COUNT(DISTINCT category) AS total_category
FROM retail_sales;

--Data Analysis & Business key problem

--Q4.Write a SQL query to retrieve all columns for sales made on '2022-11-05:
SELECT * FROM retail_sales
WHERE sale_date = '2022-11-05';
--Q5.Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022:
SELECT * FROM retail_sales
WHERE category = 'Clothing'
AND
TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
AND
quantity >=4;
--Q6.Write a SQL query to calculate the total sales (total_sale) for each category.:
SELECT category, SUM(total_sale) AS total_s,
COUNT(*) AS Total_orders
FROM retail_sales
GROUP BY category;
--Q7.Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.
SELECT AVG(age) AS Avg_Age
FROM retail_sales
WHERE category = 'Beauty';
--OR
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
--Q8.Write a SQL query to find all transactions where the total_sale is greater than 1000.:
SELECT * FROM retail_sales
WHERE total_sale > 1000;
--Q9.Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.:
SELECT category,
gender,
COUNT(*) AS Total_trans
FROM retail_sales
GROUP BY category, gender;
--Q10.Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:
SELECT 
     EXTRACT(YEAR FROM retail_sales.sale_date) AS YEAR,
	 EXTRACT(MONTH FROM retail_sales.sale_date) AS MONTH,
	 AVG(total_sale) AS TOTAL,
	 RANK() OVER(PARTITION BY EXTRACT(YEAR FROM retail_sales.sale_date) 
	 ORDER BY  AVG(total_sale) DESC )
	 FROM retail_sales
	 GROUP BY 1, 2;
--Q11.Write a SQL query to find the top 5 customers based on the highest total sales
   SELECT Customer_id,
   SUM(total_sale) AS total_sales
   FROM retail_sales
   GROUP BY 1
   ORDER BY 2 DESC
   LIMIT 5;
--Q12.Write a SQL query to find the number of unique customers who purchased items from each category.
SELECT category,
COUNT(DISTINCT customer_id) AS UNI_CU
FROM retail_sales
GROUP BY category;
--Q13.Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17):
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift

--END OF THE PROJECT--

Customer Demographics: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
High-Value Transactions: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
Sales Trends: Monthly analysis shows variations in sales, helping identify peak seasons.
Customer Insights: The analysis identifies the top-spending customers and the most popular product categories.
Reports
Sales Summary: A detailed report summarizing total sales, customer demographics, and category performance.
Trend Analysis: Insights into sales trends across different months and shifts.
Customer Insights: Reports on top customers and unique customer counts per category.
Conclusion
This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

How to Use
Clone the Repository: Clone this project repository from GitHub.
Set Up the Database: Run the SQL scripts provided in the database_setup.sql file to create and populate the database.
Run the Queries: Use the SQL queries provided in the analysis_queries.sql file to perform your analysis.
Explore and Modify: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.
Author - Abhishek kumar
   
