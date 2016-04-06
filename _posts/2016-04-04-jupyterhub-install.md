--- 
title: jupyterhub
layout: post
category: python
---

## 准备
先要安装python3, node

```shell
sudo apt-get install python3 python3-pip python3-dev -y
sudo apt-get install npm nodejs-legacy -y
sudo npm install -g configurable-http-proxy

```

## 安装

[jupyterhub github url][1]

```shell
sudo pip3 install jupyterhub
sudo pip3 install --upgrade notebook
```

## 配置

```shell
mkdir /var/www/jupyterhub
cd /var/www/jupyterhub
jupyterhub --generate-config
vi jupyterhub_config.py
```

### 修改配置文件
```
c.JupyterHub.ip = '127.0.0.1'
c.JupyterHub.port = 8000
c.JupyterHub.proxy_auth_token = 'way'
c.Authenticator.admin_users = set('way')
```

### nginx 配置

```
server {
  listen          80;       # Listen on port 80 for IPv4 requests
  listen          443 ssl;
  server_name     notebook.prowayne.com;

  ssl_certificate       /var/www/jupyterhub/ca.crt;
  ssl_certificate_key   /var/www/jupyterhub/ca.key;
  ssl_protocols         TLSv1 TLSv1.1 TLSv1.2;

  access_log      /var/log/nginx/jupyterhub/access.log;
  error_log       /var/log/nginx/jupyterhub/error.log;

  location @ipython {
    sendfile off;
    proxy_pass         http://127.0.0.1:8000;
    proxy_redirect     default;

    proxy_http_version 1.1;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection "upgrade";
    proxy_set_header   Origin "";

    proxy_set_header   Host             $host;
    proxy_set_header   X-Real-IP        $remote_addr;
    proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
    proxy_max_temp_file_size 0;

    #this is the maximum upload size
    client_max_body_size       10m;
    client_body_buffer_size    128k;

    proxy_connect_timeout      90;
    proxy_send_timeout         90;
    proxy_read_timeout         90;

    proxy_buffer_size          4k;
    proxy_buffers              4 32k;
    proxy_busy_buffers_size    64k;
    proxy_temp_file_write_size 64k;
}

  location / {
    try_files $uri @ipython;
   }
}
```

### 添加一个启动脚本

launch.sh

```shell
#!/usr/bin/env bash
set -e
exec jupyterhub -f jupyterhub_config.py --no-ssl
```

### 添加一个supervisor配置

jupyterhub.ini

```
[program:jupyterhub]
command=bash launch.sh
numprocs=1
numprocs_start=0
priority=999
autostart=true
autorestart=unexpected
startsecs=3
startretries=3
exitcodes=0,2
stopsignal=TERM
stopwaitsecs=60
directory=/var/www/jupyterhub
user=root
stdout_logfile=/var/www/jupyterhub/hub.log
stderr_logfile=/var/www/jupyterhub/hub.err
environment=PYTHONPATH='/var/www/jupterhub'
```

## 最后

```shell
supervisorctl reread
supervisorctl update
```
服务就起来了

[1]:https://github.com/jupyter/jupyterhub

