Code:
```sql
-- Create tables
CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    department_id INTEGER,
    salary DECIMAL(10,2),
    hire_date DATE,
    manager_id INTEGER
);

CREATE TABLE departments (
    department_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    budget DECIMAL(15,2)
);

CREATE TABLE sales (
    sale_id SERIAL PRIMARY KEY,
    employee_id INTEGER,
    sale_date DATE,
    amount DECIMAL(10,2),
    customer_id INTEGER
);

CREATE TABLE projects (
    project_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    start_date DATE,
    end_date DATE,
    budget DECIMAL(15,2),
    status VARCHAR(20)
);

CREATE TABLE project_assignments (
    assignment_id SERIAL PRIMARY KEY,
    project_id INTEGER,
    employee_id INTEGER,
    role VARCHAR(50),
    assignment_date DATE,
    hours_allocated INTEGER
);

-- Insert sample data
INSERT INTO departments (name, budget) VALUES
('Engineering', 1000000),
('Sales', 800000),
('Marketing', 600000),
('HR', 400000),
('Operations', 750000);

INSERT INTO employees (name, department_id, salary, hire_date, manager_id) VALUES
('John Doe', 1, 85000, '2020-01-15', NULL),
('Jane Smith', 1, 75000, '2020-03-20', 1),
('Bob Johnson', 2, 65000, '2021-02-10', 1),
('Alice Brown', 2, 72000, '2021-04-05', 3),
('Charlie Wilson', 3, 68000, '2021-06-15', 1),
('Diana Miller', 3, 71000, '2021-08-22', 5),
('Eva Davis', 4, 59000, '2022-01-10', 1),
('Frank Thomas', 4, 63000, '2022-03-15', 7),
('Grace Lee', 5, 81000, '2022-05-20', 1),
('Henry Martin', 5, 77000, '2022-07-25', 9);

INSERT INTO sales (employee_id, sale_date, amount, customer_id) VALUES
(3, '2023-01-15', 5000, 1),
(3, '2023-01-16', 7500, 2),
(4, '2023-01-16', 10000, 3),
(3, '2023-01-17', 6000, 4),
(4, '2023-01-17', 8500, 5),
(3, '2023-01-18', 12000, 6),
(4, '2023-01-18', 9000, 7),
(3, '2023-01-19', 15000, 8),
(4, '2023-01-19', 11000, 9),
(3, '2023-01-20', 13000, 10);

INSERT INTO projects (name, start_date, end_date, budget, status) VALUES
('Project Alpha', '2023-01-01', '2023-06-30', 200000, 'In Progress'),
('Project Beta', '2023-02-15', '2023-08-31', 150000, 'In Progress'),
('Project Gamma', '2023-03-01', '2023-12-31', 300000, 'Planning'),
('Project Delta', '2023-04-15', '2024-01-31', 250000, 'In Progress'),
('Project Epsilon', '2023-05-01', '2023-11-30', 180000, 'Completed');

INSERT INTO project_assignments (project_id, employee_id, role, assignment_date, hours_allocated) VALUES
(1, 1, 'Project Manager', '2023-01-01', 160),
(1, 2, 'Developer', '2023-01-01', 120),
(1, 3, 'Analyst', '2023-01-01', 80),
(2, 4, 'Project Manager', '2023-02-15', 160),
(2, 5, 'Developer', '2023-02-15', 120),
(3, 6, 'Project Manager', '2023-03-01', 160),
(3, 7, 'Analyst', '2023-03-01', 80),
(4, 8, 'Developer', '2023-04-15', 120),
(4, 9, 'Project Manager', '2023-04-15', 160),
(5, 10, 'Analyst', '2023-05-01', 80);
```

1. Calculate a running total of sales amount for each employee, but reset the running total when the day changes. Also include the percentage of daily total that each sale represents. Order by employee_id and sale_date.
```
employee_id | sale_date  | amount | daily_running_total | daily_percentage
3          | 2023-01-15 | 5000   | 5000               | 100.00
3          | 2023-01-16 | 7500   | 7500               | 42.86
4          | 2023-01-16 | 10000  | 17500              | 57.14
```

