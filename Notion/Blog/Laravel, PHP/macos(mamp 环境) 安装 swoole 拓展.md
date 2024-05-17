首先下载压缩包，[https://github.com/swoole/swoole-src/releases](https://www.shiqidu.com/url/https://github.com/swoole/swoole-src/releases)  
解压后进如 swoole 目录执行 phpize 命令，发现报了下面这个错  

```Plain
sudo /Applications/MAMP/bin/php/php7.0.22/bin/phpize           
Password:          
Configuring for:          
PHP Api Version:         20151012          
Zend Module Api No:      20151012          
Zend Extension Api No:   320151012          
Cannot find autoconf. Please check your autoconf installation and the          
$PHP_AUTOCONF environment variable. Then, rerun this script.
```

因为是 mac 环境，执行执行 brew 安装这个东西即可

```Plain
brew install autoconf
```

等待安装完成后，在执行 phpize 命令

```Plain
sudo /Applications/MAMP/bin/php/php7.0.22/bin/phpize
```

这次应该不会报错了，同事在目录下生成了`configure`可执行文件。

然后执行下面的命令

```Plain
./configure --with-php-config=/Applications/MAMP/bin/php/php7.0.22/bin/php-config
```

执行成功后就可以编译安装了

```Plain
make && make install
```

然后把 swoole 拓展加到 php.ini 里

[![](https://www.shiqidu.com/uploads_nj/article/20171102/f9a4f5741c290a40f640efe42560738a.png)](https://www.shiqidu.com/uploads_nj/article/20171102/f9a4f5741c290a40f640efe42560738a.png)

[![](https://www.shiqidu.com/uploads_nj/article/20171102/393db0fad6d2325d944f6b377211de50.png)](https://www.shiqidu.com/uploads_nj/article/20171102/393db0fad6d2325d944f6b377211de50.png)

```Plain
extension=swoole.so
```

然后重启 mamp，使用 phpinfo 函数查看是否安装成功。

[![](https://www.shiqidu.com/uploads_nj/article/20171102/00301375fc414bfc6525ae0b5f0f4f5e.png)](https://www.shiqidu.com/uploads_nj/article/20171102/00301375fc414bfc6525ae0b5f0f4f5e.png)

这个时候你按照官方教程使用`php -m`命令查看你你发现 modules 里面并没有 swoole，这是因为 mac 命令行默认使用的 php 并不是 mamp 的而是系统自带的，所以我们需要把默认的 php 切换成 mamp 的 php，具体操作如下：

在命令行输入下面的命令

```Plain
sudo vi ~/.bash_profile
```

然后在文件最下方添加下面的代码

```Plain
PATH="/Applications/MAMP/bin/php/php7.0.22/bin:$PATH"      
export PATH
```

然后`:x`保存退出。再执行`php -m`命令。

[![](https://www.shiqidu.com/uploads_nj/article/20171102/8013b3aaf43694b9a2b1632284f0ae77.png)](https://www.shiqidu.com/uploads_nj/article/20171102/8013b3aaf43694b9a2b1632284f0ae77.png)

### 更新于 2017 年 11 月 02 日 22:53:19

注意使用`php -i |grep php.ini`查看你的`php.ini`位置，如果显示在`/etc`下，但是并没有现实具体的文件名，你可能需要执行下面的生成一个`php.ini`文件

```Plain
sudo cp php.ini.default ./php.ini
```