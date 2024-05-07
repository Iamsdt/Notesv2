---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:16
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:20
tags:
  - cloud
---
Setup cors in gcloud ->

check existing cors ->

```Plain
gsutil cors get gs://10xscale2
```

setup up new cors config file

```Plain
gsutil cors set cors.json gs://10xscale2
```

File example:

```Plain
[
    {
      "origin": ["*"],
      "method": ["GET"],
      "responseHeader": ["Content Type"],
      "maxAgeSeconds": 3600
    }
]
```