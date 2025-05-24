```
sudo docker exec -e PGPASSWORD=123456 database   pg_dump -U postgres -d training10x   --no-owner --no-privileges   --exclude-table='*.aerich' --exclude-extension=vector -F p -f /tmp/data_only2.sql
```


```
gcloud sql import sql training10x gs://hire10x-prod/data_only2.sql --database=training10x
```