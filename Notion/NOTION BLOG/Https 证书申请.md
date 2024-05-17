---
type: Post
status: Published
date: 2024-01-02
tags:
  - 建站
category: 技术分享
---
1. 安装Certbot和Nginx插件：

```Shell
sudo apt update
sudo apt install certbot python3-certbot-nginx
```

1. 配置Nginx反向代理：
    
    在Nginx的配置文件中，将 `域名` 的反向代理配置为 `指定`端口。例如：
    
    ```Shell
    server {
        listen 80;
        server_name xx.xx.xx;
        location / {
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         proxy_set_header Host $http_host;
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header Range $http_range;
         proxy_set_header If-Range $http_if_range;
         proxy_redirect off;
         proxy_pass http://127.0.0.1:8181;
         # 上传的最大文件尺寸
         client_max_body_size 20000m;
      }
    
    }
    ```
    

3. 运行Certbot命令来获取和配置SSL证书： (这将使用Certbot的Nginx插件来自动配置SSL证书，并将其与Nginx进行集成。)

```Shell
sudo certbot --nginx -d xx.xx.xx
```

4. Certbot将引导您完成验证过程。一旦验证成功，证书将被下载并自动配置到Nginx中。