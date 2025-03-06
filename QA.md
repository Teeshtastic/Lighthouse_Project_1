What are your risk areas? Identify and describe them.

The dataset is heavily focused on viewers from the United States which makes it challenging to make broad assumptions without understanding how or where the data was collected. There are several instances of missing information from the city column which makes grouping by city limited. I do not understand the difference between totalTransactionRevenue, productRevenue, and itemRevenue. I used totalTransactionRevenue in my queries, but was unclear if this was appropriate. There are a significant amount of missing values, which required me to direct my cleaned table to replace with either a 0 or a country if I felt the most appropriate, but relies on my judgement with little context. 

QA Process:
Describe your QA process and include the SQL queries used to execute it.

Distribution of viewers from different countries 
```SQL
SELECT
    country,
    COUNT(*) AS record_count
FROM
    all_sessions
GROUP BY
    country
ORDER BY
    record_count DESC
LIMIT 20;
 
```

Missing or null values

```SQL
SELECT
    COUNT(*) AS total_records,
    COUNT(CASE WHEN city = '(not set)' OR city = 'not available in demo dataset' THEN 1 END) AS missing_city_count,
    COUNT(CASE WHEN totalTransactionRevenue = '' THEN 1 END) AS missing_revenue_count
FROM
    all_sessions;
```

Check how many times city was null and replaced with country

```SQL
SELECT
    COUNT(*)
FROM
    cleaned_all_sessions
WHERE
    city = country
    AND city IN ('(not set)', 'not available in demo dataset');
```

I noticed that in the sales_report table and the products table that both contained product sku or sku column names as well as ordered quantity and total_ordered so decided to make a query to check that this information matched and it does not so I really am unsure what the information means in these columns.

```SQL

SELECT 	products.sku,
		products.name,
     	products.orderedquantity,
       	sales_report.total_ordered
FROM products 
JOIN sales_report 
ON products.sku = sales_report.productsku
```