2.For each department, find employees whose salary is higher than their department's average, but lower than the overall company average. Include the department name, employee name, their salary, their department's average salary, and the company average salary.
```
dept_name   | employee_name | employee_salary | dept_avg_salary | company_avg_salary
Engineering | Jane Smith    | 75000.00       | 70000.00        | 72000.00
Sales      | Alice Brown   | 72000.00       | 68500.00        | 72000.00
```

3. Create a hierarchical view of the employee management structure, showing the levels of management (depth), total salary under each manager (including their own salary), and the percentage of company total salary that their tree represents
```
level | manager_name | subordinate_name | depth | total_tree_salary | salary_percentage
1     | John Doe     | NULL            | 0     | 85000.00         | 100.00
2     | Jane Smith   | Bob Johnson     | 1     | 140000.00        | 82.35
3     | Bob Johnson  | Alice Brown     | 2     | 137000.00        | 80.59
```

5. Find projects where the total allocated hours exceed the average allocated hours across all projects by at least 20%, and show the ratio of senior roles (Project Manager) to other roles in these projects
```
project_name | total_hours | avg_project_hours | hours_difference_pct | pm_ratio
Project Alpha| 360         | 300              | 20.00               | 0.33
Project Beta | 400         | 300              | 33.33               | 0.25
```

7. Calculate the quartile distribution of sales amounts for each employee, but only consider sales that are above the employee's median sale amount. Include the employee name and their average sale amount in the final results
```
employee_name | quartile | min_sale | max_sale | avg_sale | median_sale
Bob Johnson   | Q3       | 12000    | 15000    | 13500    | 7500
Alice Brown   | Q4       | 15000    | 20000    | 17500    | 9000
```

9. For each employee, calculate a 3-day moving average of their sales, along with the difference from the previous day's 3-day moving average, showing null for differences that can't be calculated
```
employee_id | sale_date  | amount | three_day_avg | prev_day_diff
3          | 2023-01-15 | 5000   | 5000.00      | NULL
3          | 2023-01-16 | 7500   | 6250.00      | 1250.00
3          | 2023-01-17 | 6000   | 6166.67      | -83.33
```


11. Find employees who have worked on more projects than the average number of projects per employee in their department, and show the percentage of department projects they've worked on. Only consider departments with at least 3 employees
```
dept_name   | employee_name | projects_count | dept_avg_projects | participation_pct
Engineering | John Doe      | 4              | 2.5              | 160.00
Sales       | Bob Johnson   | 3              | 2.0              | 150.00
```


13. Create a report showing the budget utilization across departments and projects. For each department that has employees assigned to projects, calculate the percentage of department budget allocated to projects (based on the ratio of employee hours allocated to projects vs. standard 160 hours), and the weighted average project completion rate
```
dept_name   | total_budget | allocated_budget | utilization_pct | avg_completion_rate
Engineering | 1000000.00   | 750000.00       | 75.00          | 85.50
Sales       | 800000.00    | 600000.00       | 75.00          | 77.25
```

1. Find periods of consecutive days where sales increased day over day for each employee. Show the employee name, start date, end date, number of consecutive days, and total amount of sales during that period
```
employee_name | start_date | end_date   | consecutive_days | total_amount
Bob Johnson   | 2023-01-15 | 2023-01-18 | 4               | 30500.00
Alice Brown   | 2023-01-16 | 2023-01-19 | 4               | 38500.00
```

1. For each project, calculate the optimal distribution of remaining hours (total budget hours - allocated hours) among currently assigned employees based on their current allocation ratio, but with the constraints that no employee should be allocated more than 160 hours per month and employees with 'Project Manager' roles should not exceed 60% of their current allocation

```
project_name | employee_name | current_hours | optimal_additional_hours | total_new_hours
Project Alpha| John Doe      | 160          | 40                      | 200
Project Alpha| Jane Smith    | 120          | 30                      | 150
Project Beta | Bob Johnson   | 80           | 20                      | 100
```

