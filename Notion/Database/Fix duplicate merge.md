---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:35
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:12
tags:
  - Graph
---
```Python
MERGE (a:Candidate {cid: {cid}})
ON CREATE SET a.exp = {exp},
              a.processing_id = {processing_id},
              a.start_date = {start_date}
ON MATCH SET a.exp = {exp},
             a.processing_id = {processing_id},
             a.start_date = {start_date}
RETURN a;
```