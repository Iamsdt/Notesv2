set
SELECT name  
FROM customers  
UNION  
SELECT coalesce(first_name, last_name) as name  
FROM employees;




Transaction
BEGIN TRANSACTION;  
-- SQL statements and changes within the transaction  
INSERT INTO employees (first_name, last_name, age, hire_date) VALUES ('Alice',  
'bob', 27, '2014-11-25');  
UPDATE products SET price = 25.00 WHERE name =  
'Product 27';  
COMMIT;


BEGIN TRANSACTION;  
-- SQL statements and changes within the transaction  
INSERT INTO employees (first_name, last_name, age, hire_date) VALUES ('Alice4',  
'bob', 27, '2014-11-25');  
UPDATE products SET price = 25.00 WHERE name =  
'Product 27';  
ROLLBACK;  
  
select * from employees where first_name = 'Alice3'



# Save point
BEGIN TRANSACTION;  
INSERT INTO employees (first_name, age) VALUES ('Carol',  
28);  
SAVEPOINT before_update;  
UPDATE products SET price = 40.00 WHERE name =  
'Product 28';  
SAVEPOINT after_update;  
UPDATE products SET price = 25.00 WHERE name = 'Product 27';  
ROLLBACK TO before_update;  
-- At this point, the Update is rolled back, but the previous remains.  
COMMIT;


# Advance
Window Functions:

- OVER clause
- Ranking functions (ROW_NUMBER, RANK, DENSE_RANK)
- Aggregate window functions (SUM, AVG, COUNT over windows)
- PARTITION BY and ORDER BY within window functions

-- window function  
SELECT  
    name,  
    city,  
    age,  
    RANK() OVER (PARTITION BY city ORDER BY age DESC) as age_rank_in_city  
FROM employees e  
JOIN customers c ON e.employee_id = c.customer_id;


with 
WITH avg_order AS (  
    SELECT AVG(total_amount) as avg_amount  
    FROM orders  
)  
SELECT c.name, o.total_amount  
FROM customers c  
JOIN orders o ON c.customer_id = o.customer_id  
CROSS JOIN avg_order  
WHERE o.total_amount > avg_order.avg_amount;


materialed view vs view
CREATE MATERIALIZED VIEW order_summary AS  
SELECT  
    c.name AS customer_name,  
    COUNT(o.order_id) AS order_count,  
    SUM(o.total_amount) AS total_spent  
FROM customers c  
JOIN orders o ON c.customer_id = o.customer_id  
GROUP BY c.customer_id, c.name;


# Query aggeration
EXPLAIN ANALYZE  
SELECT c.name, SUM(o.total_amount)  
FROM customers c  
JOIN orders o ON c.customer_id = o.customer_id  
WHERE c.city = 'New York'  
GROUP BY c.customer_id, c.name;




# Partition
CREATE TABLE orders_partitioned (  
    order_id SERIAL,  
    customer_id INT,  
    order_date DATE,  
    total_amount DECIMAL(10, 2)  
) PARTITION BY RANGE (order_date);


CREATE TABLE orders_partitioned (  
    order_id SERIAL,  
    customer_id INT,  
    order_date DATE,  
    total_amount DECIMAL(10, 2)  
) PARTITION BY RANGE (order_date);  
  
CREATE TABLE orders_2023 PARTITION OF orders_partitioned  
    FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');  
CREATE TABLE orders_2024 PARTITION OF orders_partitioned  
    FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');  
  
INSERT INTO orders_partitioned (customer_id, order_date, total_amount)  
SELECT customer_id, order_date, total_amount  
FROM orders  
WHERE order_date >= '2023-01-01' AND order_date < '2025-01-01';  
  
SELECT * FROM orders_partitioned  
WHERE order_date BETWEEN '2023-06-01' AND '2023-12-31';

explain SELECT * FROM orders_partitioned  
WHERE order_date >= '2024-05-01'


## Trigger

```
CREATE TABLE order_items (  
    order_id INT REFERENCES orders(order_id),  
    product_id INT REFERENCES products(product_id),  
    quantity INT,  
    price DECIMAL(10, 2)  
);  
  
  
CREATE OR REPLACE FUNCTION update_order_total()  
RETURNS TRIGGER AS $$  
BEGIN  
    UPDATE orders  
    SET total_amount = (  
        SELECT sum(quantity * price)  
        FROM order_items  
        WHERE order_id = NEW.order_id  
    )  
    WHERE order_id = NEW.order_id;  
    RETURN NEW;  
END;  
$$ LANGUAGE plpgsql;  
  
CREATE or REPLACE TRIGGER update_order_total_trigger2  
AFTER INSERT OR UPDATE OR DELETE ON order_items  
FOR EACH ROW EXECUTE FUNCTION update_order_total();  
  
INSERT INTO order_items (order_id, product_id, quantity, price) VALUES (2, 1, 5, 100);  
  
  
SELECT * FROM orders WHERE order_id = 2;
```