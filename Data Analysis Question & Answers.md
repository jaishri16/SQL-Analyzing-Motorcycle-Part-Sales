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

