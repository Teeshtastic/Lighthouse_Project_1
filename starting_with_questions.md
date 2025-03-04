Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT city, country, SUM(totalTransactionRevenue_usd) AS total_revenue
FROM cleaned_all_sessions
WHERE city IS NOT NULL 
  AND totalTransactionRevenue_usd > 0 
GROUP BY city, country
ORDER BY total_revenue DESC;

Answer:

San Francisco	United States
Sunnyvale	United States
Atlanta		United States
Palo Alto	United States
Tel Aviv-Yafo	Israel
New York	United States
Mountain View	United States
Los Angeles	United States
Chicago		United States
Sydney		Australia
Seattle		United States
San Jose	United States
Austin		United States
Nashville	United States
San Bruno	United States
Toronto		Canada
New York	Canada
Houston		United States
Columbus	United States
Zurich		Switzerland

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT city, country, AVG(productquantity) AS avg_ordered
FROM cleaned_all_sessions
WHERE city IS NOT NULL 
GROUP BY city, country
HAVING AVG(productquantity) > 0  
ORDER BY avg_ordered DESC;

Answer:


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT 
    v2ProductName,
    v2ProductCategory, 
    city,
    country, 
    SUM(totalTransactionRevenue_usd) AS total_revenue,
    AVG(productPrice_usd) AS avg_price
FROM cleaned_all_sessions
WHERE totalTransactionRevenue_usd > 0
GROUP BY v2ProductName, v2ProductCategory, city, country 
ORDER BY city ASC, country ASC, total_revenue DESC; 

Answer:

Atlanta has purchased an abundance of reusable shopping bags, which would lead me to think there had recently been a bylaw enforced to encourage the purchases or change in shopping behaviour. 



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT DISTINCT ON (city, country) 
    v2ProductName, 
    city,
    country, 
    SUM(totalTransactionRevenue_usd) AS total_revenue
FROM cleaned_all_sessions
WHERE totalTransactionRevenue_usd > 0 
GROUP BY v2ProductName, city, country
ORDER BY city, country, total_revenue DESC;

Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:



Answer:




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







