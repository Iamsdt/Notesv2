
Prompt: 

Don't share any code, let's only brainstorm, I will play devil's advocate
We are building a hiring app where we have a JD as Job Description, we are collecting info like primary skills, secondary skills, min and max work experience (like float value), then designation as text

Now we are collecting a lot of candidate, so we need to build a ranking algo
its need to be scale able
Let me give some example
1. Say we are looking for `Data Scientist` and min and max 0-2, which junior position, no if any candidate has 10 years of experience then its not fit for this position, and also Jay another candidate has PHD in data science he is not fit for it
2. Now we are looking for a senior role then PHD will be good fit for data science
3. Say we are looking for a Tech Lead, but One Candidate is CTO, he might not switch the job


Our main Database is Postgresql and For this we can use graph db? Prefer memgraph

What is your thoughts, how can make this ranking sophisticated not just direct skills matching

