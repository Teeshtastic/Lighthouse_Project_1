As I spent time reviewing the all_sessions table, I found that certain questions naturally developed. I've decided to choose a few things that I found myself wondering as I worked with the data. 


Question 1: What percentage of sales are being generated through each channel of a visitor arriving at a website who make a purchase?

SQL Queries:

```SQL

SELECT
    country,
    channelGrouping,
    SUM(totalTransactionRevenue_usd) AS channel_revenue,
    (SUM(totalTransactionRevenue_usd) * 100 / (SELECT SUM(totalTransactionRevenue_usd) FROM cleaned_all_sessions WHERE country = a.country AND totalTransactionRevenue_usd > 0)) AS percentage_of_country_revenue
FROM
    cleaned_all_sessions a
WHERE totalTransactionRevenue_usd > 0
GROUP BY
    country,
    channelGrouping
ORDER BY
    country ASC,
    percentage_of_country_revenue DESC;```

Answer: 

All of the sales from visitors from Australia, Israel, and Switzerland are being driven by users directly typing in the website that they purchased from. Visitors from Canada are finding the website through organic search half of the time and the other half of the time through referral via another website. Consumers from the United States are driven by referral nearly 50% of the time, direct 28%, organic search 23%, and through a paid ad on a search engine only 3% of the time. If I was a company that paid money for ads, this would give me information about what if any products this is effective for and either convince me to improve the way I conducted paid marketing or focus efforts on another channel. 


Question 2: The logical follow up question is for which products are paid ads are generating in sales? 

SQL Queries:

```SQL
SELECT 
    channelGrouping, 
    v2ProductName,
    SUM(totalTransactionRevenue_usd) AS total_revenue
FROM cleaned_all_sessions
WHERE totalTransactionRevenue_usd > 0 
AND channelgrouping = 'Paid Search'
GROUP BY channelGrouping, v2ProductName
ORDER BY channelgrouping, total_revenue DESC, v2ProductName ASC;
```

Answer:

Paid ads are most effective in generating sales of the Nest smoke alarm, google laptop and cell phone stickers, and men's 100% cotton short sleeve hero black tee shirts. 


Question 3: What locations buy Henley shirts?

SQL Queries:

```SQL
SELECT 
    v2ProductName,
    v2ProductCategory, 
    city,
    country, 
    SUM(totalTransactionRevenue_usd) AS total_revenue,
    AVG(productPrice_usd) AS avg_price
FROM cleaned_all_sessions
WHERE totalTransactionRevenue_usd > 0 
    AND v2ProductName LIKE '%Henley%'  
GROUP BY v2ProductName, v2ProductCategory, city, country 
ORDER BY city ASC, country ASC, total_revenue DESC; 
```


Answer:

I did expect to see Canada and Switzerland, but there are also Henley's sold to customers in Sunnyvale, United States. It is of note that Henley's average $20 in Canada, but are $24-25 in Switzerland and the US.


Question 4: Which products generated the highest time on site from visitors?

SQL Queries:

```SQL

SELECT 
    v2ProductName AS Product_Name,
    SUM(timeonsite) AS total_duration  
FROM cleaned_all_sessions
GROUP BY v2ProductName
ORDER BY total_duration DESC;```

Answer:

The answer is overwhelmingly tee shirts of the classic black and white variety.



