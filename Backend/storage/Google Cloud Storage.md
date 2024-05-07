---
tags:
  - cloud
  - storage
  - gcp
  - gcloud
Created by: Shudipto Trafder
Created time: 2024-05-07T01:22:00
Last edited by: Shudipto Trafder
Last edited time: 2024-05-08T01:22:00
---
### Fix Cors

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


## Upload Single File
```bash
gsutil cp ./apc.pdf gs://10xscale1testing/collection_cvs
```

# upload multiple file
```bash
gsutil -m cp -r . gs://10xscale1testing/collection_cvs
```
