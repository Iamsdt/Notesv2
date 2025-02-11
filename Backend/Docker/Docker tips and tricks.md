---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:19
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:14
tags:
  - Docker
---
1. Add multiple env variables into docker

```Plain
-e LIVEKIT_RECORDER_CONFIG="$(cat config.yaml)"
```

1. Logs: check only last hour logs

```Plain
--since 1h
```