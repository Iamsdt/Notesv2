
Not focusing on Update: 

GET request or Create JD or Create Template



# CREATE JD: 
### Duplicate the “business development” JD and customize it for “Mumbai office”
- Confirm the  ‘business development”  JD first and fetch the corresponding details #SQL 
- customize it for “Mumbai office” <modify the params to “Mumbai Office”> #llm 
- Save the JD #ui 

## Can you add job benefits for “java developer” JD?Enhance the raw content of JD
- Confirm the Java Dev JD first and fetch the corresponding details #SQL 
- Add job benefits for “java developer” JD and save it #ui #llm 
  
## Update the JD for 'Java Developer' to include a requirement for experience with Spring Boot.

- Confirm the Java Dev JD first and fetch the corresponding details #SQL 
- Based on LLM intelligence: include a requirement for experience with Spring Boot, 
- Parse the results again using llm and show the JD screen, with a confirm option to save/update, based on the JD ID. #ui 

## JD Uploaded > Data parsed> Prompt to AI assistant: Review and suggest improvements for this JD
- Fetch the JD X #SQL    
- Based on LLM intelligence review and suggested improvements

## Update the “product manager” JD to include experience with Agile Methodologies

- Confirm the “product manager” JD and fetch the corresponding details #SQL 
    
- Based on LLM intelligence: include experience with Agile Methodologies 
    
- Parse the results again and show the JD screen, with a confirm option to save/update #ui
  
## What keywords should we include in the 'Data Scientist' JD to optimize it for SEO?

- Based on LLM intelligence: What keywords should we include in the 'Data Scientist' JD to optimize it for SEO? #llm 


## Create a JD for a 'Senior Cloud Engineer' that highlights the company's benefits and remote work policies.

- Based on LLM intelligence: show a JD for a 'Senior Cloud Engineer' that highlights the company's benefits and remote work policies. #llm 
    
- Show a create JD screen with the ability to parse and save  #ui 

## Generate multiple versions of a 'Marketing Specialist' JD targeting different experience levels: junior, mid-level, and senior.

- It should show 3 different templates of  'Marketing Specialist' JD targeting different experience levels: junior, mid-level, and senior. #llm 

- Clicking on each of these show create JD with appropriate JD and corresponding JD screen #ui 

## Translate the ‘Java Developer' JD into Spanish for our international job board postings. 

- Confirm the Java Dev JD first and fetch the corresponding details #SQL 
- Based on LLM intelligence: Translate the ‘Java Developer' JD into Spanish

  
## Create a JD template for technical roles that can be easily customized by hiring managers.

- Based on LLM intelligence: Create a JD template for technical roles that can be easily customized by hiring managers. #llm 

## Can you add a diversity and inclusion statement to all existing JDs?

- Can update only 1 jd at a time.. Choose which JD you want to update #SQL #llm 
- Show relevant JD screen #ui 
- Based on LLM intelligence: show with diversity and inclusion statement added, with option to save/ update

  
## Example Statement: 
Asana is committed to providing a workplace free from discrimination or harassment. We expect every member of the Asana community to do their part to cultivate and maintain an environment where everyone has the opportunity to feel included, and is afforded the respect and dignity they deserve.

- Decisions related to hiring, compensating, training, evaluating performance, or terminating are made fairly, and we provide equal employment opportunities to all qualified candidates and employees. We examine our unconscious biases and take responsibility for always striving to create an inclusive environment that makes every employee and candidate feel welcome.”
### Can you create Java Dev JD, with 5 yrs of experience @ hyderabad, for hire10x.ai firm
	- Extracted Attributes
	- Assigned to
	- JD Name
	- Recommendations
	- Targets 
	
It should ask/ confirm these attributes and then provide a way to add/modify these attributes and then call the save JD action 

### What is the status of the "Java Developer" JD ?
- Using SQLAgent/ API fetch raw JD related data.
- Based on LLM intelligence: Format/Condense this raw data .. JD was created by userX and assigned to UserY on so-and-so date. Further, 100 candidates were sourced from linkedin and 200 from internal database… 30 candidates of these were contacted via Email and 20 via WA and 20 via Linkedin 
- 20 people have shown interest. 

- Recommendation 1, Recommendation 2, Recommendation 3

#### Recommendation 1
- Contact 20 new candidates from this JD
- <show the table with 20 candidates>
- Fetch their contact details …… EXECUTE 
- Here are the contact details 
- show the table with contact details

