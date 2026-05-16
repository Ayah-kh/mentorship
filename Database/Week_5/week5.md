# Week 4

##  Write a Trigger to create a sale history

### function
```sql

CREATE OR REPLACE FUNCTION insert_order_history()
RETURNS TRIGGER AS $$
BEGIN

    INSERT INTO order_history (
        order_id,
        order_date,
        total_amount,
        quantity,
        product_name,
        unit_price,
        customer_first_name,
        customer_last_name
    )
    SELECT
        o.order_id,
        o.order_date,
        o.total_amount,
        od.quantity,
        p.name,
        od.unit_price,
        c.first_name,
        c.last_name
    FROM orders o
    JOIN customer c
        ON c.customer_id = o.customer_id
    JOIN order_details od
        ON od.order_id = o.order_id
    JOIN product p
        ON p.product_id = od.product_id
    WHERE o.order_id = NEW.order_id;

    RETURN NEW;

END;
$$ LANGUAGE plpgsql;
```

### Trigger
```sql
CREATE TRIGGER trg_insert_order_history
AFTER INSERT ON order_details
FOR EACH ROW
EXECUTE FUNCTION insert_order_history();
```

##  Write a Trigger to create a sale history

```sql
BEGIN;

SELECT *
FROM product
WHERE product_id = 1
FOR UPDATE;

UPDATE product
SET quantity = quantity - 1
WHERE product_id = 1;

COMMIT;
```