Answer: 
```
WITH daily_totals AS (
    SELECT 
        sale_date,
        employee_id,
        SUM(amount) as daily_total
    FROM sales
    GROUP BY sale_date, employee_id
)
SELECT 
    s.employee_id,
    s.sale_date,
    s.amount,
    SUM(s.amount) OVER (
        PARTITION BY s.employee_id, s.sale_date
        ORDER BY s.sale_id
    ) as daily_running_total,
    ROUND(
        (s.amount * 100.0) / dt.daily_total,
        2
    ) as daily_percentage
FROM sales s
JOIN daily_totals dt 
    ON s.sale_date = dt.sale_date 
    AND s.employee_id = dt.employee_id
ORDER BY s.employee_id, s.sale_date, s.sale_id;
```

2 
```
WITH dept_avgs AS (
    SELECT 
        department_id,
        AVG(salary) as dept_avg_salary
    FROM employees
    GROUP BY department_id
),
company_avg AS (
    SELECT AVG(salary) as company_avg_salary
    FROM employees
)
SELECT 
    d.name as dept_name,
    e.name as employee_name,
    e.salary as employee_salary,
    ROUND(da.dept_avg_salary, 2) as dept_avg_salary,
    ROUND(ca.company_avg_salary, 2) as company_avg_salary
FROM employees e
JOIN departments d ON e.department_id = d.department_id
JOIN dept_avgs da ON e.department_id = da.department_id
CROSS JOIN company_avg ca
WHERE e.salary > da.dept_avg_salary 
    AND e.salary < ca.company_avg_salary
ORDER BY d.name, e.salary DESC;
```

3
```
WITH RECURSIVE emp_hierarchy AS (
    -- Base case: top-level managers (employees with no manager)
    SELECT 
        employee_id,
        name,
        manager_id,
        salary,
        0 as depth,
        ARRAY[employee_id] as path
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: employees with managers
    SELECT 
        e.employee_id,
        e.name,
        e.manager_id,
        e.salary,
        eh.depth + 1,
        eh.path || e.employee_id
    FROM employees e
    INNER JOIN emp_hierarchy eh ON e.manager_id = eh.employee_id
),
salary_totals AS (
    SELECT 
        eh.employee_id,
        eh.name as manager_name,
        eh.depth,
        SUM(e.salary) as total_tree_salary
    FROM emp_hierarchy eh
    JOIN employees e ON e.employee_id = ANY(eh.path)
    GROUP BY eh.employee_id, eh.name, eh.depth
),
company_total AS (
    SELECT SUM(salary) as total_salary FROM employees
)
SELECT 
    st.depth + 1 as level,
    st.manager_name,
    e.name as subordinate_name,
    st.depth,
    st.total_tree_salary,
    ROUND((st.total_tree_salary * 100.0 / ct.total_salary), 2) as salary_percentage
FROM salary_totals st
LEFT JOIN employees e ON e.manager_id = st.employee_id
CROSS JOIN company_total ct
ORDER BY st.depth, st.manager_name, e.name;
```

4 
```
WITH project_stats AS (
    SELECT 
        p.project_id,
        p.name as project_name,
        SUM(pa.hours_allocated) as total_hours,
        COUNT(CASE WHEN pa.role = 'Project Manager' THEN 1 END)::float / 
        COUNT(*)::float as pm_ratio
    FROM projects p
    JOIN project_assignments pa ON p.project_id = pa.project_id
    GROUP BY p.project_id, p.name
),
avg_hours AS (
    SELECT AVG(total_hours) as avg_project_hours
    FROM project_stats
)
SELECT 
    ps.project_name,
    ps.total_hours,
    ROUND(ah.avg_project_hours, 2) as avg_project_hours,
    ROUND(((ps.total_hours - ah.avg_project_hours) * 100.0 / ah.avg_project_hours), 2) as hours_difference_pct,
    ROUND(ps.pm_ratio::numeric, 2) as pm_ratio
FROM project_stats ps
CROSS JOIN avg_hours ah
WHERE ps.total_hours > (ah.avg_project_hours * 1.2)
ORDER BY hours_difference_pct DESC;

```

