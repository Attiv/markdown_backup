NGINX：  
Docroot is: /usr/local/var/www  

The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that

nginx can run without sudo.

nginx will load all files in /usr/local/etc/nginx/servers/.

To start nginx now and restart at login:

brew services start nginx

brew services start nginx // 重启的命令是: brew services restart nginx

  

To connect run:  
mysql -u root  

To start mysql now and restart at login:  
brew services start mysql