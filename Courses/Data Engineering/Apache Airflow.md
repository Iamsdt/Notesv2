---
Created by: Shudipto Trafder
Last edited time: 2024-12-09T20:27:00
tags:
  - airflow
---
## What is Airflow

Apache Airflow is an open-source platform to programatically author, schedule, and monitor workflows.

## Why Use Airflow

Problem Statement: We need to automate a pipeline where we need to run a set of tasks which run daily at 12.00 am UTC. Steps are:
1. Load Data
2. Transform Data
3. Store data in HDFS

- Traditional Approach: Cron Jobs (no UI, error handling, execution dependency, logs are not centralized)

To solve this, we can use Airflow. Airflow allows for the creation and management of complex workflows. It's used to orchestrate data pipelines, ensuring tasks are executed in the correct order and at the right time.

## How it Works

![Basic Flow](https://airflow.apache.org/docs/apache-airflow/stable/_images/diagram_basic_airflow_architecture.png)

## Features

- **Dynamic Pipelines**: Define workflows as code using Python.
- **Scalable**: Scales horizontally to handle increased workloads.
- **Extensible**: Custom plugins and operators, executor can be added.
- **Rich UI**: Provides a web interface for monitoring and managing workflows.

Airflow is not a data streaming solution or ETL tool. Tasks don't move data from one to another (though we can use metadata to move data).

## Architecture

Airflow's architecture consists of the following components:
![image](https://airflow.apache.org/docs/apache-airflow/2.1.4/_images/arch-diag-basic.png)

- **Scheduler**: The Scheduler handles the scheduling of tasks according to the workflows defined in DAGs (Directed Acyclic Graphs). It continuously monitors the DAGs for any changes or new tasks to execute and decides when to trigger them based on their dependencies and scheduling intervals.

- **Executor**: The Executor determines how and where tasks are executed. It manages the execution of tasks by communicating with the workers. Airflow supports different executors like SequentialExecutor for local execution and CeleryExecutor for distributed execution across multiple nodes.

- **Workers**: Workers are the processes that execute the tasks assigned by the Executor. In a distributed setup, multiple worker nodes can run in parallel, allowing Airflow to scale and handle large volumes of tasks efficiently.

- **Metadata Database**: The Metadata Database stores all the metadata used by Airflow, including DAG definitions, task statuses, and scheduling information. It uses a SQL database (e.g., PostgreSQL, MySQL) to maintain state and ensure consistency across components.

- **Web Server**: The Web Server hosts the Airflow user interface, providing a platform to monitor and manage workflows. It allows users to view DAGs, check the status of tasks, read logs, and manually trigger or pause workflows.

## Additional Points

- **DAGs (Directed Acyclic Graphs)**: Core concept for defining task dependencies.
- **Integrations**: Supports integration with various data sources and processing tools.
- **Monitoring**: Offers real-time monitoring and alerting capabilities.
- **Community Support**: Backed by a large and active community.

## DAGs (Directed Acyclic Graphs)

### Why DAGs

In Airflow, workflows are represented as DAGs (Directed Acyclic Graphs). A DAG is a collection of tasks with explicit relationships and dependencies. DAGs ensure that tasks are executed in a specific order without cycles, which is essential for maintaining data integrity and workflow correctness.

### Benefits

- **Clear Task Dependencies**: DAGs allow for explicit definition of task execution order.
- **Modularity**: Workflows can be broken down into reusable tasks.
- **Scalability**: Easy to add or modify tasks within the DAG.
- **Fault Tolerance**: Failures can be isolated to specific tasks without affecting the entire workflow.

### Drawbacks

- **Complexity Management**: Large DAGs can become difficult to manage and visualize.
- **Resource Consumption**: Complex DAGs may consume more system resources.
- **Learning Curve**: Requires understanding of DAG concepts and Airflow's programming model.

### Basic Terminologies of DAG
- **queued**: Task is in the queue waiting to be executed.
- **running**: Task is currently being executed.
- **success**: Task has completed successfully.
- **failed**: Task has failed.
- **up_for_retry**: Task has failed and is scheduled to retry.
- **up_for_reschedule**: Task is waiting to be rescheduled.
- **upstream_failed**: Task's upstream dependencies have failed.

### Operators
All operators inherit from the BaseOperator, which includes all of the required arguments for running work in Airflow. From here, each operator includes unique arguments for the type of work it’s completing. Some of the most popular operators are the PythonOperator, the BashOperator, and the KubernetesPodOperator.

- **BashOperator**: Executes a bash command.
- **PythonOperator**: Calls an arbitrary Python function.
- **EmailOperator**: Sends an email.

Use the `@task` decorator to execute an arbitrary Python function. It doesn’t support rendering `jinja` templates passed as arguments.

## Installation
To install Apache Airflow using Docker Compose, follow these steps:

1. Download the Docker Compose file:
```sh
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.10.3/docker-compose.yaml'
```

2. Initialize the Airflow database:
```sh
sudo AIRFLOW_UID=50000 docker compose up airflow-init
```

3. Start the Airflow services:
```sh
sudo AIRFLOW_UID=50000 docker compose --profile flower up -d
```