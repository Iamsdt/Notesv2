---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:10
Last edited by: Shudipto Trafder
Last edited time: 2023-10-18T20:13
tags:
  - adb
  - android
---
kill server and restart

```Plain
adb kill-server
sudo cp ~/Android/Sdk/platform-tools/adb /usr/bin/adb
sudo chmod +x /usr/bin/adb
adb start-server
```