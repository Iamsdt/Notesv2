#### Available Provider
[Available Provider](https://airflow.apache.org/docs/#active-providers)

****
## **1. Writing a DAG in Python**

A Directed Acyclic Graph (DAG) is the core abstraction in Airflow. It defines the workflow and task dependencies.

### Basic DAG Structure
```python
from datetime import datetime
from airflow import DAG
from airflow.operators.python_operator import PythonOperator

# Define default arguments
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
}

# Initialize DAG
with DAG(
    dag_id='example_dag',
    default_args=default_args,
    description='A simple example DAG',
    schedule_interval='@daily',
    start_date=datetime(2024, 1, 1),
    catchup=False,
) as dag:

    def print_hello():
        print("Hello, Airflow!")

    task = PythonOperator(
        task_id='print_hello',
        python_callable=print_hello,
    )
```

### Key Notes:
- **`DAG`**: The container for your workflow.
- **`PythonOperator`**: Executes Python functions.
- **`schedule_interval`**: Defines the schedule (e.g., `@daily`, `@hourly`).
- **`catchup`**: Prevents past executions from running.

---

## **2. Options for Python Operators**

Airflow offers various operators that use Python extensively:

### PythonOperator
Executes Python callables.
```python
PythonOperator(
    task_id='process_data',
    python_callable=process_data_function,
    op_kwargs={'param': 'value'},  # Pass arguments to the callable
)
```

### BranchPythonOperator
Allows branching based on a condition.
```python
from airflow.operators.python_operator import BranchPythonOperator

def choose_branch(**kwargs):
    return 'branch_1' if kwargs['some_condition'] else 'branch_2'

branch_task = BranchPythonOperator(
    task_id='branching',
    python_callable=choose_branch,
    provide_context=True,
)
```

### PythonVirtualenvOperator
Executes Python code within a virtual environment.
```python
from airflow.operators.python_operator import PythonVirtualenvOperator

virtualenv_task = PythonVirtualenvOperator(
    task_id='venv_task',
    python_callable=lambda: print("Running in a virtualenv!"),
    requirements=["numpy", "pandas"],
    system_site_packages=False,
)
```

---

## **3. Working with Providers**

Providers are integrations for various platforms. Here's how to use five popular ones with Python:

### 1. AWS Provider
Install: `pip install apache-airflow-providers-amazon`

#### Example: S3 File Upload
```python
from airflow.providers.amazon.aws.operators.s3 import S3CreateObjectOperator

upload_task = S3CreateObjectOperator(
    task_id='upload_to_s3',
    aws_conn_id='my_aws_conn',
    s3_bucket='my_bucket',
    s3_key='path/to/file.txt',
    data="Sample Data",
)
```

---

### 2. Google Cloud Provider
Install: `pip install apache-airflow-providers-google`

#### Example: BigQuery Query Execution
```python
from airflow.providers.google.cloud.operators.bigquery import BigQueryExecuteQueryOperator

bq_task = BigQueryExecuteQueryOperator(
    task_id='bq_query',
    sql='SELECT * FROM my_dataset.my_table',
    gcp_conn_id='my_gcp_conn',
    use_legacy_sql=False,
)
```

---

### 3. PostgreSQL Provider
Install: `pip install apache-airflow-providers-postgres`

#### Example: Run SQL on PostgreSQL
```python
from airflow.providers.postgres.operators.postgres import PostgresOperator

sql_task = PostgresOperator(
    task_id='run_postgres_query',
    postgres_conn_id='my_postgres_conn',
    sql='SELECT * FROM my_table;',
)
```

---

### 4. Slack Provider
Install: `pip install apache-airflow-providers-slack`

#### Example: Send Slack Notification
```python
from airflow.providers.slack.operators.slack_webhook import SlackWebhookOperator

slack_task = SlackWebhookOperator(
    task_id='send_slack_message',
    http_conn_id='slack_conn',
    message="Workflow completed successfully!",
    channel="#alerts",
)
```

---

### 5. MySQL Provider
Install: `pip install apache-airflow-providers-mysql`

#### Example: Execute SQL in MySQL
```python
from airflow.providers.mysql.operators.mysql import MySqlOperator

mysql_task = MySqlOperator(
    task_id='mysql_query',
    mysql_conn_id='my_mysql_conn',
    sql='INSERT INTO my_table (id, value) VALUES (1, "test");',
)
```

---

## **5. Python Cheatsheet for Apache Airflow**

| **Component**          | **Python Example**                                                |
| ---------------------- | ----------------------------------------------------------------- |
| **DAG Initialization** | `DAG(dag_id='my_dag', schedule_interval='@daily', ...)`           |
| **PythonOperator**     | `PythonOperator(task_id='task', python_callable=my_func)`         |
| **Branching**          | `BranchPythonOperator(task_id='branch', python_callable=my_func)` |
| **S3 Upload**          | `S3CreateObjectOperator(..., s3_key='path/to/file.txt')`          |
| **SQL Execution**      | `PostgresOperator(sql='SELECT * FROM table;')`                    |
| **BigQuery**           | `BigQueryExecuteQueryOperator(sql='SELECT * FROM table')`         |
| **Slack Notification** | `SlackWebhookOperator(message="Job done!")`                       |
| **Virtualenv**         | `PythonVirtualenvOperator(python_callable=my_func, ...)`          |

---

## **Working with Apache Spark in Airflow**

Apache Spark is a distributed data processing framework widely used for big data tasks. In Airflow, we can manage and orchestrate Spark jobs using operators such as:
- **`SparkSubmitOperator`**: Submits a Spark job directly to a cluster.
- **`EmrAddStepsOperator`**: Submits a Spark job to an Amazon EMR cluster.
- **`DataprocSubmitJobOperator`**: Submits a Spark job to Google Dataproc.

These operators allow us to control Spark jobs programmatically within Airflow workflows.

---
### **Complex Workflow: Conditional Spark Job Execution**

#### **Workflow Logic:**

1. Execute `spark_job_1`.
2. Execute `spark_job_2`.
3. If `spark_job_2` fails, run `spark_job_3`.
4. If `spark_job_2` succeeds, run `spark_job_4`.

---
### **DAG Implementation**

#### Step 1: Import Required Modules

```python
from airflow import DAG
from airflow.operators.dummy_operator import DummyOperator
from airflow.providers.apache.spark.operators.spark_submit import SparkSubmitOperator
from airflow.operators.python_operator import BranchPythonOperator
from datetime import datetime
```

#### Step 2: Define the DAG and Default Arguments

```python
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'email_on_failure': False,
    'retries': 1,
}

dag = DAG(
    dag_id='spark_conditional_jobs',
    default_args=default_args,
    description='A DAG with conditional Spark job execution',
    schedule_interval=None,
    start_date=datetime(2023, 12, 1),
    catchup=False,
)
```

#### Step 3: Define the SparkSubmitOperator Jobs

```python
# Spark Job 1
spark_job_1 = SparkSubmitOperator(
    task_id='spark_job_1',
    application='/path/to/spark_job_1.py',
    conn_id='spark_default',  # Connection to your Spark cluster
    application_args=['arg1', 'arg2'],
    dag=dag,
)

# Spark Job 2
spark_job_2 = SparkSubmitOperator(
    task_id='spark_job_2',
    application='/path/to/spark_job_2.py',
    conn_id='spark_default',
    application_args=['arg1', 'arg2'],
    dag=dag,
)

# Spark Job 3
spark_job_3 = SparkSubmitOperator(
    task_id='spark_job_3',
    application='/path/to/spark_job_3.py',
    conn_id='spark_default',
    application_args=['arg1', 'arg2'],
    dag=dag,
)

# Spark Job 4
spark_job_4 = SparkSubmitOperator(
    task_id='spark_job_4',
    application='/path/to/spark_job_4.py',
    conn_id='spark_default',
    application_args=['arg1', 'arg2'],
    dag=dag,
)
```

#### Step 4: Branch Logic Using BranchPythonOperator

```python
def choose_next_task(**kwargs):
    # Check the state of spark_job_2
    task_instance = kwargs['ti']
    spark_job_2_state = task_instance.xcom_pull(task_ids='spark_job_2', key='return_value')

    # Return the task to execute next
    if spark_job_2_state == 'failed':
        return 'spark_job_3'
    return 'spark_job_4'

branch_task = BranchPythonOperator(
    task_id='branch_task',
    python_callable=choose_next_task,
    provide_context=True,
    dag=dag,
)
```

#### Step 5: Define the Task Dependencies

```python
start = DummyOperator(task_id='start', dag=dag)
end = DummyOperator(task_id='end', dag=dag)

# Define dependencies
start >> spark_job_1
spark_job_1 >> spark_job_2
spark_job_2 >> branch_task
branch_task >> spark_job_3 >> end
branch_task >> spark_job_4 >> end
```

---

### **Explanation of Components**
1. **`SparkSubmitOperator`**:
    - Used to submit Spark jobs to a cluster.
    - Specify the application path, connection ID, and arguments for the Spark job.
2. **`BranchPythonOperator`**:
    - Dynamically determines the next task based on the state of a previous task.
    - In this case, it checks if `spark_job_2` succeeded or failed.
3. **Dependencies**:
    - The workflow ensures sequential execution from `spark_job_1` to `spark_job_2` and conditional branching to `spark_job_3` or `spark_job_4`.

---

### **Python Cheatsheet for Spark in Airflow**

|**Component**|**Python Example**|
|---|---|
|**SparkSubmitOperator**|`SparkSubmitOperator(application='/path/app.py', ...)`|
|**BranchPythonOperator**|`BranchPythonOperator(python_callable=my_func, ...)`|
|**Conditional Execution**|`branch_task >> task_1 >> end` or `branch_task >> task_2`|
|**Task Dependency**|`task_1 >> task_2 >> task_3`|
