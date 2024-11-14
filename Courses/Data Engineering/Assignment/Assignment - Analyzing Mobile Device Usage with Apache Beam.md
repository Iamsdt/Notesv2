---
Created by: Shudipto Trafder
Created time: 2024-11-13T00:00:00
Last edited time: 2024-11-13T00:00:00
tags:
  - pyspark
  - de
---


### Objective
In this assignment, you will use the Apache Beam framework to analyze a dataset of mobile device usage and user behavior. You will build on the provided pipeline code to implement additional transformations and write the results to output files.

### Dataset
The dataset you will be working with is the ["Mobile Device Usage and User Behavior Dataset"](https://github.com/Training10x/DataEngineering/blob/main/Data/user_behavior_dataset.csv). It contains information about user IDs, device models, operating systems, app usage time, screen-on time, battery drain, number of apps installed, data usage, age, gender, and user behavior class.

### Instructions

1. **Familiarize yourself with the provided pipeline code**: Review the code and understand the purpose of each transformation step.

2. **Implement the following additional transformations**:
   - **1. Top 5 Device Models**: Find the top 5 most common device models in the dataset and write the results to a file named `top_device_models.txt`.
   - **2. Oldest and Youngest Users**: Determine the age of the oldest and youngest users in the dataset and write the results to a file named `user_age_range.txt`.
   - **3. Data Usage by User Behavior Class**: Compute the average daily data usage for each user behavior class and write the results to a file named `data_usage_by_class.txt`.
   - **4. Gender Distribution**: Calculate the percentage of male and female users in the dataset and write the results to a file named `gender_distribution.txt`.
   - **5. Power User Analysis**: Identify the top 10 users with the highest daily app usage time and write their user IDs to a file named `power_users.txt`.
   - **6. Battery Drain by Device Model**: Compute the average daily battery drain for each device model and write the results to a file named `battery_drain_by_model.txt`.

3. **Document your code**:
   - Add docstrings to explain the purpose and behavior of each new function or transform you create.
   - Provide clear comments throughout your code to help others understand the logic.

#### Submission
1. Submit text files for each of the aggregations and insights derived from the dataset.
2. Provide your code in a `.py` file or Jupyter notebook with detailed comments explaining each step.