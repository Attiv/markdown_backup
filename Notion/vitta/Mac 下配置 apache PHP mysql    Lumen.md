Mac 下配置 apache PHP mysql

步骤：

安装 homebrew

安装 php (mac 默认有PHP 版本 )查看本机php版本：php -v

配置apache（mac默认有apache） vhost

安装mysql

配置 hosts

安装 npm

安装homebrew ：ruby -e "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/master/install](https://raw.githubusercontent.com/Homebrew/install/master/install))"

*安装：apache php版本（选装 mac自带apache php）

brew tap homebrew/apache brew tap homebrew/php

brew install httpd24 brew install php53

安装数据库

brew install mysql

配置mac 自带apache(重启 apache服务器 sudoapachectl restart 查看80端口 netstat -anl | grep "80")

地址： /etc/apache2/httpd.conf (可先复制备份一份 sudo cp /etc/apache2/httpd.conf /etc/apache2/httpd.conf.backup )

配置监听端口为80

\#LoadModule php5_module libexec/apache2/libphp5.so 将#删除 配置mac自带的php版本

如果本地mac 自带php版本过低 需升级。[http://weiww.jianshu.com/p/0456dd3cc78b](http://www.jianshu.com/p/0456dd3cc78b)

下载 php curl -s [http://php-osx.liip.ch/install.sh](http://php-osx.liip.ch/install.sh) | bash -s 5.6

在httpd.conf 加入引用本地php的配置 LoadModule php5_module /usr/local/php5-5.6.27-20161101-100213/libphp5.so（自己的路径）

配置apache ->/etc/apache/extra/httpd-vhosts.conf (最好备份)

配置vhosts文件

端口号为：80

DocumentRoot "/Users/****/projects/webtailor-backend/public" 配置后端入口 在项目的public目录下 后端代码 不要放在桌面上 最好在/users目录下 新建一个项目文件夹

配置apache ->/etc/hosts (最好备份)

配置vhosts文件

配置与 /etc/apache/extra/httpd-vhosts.conf对应

配置完成 在浏览器中打开 localhost

参考：

[https://my.oschina.net/joanfen/blog/171109](https://my.oschina.net/joanfen/blog/171109)

Lumen

后台:

Comopser 安装 项目根目录

composer install

composer require basicit/lumen-vendor-publish

composer dump-autoload

前端：

配置数据库

启动 mysql -> mysql.server start

查看mysql 是否运行： brew services list

netstat -anl | grep "3306"

下载可视化mysql管理软件：

[http://blog.csdn.net/u013980127/article/details/51604646](http://blog.csdn.net/u013980127/article/details/51604646)

mysql默认密码为空，修改密码 mysqladmin -uroot password "密码" ->修改密码为root mysqladmin -uroot password root

mysql2002错误 [http://stackoverflow.com/questions/15016376/cant-connect-to-local-mysql-server-through-socket-homebrew](http://stackoverflow.com/questions/15016376/cant-connect-to-local-mysql-server-through-socket-homebrew)

创建数据库表：打开数据库 ：

或者在可视化软件上建立数据库表

后端项目根目录 ： php artisan 命令列表

php artisan migrate 进行数据的迁移