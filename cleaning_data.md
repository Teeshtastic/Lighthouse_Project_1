What issues will you address by cleaning the data?





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