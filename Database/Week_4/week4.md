# Week 4

##  Write a SQL query to search for all products with the word "camera" in either the product name or description.

```sql

select * from product where name ilike '%camera% or description i
like '%camera%';
```

## design a query to suggest popular products in the same category for the same author, excluding the Purchsed product from the recommendations?

```sql

SELECT p.product_id, p.name, COALESCE(SUM(od.quantity), 0) AS total_sold
FROM product p
LEFT JOIN order details od
         ON product.id = od.product_id
WHERE p.category_id = (
        SELECT category_id
        FROM product
        WHERE product_id = :current_product_id
        )
AND p.product_id <> :current_Product_id
AND NOT EXISTS(
        SELECT 1
        FROM orders o
        JOIN order_details od1
        ON o.order_id = od1.order_details
        WHERE o.customer_id = specific_customer
        AND od1.product_id = p.product_id
)
GROUP BY p.product_id, p.name
ORDER BY total_sold DESC
LIMIT 10


```









