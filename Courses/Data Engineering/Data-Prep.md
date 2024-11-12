---
Created by: Shudipto Trafder
Created time: {{date:YYYY-MM-DD}}{{time:HH:mm}}
Last edited time: {{date:YYYY-MM-DD}}T{{time:HH:mm}}
tags: 
	- dataprep
	- gcp
	- de
---


Task: Create a column `admission_numeric` with values: 1 for Admit, 0 for Waitlist, and -1 for Deny.
Answer: Use condition Insert
Condition Type: Case on Single Column
Column to evaluate: admission
Case:
Comparison: admission = 'Admit'
New Value: 1
Comparison: admission = 'Waitlist'
New Value: 0
Default Value: -1
New Column Name: admission_numeric



Task:
Create a column `experience_level` based on `experience_years`:
       - `Entry-level` if experience is 0–2 years
       - `Mid-level` if experience is 3–6 years
       - `Senior` if experience is more than 6 years

Answer: Use Conditions Insert
Condition type: IF... Then ... else
IF: experience_years >= 6
Then: "Senior"
ELSE: IF(experience_years < 6 && experience_years >= 3, "Mid-level", "Entry-level")
New Column Name: experience_level


3. **Exploratory Data Analysis**:
   - Calculate the average GMAT score and GPA for each `major`.
   Answer: 
   Group by (major)
   Values: AVERAGE(gmat_score), AVERAGE(gpa)

   - Find the number of applicants admitted by `work_industry`.
Answer:
   Group by (work_industry)
   Values: count()

   - Determine the distribution of `experience_level` among applicants by `gender`.
   - Show the average GPA and GMAT scores by `race` and `international` status.