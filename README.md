
# SQL Retail Sales Queries

## Q1. Retrieve all columns for sales made on '2022-11-05'

```sql
SELECT * 
FROM retailsales 
WHERE sale_date = '2022-11-05';
````

---

## Q2. Retrieve all transactions where the category is 'clothing' and the quantity sold is more than 10 in November 2022

```sql
SELECT *
FROM retailsales
WHERE category = 'clothing'
  AND quantity > 10
  AND sale_date >= '2022-11-01'
  AND sale_date <= '2022-11-30';
```

*Note: No such row found*

---

## Q3. Calculate the total sales (`total_sale`) for each category

```sql
SELECT category, SUM(total_sale) AS Total_Sale
FROM retailsales
GROUP BY category;
```

---

## Q4. Find the average age of customers who purchased items from the 'Beauty' category

```sql
SELECT AVG(age) AS Average_age
FROM retailsales
WHERE category = 'Beauty';
```

---

## Q5. Find all transactions where the total sale is greater than 1000

```sql
SELECT * 
FROM retailsales 
WHERE total_sale > 1000;
```

---

## Q6. Find the total number of transactions (`transactions_id`) made by each gender in each category

```sql
SELECT gender, category, COUNT(transactions_id) AS Total_Transaction
FROM retailsales
GROUP BY gender, category;
```

---

## Q7. Calculate the average sale for each month and find the best-selling month in each year

```sql
SELECT YEAR(sale_date) AS year, MONTH(sale_date) AS month, AVG(total_sale) AS avg_sale
FROM retailsales
GROUP BY YEAR(sale_date), MONTH(sale_date)
ORDER BY year, month;
```

---

## Q8. Find the top 5 customers based on the highest total sales

```sql
SELECT *
FROM retailsales
ORDER BY total_sale DESC
LIMIT 5;
```

---

## Q9. Find the number of unique customers who purchased items from each category

```sql
SELECT category AS Category, COUNT(DISTINCT customer_id) AS unique_customers
FROM retailsales
GROUP BY category
ORDER BY unique_customers DESC;
```

---

## Q10. Create each shift and number of orders

```sql
SELECT 
    CASE
        WHEN HOUR(sale_time) < 12 THEN 'Morning'
        WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END AS shift,
    COUNT(transactions_id) AS total_orders
FROM retailsales
GROUP BY shift
ORDER BY total_orders DESC;
```

