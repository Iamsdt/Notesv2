https://github.com/QingdaoU/OnlineJudgeDeploy

Steps:
1. Docker pull
2. Update the domain
```
SERVICE_URL=https://code.10xscle.ai  
BACKEND_URL=https://code.10xscale.ai/api/judge_server_heartbeat/
```

3. Force HTTPs


Now generate using lets encrypt
```

```

Now update ssl
```
sudo cp /etc/letsencrypt/live/code.10xscale.ai/fullchain.pem ~/OnlineJudgeDeploy/data/backend/ssl/server.crt

sudo cp /etc/letsencrypt/live/code.10xscale.ai/privkey.pem ~/OnlineJudgeDeploy/data/backend/ssl/server.key  

sudo chown $(whoami):$(whoami) ~/OnlineJudgeDeploy/data/backend/ssl/server.crt  
sudo chown $(whoami):$(whoami) ~/OnlineJudgeDeploy/data/backend/ssl/server.key  

sudo chmod 644 ~/OnlineJudgeDeploy/data/backend/ssl/server.crt  
sudo chmod 600 ~/OnlineJudgeDeploy/data/backend/ssl/server.key
```