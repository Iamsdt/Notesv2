---
tags:
  - storage
  - gdrive
Date: 2024-05-07T23:55:00
---


- Use [GDOWN](https://github.com/wkentaro/gdown)
    
    add pip package
    

```
pip install gdown
```

and execute below command

```
gdown https://drive.google.com/uc?id=1sp7P0oJaru1iufp1_ijETsTw04btMvwd
```

here, id change id

- make sure files shared as 'Anyone with the link'

## Python code
```
import gdown

url = 'https://drive.google.com/uc?id=0B9P1L--7Wd2vNm9zMTJWOGxobkU'
output = '20150428_collected_images.tgz'
gdown.download(url, output, quiet=False)

md5 = 'fa837a88f0c40c513d975104edf3da17'
gdown.cached_download(url, output, md5=md5, postprocess=gdown.extractall)
```