5
```
WITH sales_median AS (
    SELECT 
        s.employee_id,
        PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY s.amount) AS median_sale
    FROM sales s
    GROUP BY s.employee_id
),
sales_stats AS (
    SELECT 
        s.employee_id,
        e.name AS employee_name,
        s.amount,
        sm.median_sale,
        NTILE(4) OVER (PARTITION BY s.employee_id ORDER BY s.amount) AS quartile
    FROM sales s
    JOIN employees e ON s.employee_id = e.employee_id
    JOIN sales_median sm ON s.employee_id = sm.employee_id
)
SELECT 
    employee_name,
    'Q' || quartile AS quartile,
    MIN(amount) AS min_sale,
    MAX(amount) AS max_sale,
    ROUND(AVG(amount::numeric), 2) AS avg_sale,
    ROUND(MAX(median_sale::numeric), 2) AS median_sale
FROM sales_stats
WHERE amount > median_sale
GROUP BY employee_name, quartile
ORDER BY employee_name, quartile;


```


# Appace Spark
I'll create 5 challenging questions focused on Apache Spark and Apache Beam processing scenarios. For each, I'll provide the input data structure, expected output, and specific requirements.

```python
# Sample data generation for both Spark and Beam exercises

# 1. User Events Data
user_events = """
timestamp,user_id,event_type,product_id,amount
2024-01-01 10:00:00,user1,view,prod1,0
2024-01-01 10:01:00,user1,add_to_cart,prod1,0
2024-01-01 10:02:00,user1,purchase,prod1,100
2024-01-01 10:00:00,user2,view,prod2,0
2024-01-01 10:05:00,user2,view,prod3,0
2024-01-01 10:06:00,user2,add_to_cart,prod3,0
2024-01-01 10:07:00,user2,purchase,prod3,150
2024-01-01 10:10:00,user3,view,prod1,0
2024-01-01 10:15:00,user3,view,prod2,0
"""

# 2. Product Catalog Data
product_catalog = """
product_id,category,price,inventory
prod1,electronics,100,50
prod2,electronics,200,30
prod3,clothing,150,100
prod4,clothing,75,200
"""

# 3. User Profile Data
user_profiles = """
user_id,signup_date,country,segment
user1,2023-12-01,US,premium
user2,2023-11-15,UK,standard
user3,2023-12-15,US,standard
user4,2023-12-20,CA,premium
"""

# 4. Error Logs Data
error_logs = """
timestamp,service_name,error_code,severity,message
2024-01-01 10:00:01,auth-service,500,HIGH,Database connection failed
2024-01-01 10:00:05,payment-service,404,MEDIUM,Resource not found
2024-01-01 10:00:10,auth-service,500,HIGH,Database connection failed
2024-01-01 10:01:00,cart-service,400,LOW,Invalid request
2024-01-01 10:01:30,auth-service,500,HIGH,Database connection failed
"""

# 5. Transaction Data with Late Events
transaction_data = """
timestamp,transaction_id,user_id,amount,status
2024-01-01 10:00:00,tx1,user1,100,completed
2024-01-01 09:58:00,tx2,user2,150,completed
2024-01-01 10:05:00,tx3,user3,200,pending
2024-01-01 10:02:00,tx4,user4,300,failed
2024-01-01 09:55:00,tx5,user5,250,completed
"""

```

Here are 5 complex questions using this data:

1. Session Analysis with Fixed-time Windows (Apache Beam)
Question: Implement a pipeline that analyzes user sessions where a session is defined as a sequence of events from the same user within a 5-minute window. Calculate the conversion rate (views to purchases) for each product category. Handle late data by using allowed lateness of 1 minute.

