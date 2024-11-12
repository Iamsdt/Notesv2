---
Created by: Shudipto Trafder
Created time: 2024-05-08T02:26
Last edited time: 2024-05-08T02:26
tags:
  - pgsql
  - sql
---



Clear All the Data
```bash
cat data25.sql | docker exec -i taiga-docker-taiga-db-1 psql -U taiga -d taiga -c "DROP SCHEMA public CASCADE; CREATE SCHEMA public;"
```

Now Restore
```bash
docker exec -i database /usr/bin/pg_dump -U postgres hire10xdb2 > data25.sql
```