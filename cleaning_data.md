What issues will you address by cleaning the data?


My initial priority is cleaning the all_sessions table to enable effective analysis of user behaviour and revenue data. To be able to group by cities, I will replace missing or unavailable city values with the corresponding country. Monetary values in all_sessions are stored in cents. To convert them to USD, I will divide totalTransactionRevenue, productRevenue, transactionRevenue, productPrice, itemRevenue, and productRefundAmount by 1,000,000. To enable aggregation operations (sum and average), null values in these revenue columns will be replaced with 0. I imported the CSV files into PostgreSQL using the text data type for initial flexibility. I will cast productQuantity, transactions, and timeOnSite to INTEGER, as they represent whole numbers or durations. Monetary fields will be cast to DECIMAL(38, 2) to preserve precision for financial calculations.

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