Lets create A Table in Biquery
This is bigquery schema

```
[
  {
    "name": "cid",
    "type": "INTEGER",
    "mode": "REQUIRED"
  },
  {
    "name": "name",
    "type": "STRING",
    "mode": "REQUIRED"
  },
  {
    "name": "date",
    "type": "TIMESTAMP",
    "mode": "REQUIRED"
  },
  {
    "name": "skills",
    "type": "STRING",
    "mode": "REPEATED"
  },
  {
    "name": "educations",
    "type": "RECORD",
    "mode": "REPEATED",
    "fields": [
      {
        "name": "degree",
        "type": "STRING",
        "mode": "REQUIRED"
      },
      {
        "name": "college",
        "type": "STRING",
        "mode": "REQUIRED"
      },
      {
        "name": "date",
        "type": "TIMESTAMP",
        "mode": "REQUIRED"
      }
    ]
  },
  {
    "name": "exp",
    "type": "RECORD",
    "mode": "REPEATED",
    "fields": [
      {
        "name": "company",
        "type": "STRING",
        "mode": "REQUIRED"
      },
      {
        "name": "designation",
        "type": "STRING",
        "mode": "REQUIRED"
      },
      {
        "name": "date",
        "type": "TIMESTAMP",
        "mode": "REQUIRED"
      }
    ]
  }
]
```


Now lets create script
```

```