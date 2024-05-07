---
tags:
  - db
  - pgsql
---

Clear All the Data
```bash
cat data25.sql | docker exec -i taiga-docker-taiga-db-1 psql -U taiga -d taiga -c "DROP SCHEMA public CASCADE; CREATE SCHEMA public;"
```

Now Restore
```bash
docker exec -i database /usr/bin/pg_dump -U postgres hire10xdb2 > data25.sql
```