- Communicate with them via Email, Linkedin ….. EXECUTE
- Here are the results of Communication
- show the table with the output of communication action

#### Recommendation2

- - Contact 20 new candidates from internal database
- <show the table with 20 candidates>
- Fetch their contact details …… EXECUTE 
- Here are the contact details 
- show the table with contact details
- Communicate with them via Email, Linkedin ….. EXECUTE
- Here are the results of Communication
- show the table with the output of communication action
    
#### Recommendation 3
- - Send follow-up messages to already contacted people 
- show the table with candidates contacted
- Communicate with them via Email, Linkedin ….. EXECUTE
- - Here are the results of Communication
- show the table with the output of communication action
#### Recommendation 4
- You’ve added candidates with the following keywords… add candidates with new keywords ABC... EXECUTE…
- Who has created JD specific things to creation, who is working on this JD,
- When was this JD created, What are the important attributes skill, designation for this JD… etc 
-        - Fetch JD related data #SQL 
-        - Based RAG / memory answer the question #llm 


#### Which candidates are highly relevant to "Business Developer" JD? and communicate with these candidates via Email/Linkedin
- From API: Find candidates relevant to the Business Development JD
- - Just like recommendations screen, show the option to: Communicate with these candidates via Email show all relevant templates
- - Just like recommendations screen, show the option to: Communicate with these candidates via Linkedin show all relevant templates
- Open "CXO" JD
- - redirect to CXO JD 
- How many candidates were contacted, shortlisted for "Finance Analyst" JD
- - Using SQL Agent, fetch all the relevant data for "Finance Analyst" JD and from RAG/memory answer all the necessary questions

### Candidate OUTREACH Analysis/ Task:
- Generate a report on the response rate from candidates contacted via LinkedIn for the 'Marketing Specialist' JD. 
- Using the SQL Agent, fetch 
- Provide a detailed report of candidates sourced from LinkedIn for the 'Data Engineer' JD.
- Send personalized connect requests with a note on Linkedin and personalized email inviting them to apply for the job.
- Analyze the response rates to our 'Customer Service Representative' JD and suggest optimizations. <MBA answer can be given, but not technical answer. This technical answer human has to give the thought and AI can automate/execute this task>
- Send follow-up emails to all candidates shortlisted for the 'Finance Analyst' JD.
- Can you automate follow-up messages to candidates who haven't responded to our initial outreach?
- Generate insights on the most effective sourcing channels for technical roles.
- Analyze the dropout rates of candidates in the later stages of the hiring process for the 'Operations Manager' role.

  
  

JD Analysis:

- Provide a summary of the JD requirements for the “HR Manager” position.
    
- What are the legal requirements to include in a JD for a position based in the EU?
    
- What is our average time to hire for the 'Sales Executive' position, and how can we reduce it?  
      
    

  
  

CV related questions

- Ask me work Experience, Education, Contact details etc of candidate X
    
- Communicate with candidate X
    
- Candidate X is relevant for what JDs?
    
- Upload a Resume, and tell me which JDs this candidate is relevant for?
    

- Upload a resume 
    
- FInd the suitable JD for this
    

- Can you show me the top 10 candidates in “Job role” having “x years of work experience” with “y” skills in “z” location who have worked in a “Series b” funded company 
    
- Show me the top 10 candidates for the “Java Developer/ All” JD based on your ranking
    
- Identify the relevant candidates from prospective leads  CVs for the 'Operations Manager' List and add the top 10 to JD X
    
- Rank candidates for the 'Business Analyst' role based on their experience and skills.
    
- Compare the qualifications of these two candidates “Candidate A” and “Candidate B” for the 'Sales Director' role.
    
- What are the common red flags to watch for in CVs for the 'HR Generalist' position? <INTERNET>
    
- Can you summarize the professional experience of candidate X?
    
- Generate a list of candidates from our internal database for the 'Marketing Coordinator' role.
    
- Analyze candidate feedback on the application process and provide suggestions for improvement. <Capture user feedback comments>
    
- Identify patterns in unsuccessful applications for the 'Project Manager' role to refine our screening criteria. <HUman intervention>
    
- Evaluate the performance of candidates sourced from different platforms for the 'Business Analyst' role.
    

  

Schedule related questions

- What is my schedule for today
    
- What was I working on X days ago
    
- JD X is no longer high priority, readjust and share my updated schedule
    
- Upcoming schedule for next week?
    
