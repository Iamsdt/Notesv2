---
Created by: Shudipto Trafder
Created time: 2024-01-01T23:08
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T23:16
tags:
  - pgsql
---
1. First export from current Database to SQL

```JavaScript
docker exec -i database /usr/bin/pg_dump -U postgres hire10xdb4 -s > raw2.sql
```

Now install [https://dbdocs.io/docs](https://dbdocs.io/docs)

```JavaScript
npm install -g dbdocs
```

Now install DB docs

```JavaScript
dbdocs
```

### Convert SQL to DBML

install DBML CLI

```JavaScript
npm install -g @dbml/cli
```

Now convert into DBML

```JavaScript
sql2dbml raw2.sql --postgres -o hire10xdb.dbml
```

  

## Build:

1. First login if not logged yet

```JavaScript
dbdocs login
```

1. now build

```JavaScript
dbdocs build hire10xdb.dbml
```

1. Protect with password

```JavaScript
dbdocs password --set u5E40mz0TSyPy1w --project hire10xdb
```

  

### Remove

remove your project if not required

```JavaScript
dbdocs remove hire10xdb
```