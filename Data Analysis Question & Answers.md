


```
WITH s AS (
    SELECT
        product_line,
        CASE 
            WHEN EXTRACT(MONTH FROM date) = 6 THEN 'June'
            WHEN EXTRACT(MONTH FROM date) = 7 THEN 'July'
            ELSE 'August'
        END AS month,
        warehouse,
        ROUND(SUM(total * (1 - payment_fee))::numeric, 2) AS net_revenue
    FROM  
        sales
    WHERE 
        client_type ='Wholesale'
    GROUP BY
        product_line, month, warehouse
)
SELECT 
    product_line, 
    month,
    warehouse,
    net_revenue
FROM 
    s
ORDER BY
    product_line, month, warehouse DESC;
```
RESULT:

| product_line     | month  | warehouse | net_revenue |
|------------------|--------|-----------|-------------|
| Breaking system  | August | West      | 2475.71     |
| Breaking system  | August | North     | 1753.19     |
| Breaking system  | August | Central   | 3009.10     |
| Breaking system  | July   | West      | 3030.39     |
| Breaking system  | July   | North     | 2568.55     |
| Breaking system  | July   | Central   | 3740.94     |
| Breaking system  | June   | West      | 1200.64     |
| Breaking system  | June   | North     | 1472.93     |
| Breaking system  | June   | Central   | 3648.14     |
| Electrical system| August | West      | 1229.45     |

