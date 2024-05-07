---
Created by: Shudipto Trafder
Created time: 2023-10-18T21:56
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:15
tags:
  - Docker
---
```Python
recruit
deployments
-- dev
-- local
-- 
stats
```

put the docker file inside the service

```Shell
x-docker-loc: &docker-loc
context: ../../recruit/docker
dockerfile: Dockerfile
```