What issues will you address by cleaning the data?


The first five questions all reference information that I believe I can find in the all_sessions table and for that reason I will prioritize cleaning this table. The city field has 266 distinct valid cities, but there are several entries that are not set or not available in the data. I am interested frequently in assessing information by grouping by the city so in these instances (where the value is not set or not available) I will return the country. This table refers to users who are accessing webpages to look at products, but don't always purchase the products that they are looking at and in these instances returns a null value. Because I'd like to perform sum and average operations on this column when the value is null, I will replace with a 0. The unit cost in all_sessions appears to be in micro units so dividing by 1,000,000 will produce the equivalent in USD. This is the same process for any of the fields that reference money (total transaction revenue, product revenue, transaction revenue, product price, item revenue, and refund amount). When I imported the csv files into PostgreSQL, I selected text as the base datatype to enable easier importing. Performing calculations on the data requires the appropriate data type to be chosen which I've chosen as decimal because it's referring to monetary values where the information is more precise. I cast quantity, transactions, and time on site to be an integer because it refers to whole numbers or duration. 


Queries:
Below, provide the SQL queries you used to clean your data.

```SQL
CREATE VIEW cleaned_all_sessions AS
SELECT
    fullVisitorId,
	channelGrouping,
    country,
    CASE
        WHEN city IN ('(not set)', 'not available in demo dataset') THEN country
        ELSE city
    END AS city,
    date,
    visitId,
    CASE
        WHEN totalTransactionRevenue = '' THEN 0
        ELSE CAST(totalTransactionRevenue AS DECIMAL(38, 2)) / 1000000
    END AS totalTransactionRevenue_usd,

    CASE
        WHEN productRevenue = '' THEN 0
        ELSE CAST(productRevenue AS DECIMAL(38, 2)) / 1000000
    END AS productRevenue_usd,

    CASE
        WHEN transactionRevenue = '' THEN 0
        ELSE CAST(transactionRevenue AS DECIMAL(38, 2)) / 1000000
    END AS transactionRevenue_usd,
    CASE
        WHEN productQuantity = '' THEN 0
        ELSE CAST(productQuantity AS INTEGER)
    END AS productQuantity,
    CASE
        WHEN productPrice = '' THEN 0
        ELSE CAST(productPrice AS DECIMAL(38, 2)) / 1000000  
    END AS productPrice_usd,
    productSKU,
    v2ProductName,
    v2ProductCategory,
    CASE
        WHEN itemQuantity = '' THEN 0
        ELSE CAST(itemQuantity AS INTEGER)
    END AS itemQuantity,
    CASE
        WHEN itemRevenue = '' THEN 0
        ELSE CAST(itemRevenue AS DECIMAL(38, 2)) / 1000000
    END AS itemRevenue_usd,
        CASE
        WHEN productRefundAmount = '' THEN 0
        ELSE CAST(productRefundAmount AS DECIMAL(38, 2)) / 1000000
    END AS productRefundAmount_usd,
    CASE
        WHEN transactions = '' THEN 0
        ELSE CAST(transactions AS INTEGER)
    END AS transactions,
    CASE
        WHEN timeOnSite = '' THEN 0
        ELSE CAST(timeOnSite AS INTEGER)
    END AS timeOnSite
FROM
    all_sessions;
```