- Set up interviews with these three candidates for the 'Software Engineer' role.
    

- Reschedule the interview with Jane Doe for Thursday at 11 AM.
    
- Send reminders to candidates and interviewers for tomorrow's interviews.
    

- Provide a summary of my scheduled tasks for the next week.
    
- Arrange back-to-back interviews for the 'Graphic Designer' role candidates.
    

- What was I working on five days ago?
    

- Update my schedule to prioritize the 'Project Manager' JD activities.
    

  

- Generate an interview schedule for the 'Product Manager' candidates. <HUman intervention>
    

  

- Can you suggest optimal interview times based on the availability of all participants?
    
- Set up automated reminders for upcoming interviews, including pre-interview tips for candidates.
    
- Automatically reschedule interviews in case of conflicts and notify all parties involved.
    
- Generate a report of no show candidates for a particular JD or all JDs
    
- Share candidate feedback from the 'Marketing Specialist' interviews with the team.
    
-   
    

  
  

Team related questions

- What is user "X" working on?
    
- Which of my team member is having a big workload
    

UPDATE: <not handling updates> Assign the task of sourcing candidates for the 'HR Manager' JD to user Y.

  

- Generate a report on the recruitment performance of team member Z.
    
- Which team member has the highest workload right now?
    

- Set up a team meeting to discuss the recruitment strategy for next quarter. <Human Intervention>
    

  

- What tasks have been assigned to user A in the past week?
    

  

- Generate reports for the progress of all recruitment tasks for the 'Sales Executive' JD done by X Team members.
    

  

- Send a notification to the team about the new 'Finance Manager' job opening.
    
- Provide an overview of the team's activities for this month.
    

  
  
  
  
  

-------------------------------------------------------------------------------------------------------------------------------

-------------------------------------------------------------------------------------------------------------------------------

JD Related Questions, Prompts, and Actions:

1. Not focusing on Update: GET request or Create JD or Create Template
    
2. Create JD:
    

- Duplicate the “business development” JD and customize it for “Mumbai office”
    
- Duplicate the ‘business development” JD
    

4. Can you add job benefits for “java developer” JD? <Enhance the raw content of JD>
    
5. Update the JD for 'Java Developer' to include a requirement for experience with Spring Boot.
    
6. Update the “product manager” JD to include experience with Agile Methodologies.
    
7. What keywords should we include in the 'Data Scientist' JD to optimize it for SEO?
    
8. Create a JD for a 'Senior Cloud Engineer' that highlights the company's benefits and remote work policies.
    
9. Generate multiple versions of a 'Marketing Specialist' JD targeting different experience levels: junior, mid-level, and senior.
    
10. Translate the 'Software Developer' JD into Spanish for our international job board postings.
    
11. Create a JD template for technical roles that can be easily customized by hiring managers.
    
12. Can you add a diversity and inclusion statement to all existing JDs?
    
13. Example Statement: Asana is committed to providing a workplace free from discrimination or harassment. We expect every member of the Asana community to do their part to cultivate and maintain an environment where everyone has the opportunity to feel included, and is afforded the respect and dignity they deserve. Decisions related to hiring, compensating, training, evaluating performance, or terminating are made fairly, and we provide equal employment opportunities to all qualified candidates and employees. We examine our unconscious biases and take responsibility for always striving to create an inclusive environment that makes every employee and candidate feel welcome.
    
14. Create Java Dev JD, with 5 yrs of experience @ Hyderabad, for hire10x.ai firm.
    
15. Extracted Attributes Assigned to JD Name Recommendations Targets
    
16. What is the status of the "Java Developer" JD?
    
17. Who has created JD <specific things to creation>, who is working on this JD, when was this JD created, what are the important attributes <skill, designation> for this JD?
    
18. Which candidates are highly relevant to "Business Developer" JD? and communicate with these candidates via Email/Linkedin.
    
19. Open "CXO" JD.
    
20. How many candidates were contacted, shortlisted for "Finance Analyst" JD?
    
21. JD Analysis: Provide a summary of the JD requirements for the “HR Manager” position.
    
22. What are the legal requirements to include in a JD for a position based in the EU?
    
23. What is our average time to hire for the 'Sales Executive' position, and how can we reduce it?
    
24. Fetch JD’s with keywords and not JD name (if user forgot JD name, enter keywords and fetch the JD’s related to the keywords sorted by date)
    
