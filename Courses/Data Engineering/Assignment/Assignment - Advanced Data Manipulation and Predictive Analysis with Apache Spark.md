---
Created by: Shudipto Trafder
Created time: {{date:YYYY-MM-DD}}T{{time:HH:mm}}
Last edited time: {{date:YYYY-MM-DD}}T{{time:HH:mm}}
tags: 
	- assignement
	- pyspark
	- de
---


**Objective**: This assignment will test your ability to conduct exploratory data analysis (EDA), clean data, and transform it into a format suitable for predictive analysis and aggregation tasks. [MBA](https://github.com/Training10x/DataEngineering/blob/main/Data/MBA.csv) Datasets.
#### Dataset Fields
The dataset includes the following fields:
- **application_id**: Unique identifier for each application
- **gender**: Applicant's gender (Male, Female)
- **international**: International student status (TRUE/FALSE)
- **gpa**: Grade Point Average on a 4.0 scale
- **major**: Undergraduate major (Business, STEM, Humanities)
- **race**: Racial background (e.g., White, Black, Asian, Hispanic, Other, or null for international students)
- **gmat**: GMAT score (out of 800)
- **work_exp**: Years of work experience
- **work_industry**: Industry of previous work experience (Consulting, Finance, Technology, etc.)
- **admission**: Admission status (Admit, Waitlist, or Null for Deny)

#### Assignment Tasks
1. **Data Loading and Inspection**:
   - Load the dataset into a Spark DataFrame.
   - Display a summary of the dataset to inspect field names, data types, and the first few rows.

2. **Data Cleaning and Transformation**:
   - **Rename Columns**: Rename `work_exp` to `experience_years` and `gmat` to `gmat_score`.
   - **Handle Null Values**:
     - For `gpa`, `gmat_score`, and `work_exp` columns, replace nulls with the median of each column.
     - Fill missing values in the `admission` column with `Deny`.
     - Assume null values in `race` are `International`.
   - **Add Conditional Columns**:
     - Create a column `admission_numeric` with values: 1 for Admit, 0 for Waitlist, and -1 for Deny.
     - Create a column `experience_level` based on `experience_years`:
       - `Entry-level` if experience is 0–2 years
       - `Mid-level` if experience is 3–6 years
       - `Senior` if experience is more than 6 years

3. **Exploratory Data Analysis**:
   - Calculate the average GMAT score and GPA for each `major`.
   - Find the percentage of applicants admitted by `work_industry`.
   - Determine the distribution of `experience_level` among applicants by `gender`.
   - Show the average GPA and GMAT scores by `race` and `international` status.

4. **Aggregation and Insights**:
   - Calculate the admission rate for international vs. domestic applicants.
   - Find the top 3 undergraduate majors with the highest admission rates.
   - Show the average work experience and GPA for admitted vs. denied applicants.
   - Calculate the overall average GPA and GMAT score by `admission` status.

5. **Prediction Dataset Preparation**:
   - Create a final dataset with the following features to predict `admission_numeric`: 
     - `gpa`, `gmat_score`, `experience_years`, `major`, `gender`, and `work_industry`.
   - Save the final dataset as a CSV file for future predictive modeling.

6. **Save the Results**:
   - Save the cleaned DataFrame as a CSV file.
   - Save each of the key aggregations (admission rates, averages, distributions) as separate CSV files.

#### Submission
1. Submit the cleaned DataFrame in CSV format.
2. Submit CSV files for each of the aggregations and insights derived from the dataset.
3. Provide your code in a `.py` file or Jupyter notebook with detailed comments explaining each step.