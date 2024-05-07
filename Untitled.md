---
tags: 
Created by: Shudipto Trafder
Created time: 2024-05-08{time}}
Last edited by: Shudipto Trafder
Last edited time: 2024-05-0800:55
---
```dataview
LIST
FROM #ai 
```

```dataview
TABLE file.ctime as "Created Time", file.mtime as "Updated Time"
FROM #ai 
```



Today is `= date(today)` - `= [[exams]].deadline - date(today)` until exams!
