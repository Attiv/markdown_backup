## **为何用docker？**

在电脑还是window系统的时候，经常需要基于vm服务搭建一套环境才能更好地（应该是更贴近线上环境）进行开发，而现在在docker的神秘光环底下已经能实现用最小的资源搭建本地开发环境，同时能更好地迁移到其他地方。

## **前置知识**

- 了解docker安装及使用
- 了解docker-compose命令行的使用
- 了解laravel安装及使用

本文主要使用[`laradock`](https://github.com/laradock/laradock)进行本地的docker配置。`laradock`已经集成laravel需要使用的环境，只需要简单修改配置就能搭建环境提供开发，对开发及管理来说真是一味良方。

简单说明一下，在`docker`环境下我们需要运行`laravel`项目，实际会建立下几个容器(container)：

- workspace (开发环境)
- php-fpm (php支持)
- nginx (web服务)
- mysql (数据库)

这些都是基于`laradock`再处理后的生成的容器，可参考`laradock`目录下相应名字的目录，里面包含`Dockerfile`及相关配置，感兴趣的同学可以尽情阅读学习 :)

更加深入的内容建议移步至[laradock官方文档](http://laradock.io/)。

## **准备**

在window系统下先安装[`docker`](https://www.docker.com/get-docker)

[![](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3FeJ)](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3FeJ)

等多次重启后运行`docker`命令测试一下。

[![](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Ff9)](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Ff9)

然后在你项目的平级目录使用`git`拉取`https://github.com/laradock/laradock.git`这个包。

```Plain
# 平级目录

D:/www/
 - /laradock
 - /my-project
```

这样准备就绪进入下一步。

## **配置**

这里配置的环境按常用环境进行配置

- nginx
- php-fpm 5.6
- mysql 5.6

接着需要修改`laradock/.env`文件

```Plain
/www/laradock
 - .env
```

进入`laradock`目录会发现并不存在`.env`文件，这里需要我们从`env-example`复制一份进行修改。

```Plain
# /www/laradock

$ cp env-example .env
```

### **修改PHP版本**

进入`.env`文件找到 `PHP_VERSION` 修改php版本为56（默认71，可选71, 70, 56）。

```Plain
# /www/laradock/.env
### PHP Version

PHP_VERSION=56
```

### **修改Mysql版本及配置**

进入`.env`文件找到 `MYSQL` 修改mysql版本为56（默认8，可选8, 5, 5.6, 5.5）。

其他的设置根据个人需要填写，一般情况下需要修改`MYSQL_USER`, `MYSQL_PASSWORD`, `MYSQL_ROOT_PASSWORD` 来确保链接。

```Plain
# /www/laradock/.env
### MYSQL

MYSQL_VERSION=5.6

# MYSQL_DATABASE 可选，填写后会默认创建同名数据库
MYSQL_DATABASE=default

# MYSQL_USER 用户，填写后会创建用户，默认为 default
MYSQL_USER=packy

# MYSQL_PASSWORD 密码，填写后作为新建用户的密码，默认为 secret
MYSQL_PASSWORD=123456-

# MYSQL_PORT 访问端口，默认是3306，建议不要修改
MYSQL_PORT=3306

# MYSQL_ROOT_PASSWORD root用户密码，建议使用严谨的密码，默认为 root
MYSQL_ROOT_PASSWORD=23333-
MYSQL_ENTRYPOINT_INITDB=./mysql/docker-entrypoint-initdb.d
```

### **关于Mysql版本选择**

mysql使用的是官方镜像，所以我们可以使用[hub.docker.com](https://hub.docker.com/)查询`mysql`官方镜像包含哪些版本。具体如何选择得看各自的需求。

[![](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Fgz)](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Fgz)

### **修改nginx配置**

一般情况下并不需要修改什么，使用默认的便可。关于网站的配置需要进入`laradock/nginx/sites`。

> 如需要修改端口可以进入.env文件找到 NGINX进行修改。

```Plain
# /www/laradock/.env
### NGINX

NGINX_HOST_HTTP_PORT=80
NGINX_HOST_HTTPS_PORT=443

# NGINX_HOST_LOG_PATH log存放位置，默认位置在laradock/logs/nginx/
NGINX_HOST_LOG_PATH=./logs/nginx/

# NGINX_SITES_PATH 网站配置, 默认位置在laradock/nginx/sites/
NGINX_SITES_PATH=./nginx/sites/

NGINX_PHP_UPSTREAM_CONTAINER=php-fpm
NGINX_PHP_UPSTREAM_PORT=9000
```

### **关于Nginx的配置**

`nginx`的配置文件存放在`laradock/nginx/sites`下，需要新建网站的可通过复制对应的`.example`并重命名为`.conf`进行修改。注：只用`.conf`文件才会在`nginx`下加载。

这里我复制`laravel.conf.example`作为例子重命名为`my-project.conf`：

```Plain
# laradock/nginx/sites/my-project.conf
server {

    listen 80;
    listen [::]:80;

    # 域名，改为你的域名
    server_name my-project.com;
    # 项目目录，均以 /var/www/ 开头。这个约定后续会说明
    root /var/www/my-project;
    index index.php index.html index.htm;

    location / {
         try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        try_files $uri /index.php =404;
        fastcgi_pass php-upstream;
        fastcgi_index index.php;
        fastcgi_buffers 16 16k;
        fastcgi_buffer_size 32k;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    location /.well-known/acme-challenge/ {
        root /var/www/letsencrypt/;
        log_not_found off;
    }

    error_log /var/log/nginx/laravel_error.log;
    access_log /var/log/nginx/laravel_access.log;
}
```

同时修改宿主机（就是window本地机子）的`hosts`

```Plain
# C:\Windows\System32\drivers\etc\hosts

127.0.0.1   my-project.com
```

### **尝试运行**

到这步准备工作差不多完成了。

运行以下命令进行安装及使用，因为是国外源拉取时间比较慢请耐心等待。

```Plain
docker-compose up -d nginx mysql
```

[![](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3FgS)](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3FgS)

完成后输入`docker ps`参看容器运行情况。一切正常！！！

[![](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Fhb)](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Fhb)

尝试访问`http://my-project.com`看看效果。目前能正常访问`php`文件。

[![](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3FhM)](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3FhM)

### **运行laravel**

这里就不得说`workspace`这个容器，它作为工作区提供各类工具使用（包含：PHP CLI, Composer, Git, Linuxbrew, Node, V8JS, Gulp, SQLite, xDebug, Envoy, Deployer, Vim, Yarn等）。

那如何使用这些功能呢？

### **首先进入**`**workspace**`**容器**

```Plain
# /www/laradock
docker-compose exec workspace bash
```

### **composer换国内源**

进到容器后默认就是项目目录`/var/www`，由于composer用的是国外源比较慢，这里需要切换成国内源。

```Plain
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

### **安装laravel**

这里我们需要在`my-project`目录安装laravel。

> *注：需要提前把my-project里的所有内容清空

```Plain
composer create-project laravel/laravel my-project2 "5.2.*" && \
cd my-project && \
php artisan key:generate
```

### **配置并重启nginx**

安装完成后，把`laradock/nginx/sites/my-project.conf`文件下的网站目录地址稍微改一下

```Plain
server {

    listen 80;
    listen [::]:80;

    server_name my-project.com;
    # 加上public目录
    root /var/www/my-project/public;
    index index.php index.html index.htm;

    ...
}
```

重启`nginx`容器

```Plain
# /www/laradock
docker-compose restart nginx
```

[![](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Fin)](https://www.notion.so%E4%BD%BF%E7%94%A8docker%E6%90%AD%E5%BB%BAlaravel%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%20-%20%E5%B8%95%E5%A5%87%E7%9A%84%E6%89%8B%E6%9C%AD%20-%20SegmentFault%20%E6%80%9D%E5%90%A6.resources/bV3Fin)

### **关于数据库服务**

```Plain
# .env
DB_CONNECTION=mysql

# mysql的容器网络已经解析至"mysql"域，所以这里配置"mysql"域便能访问
DB_HOST=mysql

# 默认3306，一般不需要改动，如要改动端口应该与laradock/.env中的MYSQL_PORT一致
DB_PORT=3306

# 数据库
DB_DATABASE=default

# 用户
DB_USERNAME=packy

# 密码
DB_PASSWORD=123456-
```

### **一些问题：**

Q：运行失败，提示`ERROR: for laradock_mysql_1 Cannot create container for service mysql: Drive sharing seems blocked by a firewall`

A：先暂停你本机杀毒程序的防御进程。

---

Q：运行失败，提示`ERROR: for laradock_nginx_1 Cannot start service nginx: driver failed programming external connectivity on endpoint laradock_nginx_1 (6e4f4761d30f4cd80c44c6b0fddfbd4ef0324529099aace02bee6a6653ce453a): Error starting userland proxy: Bind for 0.0.0.0:443 failed: port is already allocated`

A：建议你切换端口，我已尝试改为1443能正常运行，目前只能以这种方式处理。

---

```Plain
# .env
### NGINX

NGINX_HOST_HTTPS_PORT=1443
```

---

Q：为何网站目录必须以`/var/www`开头？

A：网站访问进入的是`nginx`容器，`/var/www`目录就是容器内网站目录存放的位置。由于配置在创建容器时，会将本地目录挂载至`/var/www`目录，所以就能访问到本地的代码。这块设置在`laradock/.env`中找到`APPLICATION`可自行设置。

---

Q：Windows下开启了Hyper-v后安卓模拟器及VMware均不能用了？

A：对的，貌似是因为Hyper-v独占硬件虚拟化，使用其他虚拟化技术（如：VMware, virtualbox）均不能使用（开启可能蓝屏），目前并没有共存手段。这里博主建议需要模拟安卓系统的可以直接在Hyper-v上安装，关于GUI渲染的性能方面听说还行。（博主并没尝试，考虑最近尝试一波）