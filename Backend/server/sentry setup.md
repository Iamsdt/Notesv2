---
Created by: Shudipto Trafder
Created time: 2023-10-25T14:04
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:20
tags:
  - cloud
  - sentry
---
git clone self-hosted repo

```Shell
git clone https://github.com/getsentry/self-hosted.git
```

  

Run the below command to generate all the config files

```Shell
sudo ./install.sh
```

  

update these files

1. config.yml
    1. update mail
    2. slack
    3. GitHub
2. sentry.conf.py
    
    1. uncomment these lines if using nginx
    
    ```Python
    SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
    USE_X_FORWARDED_HOST = True
    SESSION_COOKIE_SECURE = True
    CSRF_COOKIE_SECURE = True
    SOCIAL_AUTH_REDIRECT_IS_HTTPS = True
    ```
    
    b. add this line
    
    ```Python
    SENTRY_OPTIONS['system.url-prefix'] = "https://sentry.hire10x.ai"
    ```
    
      
    

Docker

run docker-compose, it will expose, 9000

  

use nginx, to deploy sentry

```Shell
server {
        listen 80;
        listen [::]:80;
        server_name sentry.hire10x.ai;
        return 301 https://$server_name$request_uri;
}


server {
    server_name sentry.hire10x.ai;
		location / {
        \#include proxy_params;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-Host $host;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_pass http://localhost:9000;
    }



    listen 443 ssl;
    ssl_certificate /etc/letsencrypt/live/sentry.hire10x.ai/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/sentry.hire10x.ai/privkey.pem;
    # include /etc/letsencrypt/options-ssl-nginx.conf;
    # ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
    ssl_session_timeout 1440m;
    ssl_session_tickets off;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers off;
        # ssl_ciphers "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA2>
        # keepalive_timeout 5;
}
```

### Generate SSL

```Shell
docker run -it --rm -p 80:80 --name certbot \
         -v "/etc/letsencrypt:/etc/letsencrypt" \
         -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
         certbot/certbot certonly --standalone -d code.10xscale.ai

# renew ssl
docker run -it --rm --name certbot \
	-v "/etc/letsencrypt:/etc/letsencrypt" \
  -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
  -v "/var/www/html:/var/www/html" \
  certbot/certbot renew --webroot -w /var/www/html --dry-run
```

  

TO create user

```Shell
docker-compose run --rm web createuser
```

  

Add extensions:

Github: [https://develop.sentry.dev/integrations/github/](https://develop.sentry.dev/integrations/github/)

slack: [https://develop.sentry.dev/integrations/slack/](https://develop.sentry.dev/integrations/slack/)