Expected Output:
```
window_start    | window_end      | category    | total_views | total_purchases | conversion_rate
2024-01-01 10:00| 2024-01-01 10:05| electronics | 3           | 1              | 33.33
2024-01-01 10:00| 2024-01-01 10:05| clothing    | 1           | 1              | 100.00
```

2. Error Pattern Detection (Apache Spark)
Question: Using the error logs data, implement a Spark streaming solution that detects error patterns and potential service degradation. Consider a service as degraded if it has 3 or more HIGH severity errors within any 2-minute window. Output should include the service name, time window, and error frequency pattern.

Expected Output:
```
service_name | window_start      | window_end        | error_count | pattern_severity | is_degraded
auth-service | 2024-01-01 10:00  | 2024-01-01 10:02 | 3           | HIGH            | true
```

3. Real-time User Journey Analysis (Apache Beam)
Question: Create a pipeline that tracks the complete user journey from view to purchase, calculating the time taken between each step (view → add_to_cart → purchase). Implement this using Apache Beam's stateful processing to maintain user state. Consider only completed journeys (those that end in purchase) and handle out-of-order events.

Expected Output:
```
user_id | product_id | view_time          | cart_time          | purchase_time      | view_to_cart_secs | cart_to_purchase_secs
user1   | prod1      | 2024-01-01 10:00:00| 2024-01-01 10:01:00| 2024-01-01 10:02:00| 60                | 60
```

4. Dynamic Sessionization with Custom Triggers (Apache Spark)
Question: Implement a Spark Structured Streaming solution that creates dynamic sessions based on user activity. A session ends if there's no activity for 2 minutes or if a purchase event occurs. Calculate total session value and session duration for each user segment.

Expected Output:
```
user_id | segment | session_start      | session_end        | session_duration_secs | total_value | event_count
user1   | premium | 2024-01-01 10:00:00| 2024-01-01 10:02:00| 120                  | 100         | 3
```

5. Cross-Pipeline Join with Time Skew (Apache Beam)
Question: Implement a solution that joins the transaction data with user events while handling time skew between the two streams. Consider transactions that might arrive before their corresponding events and vice versa. Implement a custom window strategy that waits for late data up to 5 minutes and matches transactions with their corresponding user journey events.

Expected Output:
```
transaction_id | user_id | journey_start      | journey_end        | transaction_time    | total_amount | status    | events_before_tx
tx1           | user1   | 2024-01-01 10:00:00| 2024-01-01 10:02:00| 2024-01-01 10:00:00| 100          | completed | 2
```

Would you like me to provide the solution for any of these questions? Each solution would include:
1. Detailed code implementation
2. Explanation of the key concepts used
3. How to handle edge cases
4. Performance considerations
5. Testing strategies

Which question would you like to start with?


```
import apache_beam as beam
from apache_beam import window
from apache_beam.transforms import trigger
from datetime import datetime
import json

class ParseEventFn(beam.DoFn):
    def process(self, element):
        record = element.split(',')
        return [{
            'timestamp': datetime.strptime(record[0], '%Y-%m-%d %H:%M:%S'),
            'user_id': record[1],
            'event_type': record[2],
            'product_id': record[3],
            'amount': float(record[4])
        }]

class AddProductCategoryFn(beam.DoFn):
    def process(self, element, product_catalog):
        product_id = element['product_id']
        category = next((p['category'] for p in product_catalog if p['product_id'] == product_id), None)
        if category:
            element['category'] = category
            yield element

def calculate_conversion_rates(pc, window_start, window_end):
    by_category = {}
    for event in pc:
        cat = event['category']
        if cat not in by_category:
            by_category[cat] = {'views': 0, 'purchases': 0}
        if event['event_type'] == 'view':
            by_category[cat]['views'] += 1
        elif event['event_type'] == 'purchase':
            by_category[cat]['purchases'] += 1
    
    for cat, stats in by_category.items():
        views = stats['views']
        purchases = stats['purchases']
        conversion_rate = (purchases / views * 100) if views > 0 else 0
        yield {
            'window_start': window_start.strftime('%Y-%m-%d %H:%M'),
            'window_end': window_end.strftime('%Y-%m-%d %H:%M'),
            'category': cat,
            'total_views': views,
            'total_purchases': purchases,
            'conversion_rate': round(conversion_rate, 2)
        }

def run_pipeline(p, input_data, product_catalog):
    return (
        p 
        | 'Read Events' >> beam.Create(input_data.split('\n'))
        | 'Parse Events' >> beam.ParDo(ParseEventFn())
        | 'Add Timestamps' >> beam.Map(
            lambda x: beam.window.TimestampedValue(x, x['timestamp'].timestamp()))
        | 'Fixed Windows' >> beam.WindowInto(
            window.FixedWindows(300),  # 5-minute windows
            trigger=trigger.AfterWatermark(
                early=trigger.AfterCount(1),
                late=trigger.AfterCount(1)
            ),
            allowed_lateness=60,  # 1 minute allowed lateness
            accumulation_mode=trigger.AccumulationMode.DISCARDING
        )
        | 'Add Category' >> beam.ParDo(AddProductCategoryFn(), product_catalog)
        | 'Group by Window' >> beam.GroupByKey()
        | 'Calculate Conversion' >> beam.FlatMap(
            lambda x: calculate_conversion_rates(x[1], x[0].start, x[0].end)
        )
    )
```

