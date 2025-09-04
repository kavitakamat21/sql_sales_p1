# sql_sales_p1
**-- Create Database**


Create database Sales;

use Sales;

'''select * from Sales02;'''



**-- Data Analysis & Business Key Problems & Answers.**


-- 0.1 Write a SQL query to retrieve all columns for sales made on 2022-11-05.

 '''select * 
 from Sales02 
 where sale_date = "2022-11-05";'''


-- Q.2 Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4  
--   in the month of nov -2022.
 select 
 *
 from Sales02 
 where category = "Clothing" 
 and sale_date = "2022-11-03"
 and quantiy >=4;

-- Q.3 Write a SQL query to calculate the total sales (total sale) for each category.
select category,sum(total_sale) from sales02 group by category;
-- Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.
select round(avg(age),2) as avg_age from sales02 where category = "Beauty";

-- Q.5 Write a SQL query to find all transactions where the total sale is greater than 1000.
select * from sales02 where total_sale >1000;
-- Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.
select category,gender,count(*) as total_transcation from sales02 group by category,gender order by 1;
-- 0.7 write a SQL query to calculate the average sale for each month. Find out best selling month in each year.
SELECT 
    YEAR(sale_date) AS year,
    MONTH(sale_date) AS month,
    AVG(total_sale) AS avg_sale
FROM sales02
GROUP BY YEAR(sale_date), MONTH(sale_date)
ORDER BY year, month;

-- Q.8 Write a SQL query to find the top 5 customers based on the highest total sales.
SELECT 
    customer_id,
    SUM(total_sale) AS total_sales
FROM Sales02
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;

-- Q.9 Write a SQL query to find the number of unique customers who purchased items from each category.
select category,count(distinct customer_id) as customers from sales02 group by category;
-- select distinct count(customer_id) as customers ,category from sales02 group by category; --wrong ans
-- Q.10 Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17).
with hourly_sale
as 
(
SELECT *,
    CASE 
        WHEN HOUR(sale_time) < 12 THEN 'Morning'
        WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END AS shift
    from sales02
)
select shift,
    COUNT(*) AS total_orders
from hourly_sale
GROUP BY shift;


select * from Sales02;

-- End of the project.


