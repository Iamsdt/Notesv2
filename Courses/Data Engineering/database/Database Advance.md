---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - pgsql
  - psql-advance
  - sql
---

## 1. Efficient Data Loading Techniques

### COPY Command
```sql
-- Faster than INSERT for bulk loading
COPY customers(id, name, email)
FROM '/path/to/file.csv' 
WITH (FORMAT CSV, HEADER true);

-- Parallel loading using COPY
BEGIN;
COPY customers_part1 FROM '/path/file1.csv' WITH (FORMAT CSV);
COPY customers_part2 FROM '/path/file2.csv' WITH (FORMAT CSV);
COMMIT;
```

### Temporary Tables for Staging
```sql
-- Create temporary table for staging
CREATE TEMPORARY TABLE temp_customers (LIKE customers);

-- Load data into staging
COPY temp_customers FROM '/path/to/file.csv' WITH (FORMAT CSV);

-- Insert only new records
INSERT INTO customers 
SELECT t.* FROM temp_customers t
LEFT JOIN customers c ON t.id = c.id
WHERE c.id IS NULL;
```

## 2. Advanced ETL Patterns

### Merge (Upsert) Operations
```sql
-- Insert or update based on condition
INSERT INTO customers (id, name, email, updated_at)
VALUES (1, 'John Doe', 'john@example.com', NOW())
ON CONFLICT (id) DO UPDATE 
SET name = EXCLUDED.name,
    email = EXCLUDED.email,
    updated_at = NOW();
```

### Slowly Changing Dimensions (SCD)
```sql
-- Type 2 SCD implementation
WITH new_records AS (
    SELECT 
        customer_id,
        name,
        address,
        NOW() as valid_from,
        NULL::timestamp as valid_to,
        TRUE as is_current
    FROM staging_customers
)
UPDATE customer_dim
SET valid_to = NOW(),
    is_current = FALSE
WHERE customer_id IN (SELECT customer_id FROM new_records)
    AND is_current = TRUE;

INSERT INTO customer_dim
SELECT * FROM new_records;
```

## 3. Performance Optimization Techniques

### Partitioning with Inheritance
```sql
-- Create parent table
CREATE TABLE logs (
    log_time timestamp,
    user_id int,
    action text
) PARTITION BY RANGE (log_time);

-- Create monthly partitions
CREATE TABLE logs_2024_01 PARTITION OF logs
    FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');

CREATE TABLE logs_2024_02 PARTITION OF logs
    FOR VALUES FROM ('2024-02-01') TO ('2024-03-01');
```

### Parallel Query Execution
```sql
-- Set parallel workers
SET max_parallel_workers_per_gather = 4;

-- Force parallel scan
SELECT /*+ PARALLEL(users 4) */
    user_id, COUNT(*) 
FROM users 
GROUP BY user_id;
```

## 4. Window Functions for Analytics

### Moving Averages and Running Totals
```sql
SELECT 
    date,
    amount,
    AVG(amount) OVER (
        ORDER BY date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) as moving_avg_7day,
    SUM(amount) OVER (
        ORDER BY date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) as running_total
FROM daily_sales;
```

### Percentile Calculations
```sql
SELECT 
    department,
    employee_name,
    salary,
    PERCENT_RANK() OVER (PARTITION BY department ORDER BY salary) as salary_percentile,
    NTILE(4) OVER (PARTITION BY department ORDER BY salary) as salary_quartile
FROM employees;
```

## 5. Advanced Aggregation Techniques

### FILTER Clause
```sql
SELECT 
    department,
    COUNT(*) as total_employees,
    COUNT(*) FILTER (WHERE performance_score >= 4) as high_performers,
    AVG(salary) FILTER (WHERE role = 'Senior') as avg_senior_salary
FROM employees
GROUP BY department;
```

### Custom Aggregates
```sql
-- Create array of distinct values
SELECT 
    department,
    ARRAY_AGG(DISTINCT role ORDER BY role) as unique_roles,
    STRING_AGG(DISTINCT name, ', ' ORDER BY name) as employee_list
FROM employees
GROUP BY department;
```

## 6. Data Quality and Validation

