# User Service

Get single user
Get: user-service/v1/users/{id}
Output: current /me api

Get: user-service/v2/users/{id}
Output: current /me api

Search User
user-service/v1/users?q='user1'
Output: user_id, name, role, designations


# JD Service
Post: jd-service/v1/jds
Input: check figma Create jd page (extracted attributes, assign, Recommendation and Targets)
Output:
```
jd_id, and all the fields shared
```

Patch: jd_service/v1/jds/{jd_id}
input:
```
job_type: application_form
data: json value (check if json is valid and not empty)

job_type: save_jd

job_type: career_page
data: json value (check if json is valid and not empty)
```

Output: Success message
Note: for save_jd change jd status as saved

GET: jd-service/v1/jds/{id}
Return all the JD details


GET: jd-service/v1/jds/{id}:applyForm
This is for application form
output: check figma application form dialog, share jd details with application form, don't add any extra details

GET: jd-service/v1/jds/{id}:applyCareer
This is for application form
output: check figma application form dialog, share jd details with application form, don't add any extra details

Save JD share in linkedin
POST: jd-service/v1/jds/{id}/socials
input: 
```
type: group, post
-- other data talk with frontend team
```

Manage JD:
Get: jd-service/v1/jds
query: check figma

# Communication Service
Get All Linkedin Groups
Get: communication-service/v1/linkedins/

Save Linkedin Groups
POST: communication-service/v1/linkedins


# Candidate Service

Save Candidate From Different Sources
Post: candidate-service/v1/candidates/
