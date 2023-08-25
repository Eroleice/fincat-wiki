---
title: 在腾讯云部署Wiki.js
description: 如何在国内云服务器部署Wiki.js
published: true
date: 2023-08-25T13:09:14.622Z
tags: 
editor: markdown
dateCreated: 2023-06-04T10:48:57.574Z
---

# 环境
CPU - 4核 内存 - 8GB
系统盘 - SSD云硬盘 100GB
Ubuntu 22.04 LTS

实际上Wiki.js对资源的占用很低，我单纯是因为手头有这么一个就用了，活动时候买的，放着也是放着。

# 安装Node
> wiki.js仅可运行于Node v12/v14/v16 版本上！
{.is-warning}

## 更新apt
```
sudo apt update
sudo apt upgrade
```

## 安装curl
```
sudo apt install -y curl
```

## 运行Node v16的安装脚本
```
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt install -y nodejs
```

## 检查Node版本
```
node --version
```

# 配置PostgreSQL
## 安装PostgreSQL
```
sudo apt-get install postgresql postgresql-contrib -y
```

## 创建用户和数据库
切换至postgres用户：
```
sudo su - postgres
```
进入postgresSQL：
```
psql
```
创建新的用户`wikijs`并设置密码：
```
CREATE ROLE wikijs WITH LOGIN;
\password wikijs
```
此时根据提示设置密码，输入两次。
```
CREATE DATABASE wikidb;
```
设置权限：
```
GRANT ALL PRIVILEGES ON DATABASE wikidb TO wikijs;
```
退出postgresSQL：
```
\q
```
注销postgres用户：
```
exit
```

# 配置Wiki.js
## 新建用户wikijs用于权限控制
```
sudo adduser wikijs
sudo mkdir -p /var/www/wikijs
sudo chown wikijs:wikijs /var/www/wikijs
sudo su wikijs
```

## 下载Wiki.js
```
cd /var/www/wikijs && wget https://github.com/Requarks/wiki/releases/latest/download/wiki-js.tar.gz
tar xzf wiki-js.tar.gz
```

## 设置Wiki.js
```
cp config.sample.yml config.yml
nano config.yml
```

找到数据库的设置，可以找：
> PostgreSQL / MySQL / MariaDB / MS SQL Server only:
host: localhost
port: 5432
user: wikijs
pass: wikijsrocks
db: wiki

把以上内容中的`wikijsrocks`改为之前设置的数据库密码，把`db: wiki`改为`db: wikidb`。

考虑到之后要通过Nginx进行重定向，可以将`bindIP: 0.0.0.0`改为`bindIP: 127.0.0.1`

## 第一次启动Wiki.js
```
node server
```
之后还需要设置自动启动和Nginx重定向，因此先`Ctrl+C`关掉服务。

# 设置Wiki.js开机启动
```
sudo nano /etc/systemd/system/wikijs.service
```
输入以下内容：
```
[Unit]
Description=Wiki.js
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/node server
Restart=always

User=wikijs
Environment=NODE_ENV=production
WorkingDirectory=/var/www/wikijs

[Install]
WantedBy=multi-user.target
```
`Ctrl+X`退出并保存后设置启动项：
```
sudo systemctl daemon-reload
sudo systemctl enable wikijs.service
```

# 配置Nginx
## 安装Nginx
```
sudo apt install nginx -y
```

## 设置Nginx
> 考虑到安全性，这里默认设置https。
{.is-info}
### 配置http重定向至https
```
sudo rm /etc/nginx/sites-enabled/default
sudo nano /etc/nginx/sites-available/wikijs-http.conf
```
输入以下内容：
```
server {
  listen 80 default_server;
  listen [::]:80 default_server;

  server_name example.com;
  root /var/www/wikijs;

  location / {
      return 301 https://$server_name$request_uri;
  }
}
```
```
sudo ln -s /etc/nginx/sites-available/wikijs-http.conf /etc/nginx/sites-enabled/wikijs-http.conf
```
### 配置https
将下载的SSL证书，包括`.pem`和`.key`文件上传至服务器，例如`/etc/https/example.com/wiki.example.com.pem`和`/etc/https/example/wiki.example.com.key`。

```
sudo openssl dhparam -out /etc/nginx/dhparam.pem 2048
sudo nano /etc/nginx/sites-available/wikijs-https.conf
```
输入以下内容：
```
server {

  listen 443 ssl http2;
  listen [::]:443 ssl http2;

  ssl_certificate /etc/https/example.com/wiki.example.com.pem;
  ssl_certificate_key /etc/https/example.com/wiki.example.com.key;

  ssl_session_timeout 1d;
  ssl_session_cache shared:MozSSL:10m;  # about 40000 sessions

  # DH parameters file
  ssl_dhparam /etc/nginx/dhparam.pem;

  # intermediate configuration
  ssl_protocols TLSv1.2;
  ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
  ssl_prefer_server_ciphers off;

  # HSTS (ngx_http_headers_module is required) (63072000 seconds)
  # Uncomment the following line only if your website fully supports HTTPS
  # and you have no intention of going back to HTTP, otherwise, it will
  # break your site.

  # add_header Strict-Transport-Security "max-age=63072000" always;

  # OCSP stapling

  ssl_stapling on;
  ssl_stapling_verify on;
  
  # verify chain of trust of OCSP response using Root CA and Intermediate certs
  ssl_trusted_certificate /etc/https/example.com/wiki.example.com.pem;

  # Use Cloudflare DNS resolver
  resolver 1.1.1.1;

  server_name  wiki.example.com;
  root   /var/www/wikijs;

  # Pass requests to the Wiki.js service listening on 127.0.0.1:3000
  location / {
    proxy_pass          http://127.0.0.1:3000;
    proxy_http_version  1.1;
    proxy_set_header    Upgrade $http_upgrade;
    proxy_set_header    Connection "upgrade";
    proxy_set_header    Host $host;
    proxy_set_header    X-Real-IP $remote_addr;
    proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header    X-Forwarded-Proto $scheme;
  }
}
```
保存后，执行：
```
sudo ln -s /etc/nginx/sites-available/wikijs-https.conf /etc/nginx/sites-enabled/wikijs-https.conf
nginx -t
```
如果没有报错，重启Nginx：
```
sudo systemctl reload nginx.service
```

# 完成
```
sudo reboot
```