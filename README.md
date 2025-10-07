# INISTALASI WEB

## ⚡ Instal Aapanel

```bash
URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel
```

## ⚡ Set Waktu Jakarta

```bash
sudo timedatectl set-timezone Asia/Jakarta
```
## ⚡ Instal Tmux,Python,Gdown

```bash
sudo apt install tmux -y
sudo apt install python3 python3-pip -y
pip install gdown --break-system-packages
```

## ⚡ Download & Ekstrak Tool Live Premium
VIP
```bash
gdown https://drive.google.com/uc?id=1lhm7PP0fM6rxqkdscavw00mxvSKrpwty
unzip livesaldopremiumvip.zip
```

## ⚡ Jalankan Backend
VIP
```bash
cd livesaldopremiumvip
pm2 start index.js --name backend
```

## ⚡ Tambahkan Website Di Aapanel + SSL
domain frontend php
config ubah sesuai domain
```bash
server {
  listen 80;
  listen 443 ssl http2;
  server_name aku.hidupberkah.site;

  root /www/wwwroot/aku.hidupberkah.site;
  index index.php index.html index.htm default.php default.htm default.html;

  include /www/server/panel/vhost/nginx/extension/aku.hidupberkah.site/*.conf;
  include /www/server/panel/vhost/nginx/well-known/aku.hidupberkah.site.conf;

  # --- SSL (punyamu) ---
  ssl_certificate     /www/server/panel/vhost/cert/aku.hidupberkah.site/fullchain.pem;
  ssl_certificate_key /www/server/panel/vhost/cert/aku.hidupberkah.site/privkey.pem;
  ssl_protocols TLSv1.1 TLSv1.2 TLSv1.3;
  add_header Strict-Transport-Security "max-age=31536000";
  error_page 497 https://$host$request_uri;

  error_page 404 /404.html;
  error_page 502 /502.html;

  include enable-php-83.conf;
  include /www/server/panel/vhost/rewrite/aku.hidupberkah.site.conf;

  # ----> PRIORITAS KE NODE: SSE
  location ^~ /api/progress-sse/ {
    proxy_pass http://127.0.0.1:3535;
    proxy_http_version 1.1;
    proxy_set_header Connection '';
    proxy_buffering off;
    proxy_cache off;
    proxy_read_timeout 3600s;
    add_header X-Accel-Buffering no;
  }

  client_max_body_size 7g;
  client_body_timeout 3600;

  # ----> PRIORITAS KE NODE: API
  location ^~ /api/ {
    proxy_request_buffering off;
    proxy_buffering off;
    proxy_set_header Range $http_range;
    proxy_set_header If-Range $http_if_range;
    proxy_force_ranges on;
    proxy_connect_timeout 600;
    proxy_send_timeout 3600;
    send_timeout 3600;

    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_read_timeout 300s;

    proxy_pass http://127.0.0.1:3535/api/;   # <-- dengan trailing slash
  }

  # ----> PRIORITAS KE NODE: UPLOADS (thumbs & previews)
  location ^~ /uploads/ {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_read_timeout 300s;

    proxy_pass http://127.0.0.1:3535/uploads/;  # <-- dengan trailing slash
  }

  # ---- static umum (TETAPKAN DI BAWAH YANG ^~)
  location ~* \.(gif|jpg|jpeg|png|bmp|swf)$ {
    expires 30d;
    access_log off; error_log off;
  }
  location ~* \.(js|css)?$ {
    expires 12h;
    access_log off; error_log off;
  }

  # proteksi & lainnya (punyamu) ...
  location ~ ^/(\.user.ini|\.htaccess|\.git|\.env|\.svn|\.project|LICENSE|README.md) { return 404; }
  location ~ \.well-known { allow all; }

  access_log /www/wwwlogs/aku.hidupberkah.site.log;
  error_log  /www/wwwlogs/aku.hidupberkah.site.error.log;
}

```
## ⚡ Instal Fronten
VIP
```bash
gdown https://drive.google.com/uc?id=1ga9qfQjZa0I8RnsHGAhU98xDKGU_dj0L
unzip frontendlivesaldopremiumvip.zip
```





