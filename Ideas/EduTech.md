
# Interview Preparation
Table:
Problem Table
```
id, title, description, week, tags, difficulty, concepts_description, concepts_video_link, test_case
```




/api/problem-service/
```
Api: /v1/stats
Response:
2. Stats, solved
```


```
Api:GET /v1/problems
Response:
1. All the Problems (id, title, diffucilty, week, tags)
```

```
API:GET /v1/problems/id
1. Description
2. Concepts
3. Solution
4. Submission
5. Notes
6. TestCase
```

```
Update Notes
API:PUT /v1/problems/id
Notes
```

```
API: GET /v1/notes
GET ALL Notes
```

### Submission:
```
POST: v1/problems/id/submissions
Code
```

```
POST: v1/problems/id/runs
Code
```

``` 
this is to generate AI suggestion
POST: v1/problems/id/submissions/id
Code
```
