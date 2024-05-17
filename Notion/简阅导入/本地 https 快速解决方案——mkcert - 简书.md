[原文链接](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.dteam.top%2Fposts%2F2019-04%2F%25E6%259C%25AC%25E5%259C%25B0https%25E5%25BF%25AB%25E9%2580%259F%25E8%25A7%25A3%25E5%2586%25B3%25E6%2596%25B9%25E6%25A1%2588mkcert.html)

# 前言

在本地开发中，有时候我们经常需要模拟 https 环境，比如 PWA 应用要求必须使用 https 访问。在传统的解决方案中，我们需要使用自签证书，然后在 http server 中使用自签证书。由于自签证书浏览器不信任，为了解决浏览器信任问题我们需要将自签证书使用的 CA 证书添加到系统或浏览器的可信 CA 证书中，来规避这个问题。

以前这些步骤需要一系列繁琐的 `openssl` 命令生成，尽管有脚本化的方案帮助我们简化输入这些命令 (可以参考以前的 blog: [Nginx SSL 快速双向认证配置](https://www.jianshu.com/p/ba7f3f346bb8))。但是仍然觉得对本地开发不那么友好，有些繁重了。本文将介绍一种更加简单友好的方式生成本地 https 证书，并且信任自签 CA 的方案 —— [mkcert](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FFiloSottile%2Fmkcert)。

# mkcert 简介

[mkcert](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FFiloSottile%2Fmkcert) 是一个使用 go 语言编写的生成本地自签证书的小程序，具有跨平台，使用简单，支持多域名，自动信任 CA 等一系列方便的特性可供本地开发时快速创建 https 环境使用。

安装方式也非常简单，由于 go 语言的静态编译和跨平台的特性，官方提供各平台预编译的版本，直接下载到本地，给可执行权限 (Linux/Unix 需要) 就可以了。下载地址: [https://github.com/FiloSottile/mkcert/releases/latest](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FFiloSottile%2Fmkcert%2Freleases%2Flatest)

此外，mkcert 已经推送至 [Homebrew](https://links.jianshu.com/go?to=https%3A%2F%2Fbrew.sh%2F), [MacPorts](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.macports.org%2F), [Linuxbrew](https://links.jianshu.com/go?to=http%3A%2F%2Flinuxbrew.sh%2F), Chocolatey, Scoop 等包管理平台中，也可以直接借助对应的包管理平台安装。如:

```Plain
brew install mkcert  # Homebrew/Linuxbrew
choco install mkcert  # Chocolatey
```

安装成功后，应该可以使用 `mkcert` 命令了:

```Plain
PS C:\Users\abcfy\projects> mkcert
Using the local CA at "C:\Users\abcfy\AppData\Local\mkcert" ✨
Usage of mkcert:

        $ mkcert -install
        Install the local CA in the system trust store.

        $ mkcert example.org
        Generate "example.org.pem" and "example.org-key.pem".

        $ mkcert example.com myapp.dev localhost 127.0.0.1 ::1
        Generate "example.com+4.pem" and "example.com+4-key.pem".

        $ mkcert "*.example.it"
        Generate "_wildcard.example.it.pem" and "_wildcard.example.it-key.pem".

        $ mkcert -uninstall
        Uninstall the local CA (but do not delete it).

For more options, run "mkcert -help".
```

# mkcert 基本使用

从上面自带的帮助输出来看，`mkcert` 已经给出了一个基本的工作流，规避了繁杂的 `openssl` 命令，几个简单的参数就可以生成一个本地可信的 https 证书了。更详细的用法直接看[官方文档](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FFiloSottile%2Fmkcert%23mkcert)就好。

## 将 CA 证书加入本地可信 CA

```Plain
$ mkcert -install
Using the local CA at "C:\Users\abcfy\AppData\Local\mkcert" ✨
```

仅仅这么一条简单的命令，就帮助我们将 mkcert 使用的根证书加入了本地可信 CA 中，以后由该 CA 签发的证书在**本地**都是可信的。

在 Windows 的可信 CA 列表可以找到该证书:

[![](http://upload-images.jianshu.io/upload_images/4228468-b85e75b055f02007.png)](http://upload-images.jianshu.io/upload_images/4228468-b85e75b055f02007.png)

image.png

在 MacOS 的证书列表同样也可以找到:

[![](http://upload-images.jianshu.io/upload_images/4228468-3654014f39ed851a.png)](http://upload-images.jianshu.io/upload_images/4228468-3654014f39ed851a.png)

image.png

[![](http://upload-images.jianshu.io/upload_images/4228468-7c06cc8fc9c00ab9.png)](http://upload-images.jianshu.io/upload_images/4228468-7c06cc8fc9c00ab9.png)

image.png

同理，在 Linux 系统中也是类似的效果，这里就不演示了。

## 生成自签证书

生成自签证书的命令十分简单:

```Plain
mkcert domain1 [domain2 [...]]
```

直接跟多个要签发的域名或 ip 就行了，比如签发一个仅本机访问的证书 (可以通过 `127.0.0.1` 和 `localhost`，以及 ipv6 地址`::1` 访问)

```Plain
mkcert localhost 127.0.0.1 ::1
Using the local CA at "C:\Users\abcfy\AppData\Local\mkcert" ✨

Created a new certificate valid for the following names 📜
 - "localhost"
 - "127.0.0.1"
 - "::1"

The certificate is at "./localhost+2.pem" and the key at "./localhost+2-key.pem" ✅
```

通过输出，我们可以看到成功生成了 `localhost+2.pem` 证书文件和 `localhost+2-key.pem` 私钥文件，只要在 web server 上使用这两个文件就可以了。

# 使用生成的证书文件

默认生成的证书格式为 `PEM`(Privacy Enhanced Mail) 格式，任何支持 `PEM` 格式证书的程序都可以使用。比如常见的 `Apache` 或 `Nginx` 等，这里我们用 python 自带的 `SimpleHttpServer` 演示一下这个证书的效果 (代码参考来自: [https://gist.github.com/RichardBronosky/644cdfea681518403f5409fa16823c1f](https://links.jianshu.com/go?to=https%3A%2F%2Fgist.github.com%2FRichardBronosky%2F644cdfea681518403f5409fa16823c1f)):

python2 版本 (MacOS 自带的版本):

```Plain
#!/usr/bin/env python2

import BaseHTTPServer, SimpleHTTPServer
import ssl

httpd = BaseHTTPServer.HTTPServer(('0.0.0.0', 443), SimpleHTTPServer.SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket(httpd.socket, certfile='./localhost+2.pem', keyfile='./localhost+2-key.pem', server_side=True, ssl_version=ssl.PROTOCOL_TLSv1_2)
httpd.serve_forever()
```

python3 版本:

```Plain
#!/usr/bin/env python3

import http.server
import ssl

httpd = http.server.HTTPServer(('0.0.0.0', 443), http.server.SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket(httpd.socket, certfile='./localhost+2.pem', keyfile='./localhost+2-key.pem', server_side=True, ssl_version=ssl.PROTOCOL_TLSv1_2)
httpd.serve_forever()
```

使用 `python simple-https-server.py` 运行即可 (注意 Linux/Unix 下绑定 443 端口需要 root 权限，你可能需要使用 `sudo` 提权)

[![](http://upload-images.jianshu.io/upload_images/4228468-c0db74dc087f9417.png)](http://upload-images.jianshu.io/upload_images/4228468-c0db74dc087f9417.png)

image.png

[![](http://upload-images.jianshu.io/upload_images/4228468-bada3ecbe8e77f5e.png)](http://upload-images.jianshu.io/upload_images/4228468-bada3ecbe8e77f5e.png)

证书效果

# 局域网内使用

有时候我们需要在局域网内测试 https 应用，这种环境可能不对外，因此也无法使用像 `Let's encrypt` 这种免费证书的方案给局域网签发一个可信的证书，而且 `Let's encrypt` 本身也不支持认证 Ip。

先来回忆一下证书可信的三个要素:

- 由可信的 CA 机构签发
- 访问的地址跟证书认证地址相符
- 证书在有效期内

如果期望我们自签证书在局域网内使用，以上三个条件都需要满足。很明显自签证书一定可以满足证书在有效期内，那么需要保证后两条。我们签发的证书必须匹配浏览器的地址栏，比如局域网的 ip 或者域名，此外还需要信任 CA。

我们先重新签发一下证书，加上本机的局域网 ip 认证:

```Plain
mkcert localhost 127.0.0.1 ::1 192.168.31.170
Using the local CA at "C:\Users\abcfy\AppData\Local\mkcert" ✨

Created a new certificate valid for the following names 📜
 - "localhost"
 - "127.0.0.1"
 - "::1"
 - "192.168.31.170"

The certificate is at "./localhost+3.pem" and the key at "./localhost+3-key.pem" ✅
```

再次验证发现使用 `https://192.168.31.170` 本机访问也是可信的。然后我们需要将 CA 证书发放给局域网内其他的用户。

```Plain
mkcert -CAROOT
C:\Users\abcfy\AppData\Local\mkcert
```

使用 `mkcert -CAROOT` 命令可以列出 CA 证书的存放路径

```Plain
ls $(mkcert -CAROOT)


    目录: C:\Users\abcfy\AppData\Local\mkcert


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----  2019-04-09-星期二  上午 1           2484 rootCA-key.pem
                             2:16
-a----  2019-04-09-星期二  上午 1           1651 rootCA.pem
                             2:16
```

可以看到 CA 路径下有两个文件 `rootCA-key.pem` 和 `rootCA.pem` 两个文件，用户需要信任 `rootCA.pem` 这个文件。将 `rootCA.pem` 拷贝一个副本，并命名为 `rootCA.crt`(因为 windows 并不识别 `pem` 扩展名，并且 Ubuntu 也不会将 `pem` 扩展名作为 CA 证书文件对待)，将 `rootCA.crt` 文件分发给其他用户，手工导入。

windows 导入证书的方法是双击这个文件，在证书导入向导中将证书导入`受信任的根证书颁发机构`:

[![](http://upload-images.jianshu.io/upload_images/4228468-ee455e55362201b3.png)](http://upload-images.jianshu.io/upload_images/4228468-ee455e55362201b3.png)

image.png

MacOS 的做法也一样，同样选择将 CA 证书导入到受信任的根证书办法机构。

Ubuntu 的做法可以将证书文件 (必须是 `crt` 后缀) 放入 `/usr/local/share/ca-certificates/`，然后执行 `sudo update-ca-certificates`

Android 和 IOS 信任 CA 证书的做法参考[官方文档](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FFiloSottile%2Fmkcert%23mobile-devices)。

在局域网其他计算机就可以访问 https 而不报警了。我在另一台虚拟机 Ubuntu 上使用 curl 测试结果:

```Plain
$ curl -I https://192.168.31.170
HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.6.8
Date: Tue, 09 Apr 2019 05:22:12 GMT
Content-type: text/html; charset=utf-8
Content-Length: 1794
```

无警告，加上 `-v` 参数输出还会告诉证书是可信的。

# 其他一些高级用法

以上我们演示了一些 `mkcert` 最基本的用法，非常简单。如果我们打开 `mkcert --help` 看帮助的话，还会发现很多高级用法。

比如 `-cert-file FILE, -key-file FILE, -p12-file FILE` 可以定义输出的证书文件名。

- `client` 可以产生客户端认证证书，用于 SSL 双向认证。之前的文章介绍过使用 openssl 脚本的 ([Nginx SSL 快速双向认证配置](https://www.jianshu.com/p/ba7f3f346bb8))，可以对比下。
- `pkcs12` 命令可以产生 `PKCS12` 格式的证书。java 程序通常不支持 `PEM` 格式的证书，但是支持 `PKCS12` 格式的证书。通过这个程序我们可以很方便的产生 `PKCS12` 格式的证书直接给 Java 程序使用，这里就不演示了。

其他高级用法不做介绍了，各位有兴趣可以根据自己的实际需求和场景进行发掘吧。

# 小结

本篇文章我们介绍了一个好用的小工具 [mkcert](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FFiloSottile%2Fmkcert)，简化我们在本地搭建 https 环境的复杂性，无需操作繁杂的 openssl 实现自签证书了，这个小程序就可以帮助我们自签证书，在本机使用还会自动信任 CA，非常方便。 > 本文由简悦 SimpRead 转码