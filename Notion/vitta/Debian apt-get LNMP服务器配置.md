`vi /etc/apt/sources.list`  
#在最后加入：  

```Plain
deb http://mirror.us.leaseweb.net/dotdeb/ stable all
deb-src http://mirror.us.leaseweb.net/dotdeb/ stable all
wget http://www.dotdeb.org/dotdeb.gpg  #导入密钥
apt-key add dotdeb.gpg
```

//上述可能没有作用`sudo apt-get update`

1. `sudo apt-get install -y mysql-server mysql-client`
2. `sudo apt-get intsall nginx`
3. `sudo apt-get install php7.0`

https://laracasts.com/discuss/channels/forge/updating-forgeubuntu-w-ppaondrejphp

`sudo apt-get install software-properties-common`

`sudo rm /etc/apt/sources.list.d/ondrej-php-*`

`sudo add-apt-repository ppa:ondrej/php`

`sudo apt-get update`

`sudo apt-get install php7.0`

如果有问题请执行开头，主要是 `sudo apt-get update`

4.php一些扩展

`sudo apt-get install php7.0-fpm php7.0-mcrypt`等。。。。

%60vi%20%2Fetc%2Fapt%2Fsources.list%60%0A%23%E5%9C%A8%E6%9C%80%E5%90%8E%E5%8A%A0%E5%85%A5%EF%BC%9A%0A%60%60%60%0Adeb%20http%3A%2F%2Fmirror.us.leaseweb.net%2Fdotdeb%2F%20stable%20all%0Adeb-src%20http%3A%2F%2Fmirror.us.leaseweb.net%2Fdotdeb%2F%20stable%20all%0Awget%20http%3A%2F%2Fwww.dotdeb.org%2Fdotdeb.gpg%20%20%23%E5%AF%BC%E5%85%A5%E5%AF%86%E9%92%A5%0Aapt-key%20add%20dotdeb.gpg%0A%60%60%60%0A%2F%2F%E4%B8%8A%E8%BF%B0%E5%8F%AF%E8%83%BD%E6%B2%A1%E6%9C%89%E4%BD%9C%E7%94%A8%0A%60sudo%20apt-get%20update%60%0A%20%0A1.%20%60sudo%20apt-get%20install%20-y%20mysql-server%20mysql-client%60%0A%0A2.%20%60sudo%20apt-get%20intsall%20nginx%60%0A%0A3.%20%60sudo%20apt-get%20install%20php7.0%60%0A%0Ahttps%3A%2F%2Flaracasts.com%2Fdiscuss%2Fchannels%2Fforge%2Fupdating-forgeubuntu-w-ppaondrejphp%0A%0A%60sudo%20apt-get%20install%20software-properties-common%60%0A%0A%60sudo%20rm%20%2Fetc%2Fapt%2Fsources.list.d%2Fondrej-php-*%60%0A%0A%60sudo%20add-apt-repository%20ppa%3Aondrej%2Fphp%60%0A%0A%60sudo%20apt-get%20update%60%0A%0A%60sudo%20apt-get%20install%20php7.0%60%0A%0A%E5%A6%82%E6%9E%9C%E6%9C%89%E9%97%AE%E9%A2%98%E8%AF%B7%E6%89%A7%E8%A1%8C%E5%BC%80%E5%A4%B4%EF%BC%8C%E4%B8%BB%E8%A6%81%E6%98%AF%20%60sudo%20apt-get%20update%60%0A%0A4.php%E4%B8%80%E4%BA%9B%E6%89%A9%E5%B1%95%0A%0A%60sudo%20apt-get%20install%20php7.0-fpm%20php7.0-mcrypt%60%E7%AD%89%E3%80%82%E3%80%82%E3%80%82%E3%80%82%0A%0A