### Constraints and Checks
```sql
CREATE TABLE orders (
    order_id int PRIMARY KEY,
    order_date date,
    amount numeric,
    CONSTRAINT valid_amount CHECK (amount > 0),
    CONSTRAINT valid_date CHECK (order_date <= CURRENT_DATE)
);
```

### Data Quality Monitoring
```sql
-- Monitor null values and data distributions
SELECT 
    column_name,
    COUNT(*) as total_rows,
    COUNT(*) FILTER (WHERE column_name IS NULL) as null_count,
    COUNT(DISTINCT column_name) as distinct_values,
    MIN(column_name) as min_value,
    MAX(column_name) as max_value
FROM table_name
GROUP BY column_name;
```

## 7. Working with JSON Data

### JSON Operations
```sql
-- Extract and aggregate JSON data
SELECT 
    user_id,
    jsonb_array_elements(preferences)->'category' as category,
    COUNT(*)
FROM user_preferences
GROUP BY user_id, category;

-- Update nested JSON
UPDATE users
SET preferences = jsonb_set(
    preferences,
    '{notifications,email}',
    'true'
);
```


# Advance View Technique
# Advanced PostgreSQL View Techniques for Data Engineers

## 1. Materialized Views with Concurrent Refresh

### Basic Materialized View with Indexes
```sql
CREATE MATERIALIZED VIEW mv_sales_summary AS
SELECT 
    date_trunc('month', order_date) as month,
    product_category,
    region,
    SUM(amount) as total_sales,
    COUNT(DISTINCT customer_id) as unique_customers,
    AVG(amount) as avg_order_value
FROM orders o
JOIN products p ON o.product_id = p.id
GROUP BY 1, 2, 3
WITH DATA;

-- Create indexes on materialized view
CREATE INDEX idx_mv_sales_summary_month ON mv_sales_summary(month);
CREATE INDEX idx_mv_sales_summary_category ON mv_sales_summary(product_category);
```

### Concurrent Refresh Strategy
```sql
-- Enable concurrent refresh
CREATE UNIQUE INDEX idx_mv_sales_summary_unique 
ON mv_sales_summary(month, product_category, region);

-- Refresh without blocking reads
REFRESH MATERIALIZED VIEW CONCURRENTLY mv_sales_summary;

-- Create a function for smart refresh
CREATE OR REPLACE FUNCTION refresh_mv_sales_summary()
RETURNS void AS $$
DECLARE
    last_refresh timestamp;
BEGIN
    SELECT last_refresh INTO last_refresh 
    FROM mv_refresh_log 
    WHERE mv_name = 'mv_sales_summary';
    
    IF last_refresh IS NULL OR 
       last_refresh < NOW() - interval '1 hour' THEN
        REFRESH MATERIALIZED VIEW CONCURRENTLY mv_sales_summary;
        
        UPDATE mv_refresh_log 
        SET last_refresh = NOW() 
        WHERE mv_name = 'mv_sales_summary';
    END IF;
END;
$$ LANGUAGE plpgsql;
```

## 2. Recursive Views

### Hierarchical Data Navigation
```sql
CREATE RECURSIVE VIEW employee_hierarchy AS
WITH RECURSIVE emp_tree AS (
    -- Base case: top-level employees
    SELECT 
        id,
        name,
        manager_id,
        1 as level,
        ARRAY[name] as path,
        CAST(id AS text) as path_id
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: employees with managers
    SELECT 
        e.id,
        e.name,
        e.manager_id,
        t.level + 1,
        t.path || e.name,
        t.path_id || ',' || e.id
    FROM employees e
    JOIN emp_tree t ON e.manager_id = t.id
)
SELECT * FROM emp_tree;

-- Usage example: Find all subordinates
CREATE VIEW subordinates_view AS
SELECT 
    e.name as manager_name,
    string_agg(s.name, ', ' ORDER BY s.name) as subordinates,
    COUNT(*) as team_size
FROM employee_hierarchy e
JOIN employee_hierarchy s ON s.path_id LIKE e.path_id || ',%'
GROUP BY e.id, e.name;
```

## 3. Updatable Views with Rules

