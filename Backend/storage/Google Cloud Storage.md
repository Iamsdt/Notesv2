---
tags:
  - cloud
  - storage
  - gcp
  - gcloud
Date: 2024-05-07T23:52:00
---
## Upload Single File
```bash
gsutil cp ./apc.pdf gs://10xscale1testing/collection_cvs
```

# upload multiple file
```bash
gsutil -m cp -r . gs://10xscale1testing/collection_cvs
```
`ris:Google`