```
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from pyspark.sql.types import *
from pyspark.sql.window import Window

# Create Spark Session
spark = SparkSession.builder \
    .appName("Error Pattern Detection") \
    .getOrCreate()

# Define schema for error logs
error_schema = StructType([
    StructField("timestamp", TimestampType(), True),
    StructField("service_name", StringType(), True),
    StructField("error_code", IntegerType(), True),
    StructField("severity", StringType(), True),
    StructField("message", StringType(), True)
])

def detect_error_patterns(input_df):
    # Convert timestamp to timestamp type if it's string
    if isinstance(input_df.schema["timestamp"].dataType, StringType):
        input_df = input_df.withColumn(
            "timestamp", 
            to_timestamp("timestamp", "yyyy-MM-dd HH:mm:ss")
        )

    # Create 2-minute tumbling windows
    windowed_errors = input_df \
        .withWatermark("timestamp", "1 minute") \
        .groupBy(
            window("timestamp", "2 minutes"),
            "service_name",
            "severity"
        ) \
        .agg(
            count("*").alias("error_count"),
            collect_list("error_code").alias("error_codes")
        )

    # Filter for degraded services
    degraded_services = windowed_errors \
        .filter(
            (col("severity") == "HIGH") & 
            (col("error_count") >= 3)
        ) \
        .withColumn("window_start", col("window").getField("start")) \
        .withColumn("window_end", col("window").getField("end")) \
        .withColumn("is_degraded", lit(True)) \
        .withColumn(
            "pattern_severity", 
            when(col("error_count") >= 5, "CRITICAL")
            .when(col("error_count") >= 3, "HIGH")
            .otherwise("MEDIUM")
        )

    # Select final columns
    result = degraded_services.select(
        "service_name",
        "window_start",
        "window_end",
        "error_count",
        "pattern_severity",
        "is_degraded"
    ).orderBy("window_start", "service_name")

    return result

# For streaming application
def process_stream(input_stream):
    return detect_error_patterns(input_stream) \
        .writeStream \
        .outputMode("append") \
        .format("console") \
        .start()
```