25. JD redundancy - Fetch JD’s with same content and display the JD’s to delete from the system. If candidates are added, ask the user to migrate the candidates to the main JD
    
26. Fetch JD’s which were untouched for a long time (More than 3 months or so)
    
27. Give a list of other keywords while JD creation (Example: if a user is creating JD for testing, include suggest to include keywords such as HP-ALM, Selenium, Web testing, Device Testing, Perfecto, Manual Testing, Automation testing, etc) to include in the JD 
    

Candidate Related Questions (Questions, Prompts, and Actions):

1. Candidate OUTREACH Analysis/ Task:
    

- Generate a report on the response rate from candidates contacted via LinkedIn for the 'Marketing Specialist' JD.
    
- Provide a detailed report of candidates sourced from LinkedIn for the 'Data Engineer' JD.
    
- Send personalized connect requests with a note on Linkedin and personalized email inviting them to apply for the job.
    
- Analyze the response rates to our 'Customer Service Representative' JD and suggest optimizations. <MBA answer can be given, but not technical answer. This technical answer human has to give the thought and AI can automate/execute this task>
    
- Send follow-up emails to all candidates shortlisted for the 'Finance Analyst' JD.
    
- Can you automate follow-up messages to candidates who haven't responded to our initial outreach?
    
- Generate insights on the most effective sourcing channels for technical roles.
    
- Analyze the dropout rates of candidates in the later stages of the hiring process for the 'Operations Manager' role.
    

3. Ask me work Experience, Education, Contact details, etc., of candidate X.
    
4. Communicate with candidate X.
    
5. Candidate X is relevant for what JDs?
    
6. Upload a Resume, and tell me which JDs this candidate is relevant for?
    
7. Upload a resume. Find the suitable JD for this.
    
8. Can you show me the top 10 candidates in “Job role” having “x years of work experience” with “y” skills in “z” location who have worked in a “Series b” funded company?
    
9. Show me the top 10 candidates for the “Java Developer/ All” JD based on your ranking.
    
10. Identify the relevant candidates from prospective leads CVs for the 'Operations Manager' List and add the top 10 to JD X.
    
11. Rank candidates for the 'Business Analyst' role based on their experience and skills.
    
12. Compare the qualifications of these two candidates “Candidate A” and “Candidate B” for the 'Sales Director' role.
    
13. What are the common red flags to watch for in CVs for the 'HR Generalist' position? <INTERNET>
    
14. Can you summarize the professional experience of candidate X?
    
15. Generate a list of candidates from our internal database for the 'Marketing Coordinator' role.
    
16. Analyze candidate feedback on the application process and provide suggestions for improvement. <Capture user feedback comments>
    
17. Identify patterns in unsuccessful applications for the 'Project Manager' role to refine our screening criteria. <Human intervention>
    
18. Evaluate the performance of candidates sourced from different platforms for the 'Business Analyst' role.
    

CV/Resume Related Questions, Prompts, and Actions:

1. Provide a summary of the JD requirements for the “HR Manager” position.
    
2. What are the legal requirements to include in a JD for a position based in the EU?
    
3. What is our average time to hire for the 'Sales Executive' position, and how can we reduce it?
    

Interview Scheduling related Questions, Prompts, and Actions:

1. Generate an interview schedule for the 'Product Manager' candidates. <Human intervention>
    
2. Can you suggest optimal interview times based on the availability of all participants?
    
3. Set up automated reminders for upcoming interviews, including pre-interview tips for candidates.
    
4. Automatically reschedule interviews in case of conflicts and notify all parties involved.
    
5. Generate a report of no-show candidates for a particular JD or all JDs.
    
6. Share candidate feedback from the 'Marketing Specialist' interviews with the team.
    

Team Related Questions, Prompts, and Actions:

1. What is user "X" working on?
    
2. Which of my team member is having a big workload.
    
3. UPDATE: <not handling updates> Assign the task of sourcing candidates for the 'HR Manager' JD to user Y.
    
4. Generate a report on the recruitment performance of team member Z.
    
5. Which team member has the highest workload right now?
    
6. Set up a team meeting to discuss the recruitment strategy for the next quarter. <Human Intervention>
    
7. What tasks have been assigned to user A in the past week?
    
8. Generate reports for the progress of all recruitment tasks for the 'Sales Executive' JD done by X Team members.
    
9. Send a notification to the team about the new 'Finance Manager' job opening.
    
10. Provide an overview of the team's activities for this month.