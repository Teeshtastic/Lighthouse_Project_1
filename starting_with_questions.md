Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

``SQL
SELECT city, country, SUM(totalTransactionRevenue_usd) AS total_revenue
FROM cleaned_all_sessions
WHERE totalTransactionRevenue_usd > 0 
GROUP BY city, country
ORDER BY total_revenue DESC;
``

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


``SQL
SELECT city, country, AVG(productquantity) AS avg_ordered
FROM cleaned_all_sessions
GROUP BY city, country
HAVING AVG(productquantity) > 0  
ORDER BY avg_ordered DESC;``

Answer:

The average number of products ordered varied considerably across the top five locations. Columbus and Madrid had the highest average at 0.5 products per visitor. Detroit averaged 0.25 products per visitor, while Salem averaged 0.16. Finland had the lowest average of the top five, at just 0.07 products per visitor. The full dataset includes averages for 26 locations, accessible via the query provided.

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

``SQL
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
``

Answer:

Popular categories are bags, apparel, electronics (thermostats/smoke detectors), and home products writing instruments, drink ware). 



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

``SQL
	
SELECT DISTINCT ON (city, country) 
    v2ProductName, 
    city,
    country, 
    SUM(totalTransactionRevenue_usd) AS total_revenue
FROM cleaned_all_sessions
WHERE totalTransactionRevenue_usd > 0 
GROUP BY v2ProductName, city, country
ORDER BY city, country, total_revenue DESC;
``

Answer:

Atlanta has purchased an abundance of reusable shopping bags, which would lead me to think there had recently been a bylaw change to charge for bags or something else to encourage the change in shopping behaviour. T-shirts are a popular purchase and are listed three times in the top ten products purchased in New York, Austin, Los Angelos, San Bruno and Columbus. Chicago's most popular purchase is sunglasses, which may indicate the time of year that users from this location are purchasing from collected websites. Nashville's top purchase is a learning thermostat which may indicate either a seasonal temperature variation and/or regulatory/commercial change that is incentivizing purchasers to try to reduce their energy consumption. Similarly, the security cams being purchased in Palo Alto might correspond to an increase in crime. 



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

``SQL
SELECT
    city,
    country,
    SUM(totalTransactionRevenue_usd) AS total_transaction_revenue_usd,
    SUM(itemRevenue_usd) AS total_item_revenue_usd,
    SUM(totalTransactionRevenue_usd + itemRevenue_usd) AS total_revenue_usd,
    COUNT(DISTINCT fullVisitorId) FROM
    cleaned_all_sessions
WHERE totalTransactionRevenue_usd > 0
GROUP BY
    city, country
ORDER BY
    total_revenue_usd DESC;
;
``

Answer:

Yes, we can summarize the impact of revenue generated for 21 locations that have revenue reported. Locations in the United States have seen the largest benefit in this data source. Locations outside of the United States include Israel, Australia, Canada, and Switzerland.