```
import apache_beam as beam
from apache_beam.transforms import window
from apache_beam.transforms.userstate import BagStateSpec, TimerSpec
from datetime import datetime, timedelta

class UserJourneyStatefulFn(beam.DoFn):
    JOURNEY_STATE = BagStateSpec('journey', beam.coders.PickleCoder())
    JOURNEY_TIMER = TimerSpec('journey_timer', beam.coders.TimeDomain.REAL_TIME)
    
    def process_timer(self, timer_time, journey_state=beam.DoFn.StateParam(JOURNEY_STATE)):
        journey_events = list(journey_state.read())
        if journey_events:
            journey_events.sort(key=lambda x: x['timestamp'])
            if self._is_complete_journey(journey_events):
                yield self._create_journey_summary(journey_events)
        journey_state.clear()
    
    def process(self, 
                element,
                journey_state=beam.DoFn.StateParam(JOURNEY_STATE),
                timer=beam.DoFn.TimerParam(JOURNEY_TIMER)):
        
        current_events = list(journey_state.read())
        current_events.append(element)
        journey_state.clear()
        journey_state.add(element)
        
        # Set timer for 5 minutes after event
        timer_timestamp = element['timestamp'] + timedelta(minutes=5)
        timer.set(timer_timestamp)
        
        if self._is_complete_journey(current_events):
            yield self._create_journey_summary(current_events)
    
    def _is_complete_journey(self, events):
        event_types = set(e['event_type'] for e in events)
        return {'view', 'add_to_cart', 'purchase'}.issubset(event_types)
    
    def _create_journey_summary(self, events):
        events_by_type = {e['event_type']: e for e in sorted(events, key=lambda x: x['timestamp'])}
        view_time = events_by_type['view']['timestamp']
        cart_time = events_by_type['add_to_cart']['timestamp']
        purchase_time = events_by_type['purchase']['timestamp']
        
        return {
            'user_id': events[0]['user_id'],
            'product_id': events[0]['product_id'],
            'view_time': view_time,
            'cart_time': cart_time,
            'purchase_time': purchase_time,
            'view_to_cart_secs': int((cart_time - view_time).total_seconds()),
            'cart_to_purchase_secs': int((purchase_time - cart_time).total_seconds())
        }

def run_pipeline(p, input_data):
    return (
        p
        | 'Read Events' >> beam.Create(input_data.split('\n'))
        | 'Parse Events' >> beam.ParDo(ParseEventFn())
        | 'Key By User-Product' >> beam.Map(
            lambda x: ((x['user_id'], x['product_id']), x))
        | 'Group and Process Journey' >> beam.ParDo(UserJourneyStatefulFn())
        | 'Format Output' >> beam.Map(format_journey_output)
    )

def format_journey_output(journey):
    return '{user_id},{product_id},{view_time},{cart_time},{purchase_time},{view_to_cart_secs},{cart_to_purchase_secs}'.format(**journey)
```

```
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from pyspark.sql.window import Window

def create_dynamic_sessions(events_df, user_profiles_df):
    # Join with user profiles to get segment information
    enriched_events = events_df.join(
        user_profiles_df,
        "user_id"
    )
    
    # Window specification for session identification
    user_window = Window.partitionBy("user_id").orderBy("timestamp")
    
    # Mark session boundaries
    sessioned_events = enriched_events \
        .withColumn("prev_timestamp",
            lag("timestamp").over(user_window)
        ) \
        .withColumn("time_diff_seconds",
            when(col("prev_timestamp").isNotNull(),
                unix_timestamp("timestamp") - unix_timestamp("prev_timestamp")
            ).otherwise(0)
        ) \
        .withColumn("new_session",
            (col("time_diff_seconds") > 120) |  # 2 minutes inactivity
            (col("event_type") == "purchase") |  # Purchase ends session
            (col("prev_timestamp").isNull())     # First event
        )
    
    # Generate session IDs
    events_with_sessions = sessioned_events \
        .withColumn("session_id",
            sum("new_session").over(user_window)
        )
    
    # Calculate session metrics
    session_metrics = events_with_sessions \
        .groupBy("user_id", "segment", "session_id") \
        .agg(
            min("timestamp").alias("session_start"),
            max("timestamp").alias("session_end"),
            count("*").alias("event_count"),
            sum(when(col("event_type") == "purchase", col("amount")).otherwise(0))
                .alias("total_value")
        ) \
        .withColumn("session_duration_secs",
            unix_timestamp("session_end") - unix_timestamp("session_start")
        )
    
    return session_metrics.select(
        "user_id",
        "segment",
        "session_start",
        "session_end",
        "session_duration_secs",
        "total_value",
        "event_count"
    )

# For streaming application
def process_stream(events_stream, user_profiles_df):
    return create_dynamic_sessions(events_stream, user_profiles_df) \
        .writeStream \
        .outputMode("append") \
        .format("console") \
        .trigger(processingTime="1 minute") \
        .start()
```