### Complex Updatable View
```sql
CREATE OR REPLACE VIEW current_employee_details AS
SELECT 
    e.id,
    e.name,
    e.department_id,
    e.salary,
    d.name as department_name,
    e.manager_id,
    m.name as manager_name
FROM employees e
JOIN departments d ON e.department_id = d.id
LEFT JOIN employees m ON e.manager_id = m.id
WHERE e.status = 'active';

-- Make the view updatable
CREATE OR REPLACE RULE current_employee_details_update AS
ON UPDATE TO current_employee_details DO INSTEAD
UPDATE employees SET
    name = NEW.name,
    department_id = NEW.department_id,
    salary = NEW.salary,
    manager_id = NEW.manager_id
WHERE id = OLD.id;

-- Insert rule
CREATE OR REPLACE RULE current_employee_details_insert AS
ON INSERT TO current_employee_details DO INSTEAD
INSERT INTO employees (
    name, department_id, salary, manager_id, status
) VALUES (
    NEW.name, NEW.department_id, NEW.salary, NEW.manager_id, 'active'
);
```

## 4. Parameterized Views

### Using Custom Types
```sql
-- Create custom type for parameters
CREATE TYPE report_params AS (
    start_date date,
    end_date date,
    department_id int
);

-- Create function that returns a table
CREATE OR REPLACE FUNCTION department_performance(params report_params)
RETURNS TABLE (
    department_name text,
    total_sales numeric,
    employee_count int,
    avg_sales_per_employee numeric
) AS $$
BEGIN
    RETURN QUERY
    SELECT 
        d.name,
        SUM(s.amount),
        COUNT(DISTINCT e.id),
        SUM(s.amount) / COUNT(DISTINCT e.id)
    FROM departments d
    JOIN employees e ON d.id = e.department_id
    JOIN sales s ON e.id = s.employee_id
    WHERE s.sale_date BETWEEN params.start_date AND params.end_date
    AND (params.department_id IS NULL OR d.id = params.department_id)
    GROUP BY d.id, d.name;
END;
$$ LANGUAGE plpgsql;

-- Create view that uses the function
CREATE OR REPLACE VIEW department_performance_view AS
SELECT *
FROM department_performance(
    (CURRENT_DATE - interval '30 days',
     CURRENT_DATE,
     NULL)::report_params
);
```

## 5. Materialized View Chains

### Dependent Materialized Views
```sql
-- Base materialized view
CREATE MATERIALIZED VIEW mv_daily_sales AS
SELECT 
    date_trunc('day', sale_timestamp) as sale_date,
    product_id,
    SUM(amount) as daily_total,
    COUNT(*) as daily_transactions
FROM sales
GROUP BY 1, 2
WITH DATA;

-- Dependent materialized view
CREATE MATERIALIZED VIEW mv_product_trends AS
SELECT 
    product_id,
    sale_date,
    daily_total,
    daily_transactions,
    AVG(daily_total) OVER (
        PARTITION BY product_id 
        ORDER BY sale_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) as moving_avg_7day
FROM mv_daily_sales
WITH DATA;

-- Refresh function for view chain
CREATE OR REPLACE FUNCTION refresh_sales_views()
RETURNS void AS $$
BEGIN
    REFRESH MATERIALIZED VIEW mv_daily_sales;
    REFRESH MATERIALIZED VIEW mv_product_trends;
END;
$$ LANGUAGE plpgsql;
```

## 6. View Performance Optimization

### Using Indexes with Materialized Views
```sql
-- Create covering indexes for common queries
CREATE MATERIALIZED VIEW mv_customer_activity AS
SELECT 
    customer_id,
    date_trunc('month', activity_date) as month,
    COUNT(*) as activity_count,
    SUM(amount) as total_spend,
    array_agg(DISTINCT product_id) as products_bought
FROM customer_activities
GROUP BY 1, 2
WITH DATA;

-- Create indexes to support different access patterns
CREATE INDEX idx_mv_customer_activity_customer 
ON mv_customer_activity(customer_id);

CREATE INDEX idx_mv_customer_activity_month 
ON mv_customer_activity(month);

CREATE INDEX idx_mv_customer_activity_amount 
ON mv_customer_activity(total_spend DESC);

-- Create partial indexes for specific conditions
CREATE INDEX idx_mv_customer_activity_high_value 
ON mv_customer_activity(customer_id)
WHERE total_spend > 1000;
```