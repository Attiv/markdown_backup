> 服务端要使用 https 几乎已经是所有开发者的共识，目前日常接触到的绝大部分网站都启用的 https，各大浏览器也会对非 https 网站进行标识，已表明它是不安全的。

服务端要使用 https 几乎已经是所有开发者的共识，目前日常接触到的绝大部分网站都启用的 https，各大浏览器也会对非 https 网站进行标识，已表明它是不安全的。  
但为什么本地环境下也需要启用 https 环境呢？  
  
即使忽略掉本地环境的不安全因素（如  
[HTTPS Downgrade Attacks](https://auth0.com/blog/preventing-https-downgralde-attacks/)），本地开启 https 服务也是极有意义的。  
比如可以使用浏览器的一些新特性 (Notification, Geolocation, Clipboard)，几乎所有特性都强制要求使用 https，否则就直接罢工，不能本地总是只管写，测试到了服务端再测吧？  
  
详情可以参考  
[Secure contexts](https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts)  
或者可以避免跨域以带来的 iframe 或者 cookie 的权限问题，又或者可以通过自定义域然后通过反向代理来区分不同的项目，同时启动多个开发环境。  

## 介绍

忽略掉使用 OpenSSL 生成根证书、信任根证书、为域颁发证书、启动开发服务时使用证书等等等等的一系列复杂的步骤。[mkcert](https://github.com/FiloSottile/mkcert) 是一个使用 go 语言编写的生成本地自签证书的工具，具有跨平台，使用简单，支持多域名，自动信任 CA 等一系列方便的特性，让你可以在本地简单又迅速的生成证书并且快速部署到开发环境中去。

## 使用

### 安装

无论你在使用哪个平台，都推荐使用包管理器进行[安装](https://github.com/FiloSottile/mkcert#installation)：

```Plain
brew install mkcert
// 或者
choco install mkcert
```

安装成功后，就可以使用 mkcert 命令了。

### 信任

> mkcert 自动生成的 rootCA-key.pem 文件提供了拦截来自本机安全请求的完整能力。不要分享这个文件。

将 CA 证书加入本地可信 CA 这一步非常简单，只需要：

```Plain
mkcert -install
```

然后在系统中可以找到：

[![](https://blog.osvlabs.com/wp-content/uploads/2023/01/cert-local.png)](https://blog.osvlabs.com/wp-content/uploads/2023/01/cert-local.png)

### 生成证书

生成证书非常简单，只需要如下命令：

```Plain
mkcert example.org
```

即可在当前目录下生成证书，默认为 PEM 格式。

### 使用

### webpack

前端开发中通常使用 webpack 来进行构造开发环境，其他工具请参考相应文档。  
Webpack 中使用 https 非常简单，只需要再 devServer 处添加证书  

```Plain
module.exports= {
  //…
    devServer: {
    https: true,
    key: fs.readFileSync('/path/to/server-key.pem'),
    cert: fs.readFileSync('/path/to/server.pem')
  }
};
```

### ngnix

Ngnix 只需配置 nginx.conf：

```Plain
server{
    // …
    ssl_certificate cert/domain name.pem;
    ssl_certificate_key cert/domain server-key.pem;
}
```

## traffic

Traffic 的配置也十分简单，同样只需要在配置中加入证书位置即可：

```Plain
[[tls.certificates]]
certFile = "/path/to/domain.pem"
keyFile = "/path/to/server-key.pem"
```

> 本文由简悦 SimpRead 转码