```
import apache_beam as beam
from apache_beam import window
from apache_beam.transforms import trigger
from datetime import datetime, timedelta

class JoinedDataStatefulFn(beam.DoFn):
    EVENTS_STATE = BagStateSpec('events', beam.coders.PickleCoder())
    TRANSACTION_STATE = BagStateSpec('transaction', beam.coders.PickleCoder())
    CLEANUP_TIMER = TimerSpec('cleanup', beam.coders.TimeDomain.REAL_TIME)
    
    def process(self,
                element,
                events_state=beam.DoFn.StateParam(EVENTS_STATE),
                transaction_state=beam.DoFn.StateParam(TRANSACTION_STATE),
                timer=beam.DoFn.TimerParam(CLEANUP_TIMER)):
        
        # Set cleanup timer
        cleanup_time = element['timestamp'] + timedelta(minutes=5)
        timer.set(cleanup_time)
        
        if 'transaction_id' in element:
            # Process transaction
            transaction_state.add(element)
        else:
            # Process event
            events_state.add(element)
        
        # Try to match and emit
        transactions = list(transaction_state.read())
        events = list(events_state.read())
        
        for tx in transactions:
            matched_events = [e for e in events 
                            if e['user_id'] == tx['user_id'] and
                            e['timestamp'] <= tx['timestamp']]
            
            if matched_events:
                yield self._create_joined_record(tx, matched_events)
    
    def process_timer(self,
                     timer_time,
                     events_state=beam.DoFn.StateParam(EVENTS_STATE),
                     transaction_state=beam.DoFn.StateParam(TRANSACTION_STATE)):
        # Clean up old state
        events_state.clear()
        transaction_state.clear()
    
    def _create_joined_record(self, transaction, events):
        events.sort(key=lambda x: x['timestamp'])
        return {
            'transaction_id': transaction['transaction_id'],
            'user_id': transaction['user_id'],
            'journey_start': events[0]['timestamp'],
            'journey_end': events[-1]['timestamp'],
            'transaction_time': transaction['timestamp'],
            'total_amount': transaction['amount'],
            'status': transaction['status'],
            'events_before_tx': len(events)
        }

def run_pipeline(p, events_data, transactions_data):
    events = (p 
        | 'Read Events' >> beam.Create(events_data.split('\n'))
        | 'Parse Events' >> beam.ParDo(ParseEventFn()))
    
    transactions = (p
        | 'Read Transactions' >> beam.Create(transactions_data.split('\n'))
        | 'Parse Transactions' >> beam.ParDo(ParseTransactionFn()))
    
    return ((events, transactions)
        | 'Flatten' >> beam.Flatten()
        | 'Ad
```



VM:
```
WITH dept_avg AS ( SELECT e.department_id, d.name AS dept_name, ROUND(AVG(e.salary), 2) AS dept_avg_salary FROM employees e JOIN departments d ON e.department_id = d.department_id GROUP BY e.department_id, d.name ), company_avg AS ( SELECT ROUND(AVG(salary), 2) AS company_avg_salary FROM employees ) SELECT e.name AS employee_name, d.name AS dept_name, ROUND(e.salary, 2) AS employee_salary, da.dept_avg_salary, ca.company_avg_salary FROM employees e JOIN departments d ON e.department_id = d.department_id JOIN dept_avg da ON e.department_id = da.department_id JOIN company_avg ca ON true WHERE e.salary > da.dept_avg_salary AND e.salary < ca.company_avg_salary ORDER BY e.department_id, e.name; SELECT d.name AS dept_name, ROUND(AVG(e.salary), 2) AS dept_avg_salary FROM employees e JOIN departments d ON e.department_id = d.department_id GROUP BY d.name;

```