# Brew install

`-fs` 安装当前可用版本

# Apache配置

`/usr/local/etc/apache2/2.4`

> Apache2.4的配置:

```Plain
Options +Indexes +FollowSymLinks +MultiViews
 AllowOverride All
 Require all granted
```

# 查找`php.ini`

`php -i | grep "php.ini"`

# 数据库

`/usr/local/mysql/bin/mysql -u 用户名 -p`

%0A%23%23%20Brew%20install%0A%60-fs%60%20%E5%AE%89%E8%A3%85%E5%BD%93%E5%89%8D%E5%8F%AF%E7%94%A8%E7%89%88%E6%9C%AC%0A%0A%23%23%20Apache%E9%85%8D%E7%BD%AE%0A%60%2Fusr%2Flocal%2Fetc%2Fapache2%2F2.4%60%0A%0A%3EApache2.4%E7%9A%84%E9%85%8D%E7%BD%AE%3A%0A%60%60%60%0AOptions%20%2BIndexes%20%2BFollowSymLinks%20%2BMultiViews%0A%20AllowOverride%20All%0A%20Require%20all%20granted%20%20%0A%60%60%60%0A%0A%23%23%20%E6%9F%A5%E6%89%BE%60php.ini%60%0A%60php%20-i%20%7C%20grep%20%22php.ini%22%60%0A%0A%0A%23%23%20%E6%95%B0%E6%8D%AE%E5%BA%93%0A%60%20%2Fusr%2Flocal%2Fmysql%2Fbin%2Fmysql%20-u%20%E7%94%A8%E6%88%B7%E5%90%8D%20-p%60