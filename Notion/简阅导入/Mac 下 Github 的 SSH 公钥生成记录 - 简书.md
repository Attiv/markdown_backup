## 前言：

自己作死下载了多个破解软件，不知道那个可能程序有问题，导致了电脑重启后无法开机，苦逼的只能重装系统，所以之前的所有配置都需要重新弄。所以破解软件请`**谨慎安装**`。

### Git 安装

> 直接下载安装 Xcode，高版本 Xcode 已经默认集成了 Git 。

### 生成 SSH key

SSH key 提供了一种与 GitHub 通信的方式，通过这种方式，能够在不输入密码的情况下，将 GitHub 作为自己的 remote 端服务器，可以实现本地 Git 仓库和 GitHub 仓库之间的数据传输，方便进行版本控制。

大多数 Git 服务器都会选择使用 SSH 公钥来进行授权。系统中的每个用户都必须提供一个公钥用于授权，没有的话就要生成一个。

> 步骤:
> 
> - 首先先确认一下是否已经有一个公钥了。SSH 公钥默认储存在账户的主目录下的～/.ssh 目录。进去看看：
> 
> ```Plain
> $ cd ~/.ssh
> $ ls
>  id_dsa       known_hosts
>  id_dsa.pub     config
> ```
> 
> - 关键是看有没有用 something 和 something.pub 来命名的一对文件，这个 something 通常就是 id_dsa 或 id_rsa。有 .pub 后缀的文件就是公钥，另一个文件则是密钥。如果已经有了，可直接跳到打开 id_rsa.pub，然后 copy 到 GitHub。如果没有，打开终端（Shell） ，创建 SSH Key：
> 
> ```Plain
> $ ssh-keygen -t rsa -C "youremail@example.com"
> ```
> 
> 或
> 
> ```Plain
> $ ssh-keygen
> Generating public/private rsa key pair.
> Enter file in which to save the key (/Users/schacon/.ssh/id_rsa):
> Enter passphrase (empty for no passphrase):
> Enter same passphrase again:
> Your identification has been saved in /Users/schacon/.ssh/id_rsa.
> Your public key has been saved in /Users/schacon/.ssh/id_rsa.pub.
> The key fingerprint is:
> 43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a schacon@agadorlaptop.local
> ```
> 
> `⚠️注意`它先要求你确认保存公钥的位置（.ssh/id_rsa），然后它会让你重复一个密码两次，如果不想在使用公钥的时候输入密码，可以留空或直接一路回车确定下就安装好了。查看是否成功：
> 
> ```Plain
> $ cd ~/.ssh
> $ ls
> id_rsa
> id_rsa.pub
> ```
> 
> - 打开 id_rsa.pub 文件，里面就有需要的 ssh key。  
>     在终端输入命令打开 id_rsa.pub，然后 copy。  
>     
> 
> ```Plain
> vim ~/.ssh/id_rsa.pub
> ```
> 
> 或
> 
> ```Plain
> $ cat ~/.ssh/id_rsa.pub
> ```
> 
> [![](http://upload-images.jianshu.io/upload_images/1076653-00fd3c6093500284.png)](http://upload-images.jianshu.io/upload_images/1076653-00fd3c6093500284.png)
> 
> 另注：所有做过这一步的用户都得把它们的公钥给你或者 Git 服务器的管理员（假设 SSH 服务被设定为使用公钥机制）。他们只需要复制 .pub 文件的内容然后发邮件给管理员。

### 将 SSH Key 添加到 GitHub 中

> 登陆 GitHub，打开 “SSH and GPG Keys” 页面：
> 
> [![](http://upload-images.jianshu.io/upload_images/1076653-989e4903cbee5866.png)](http://upload-images.jianshu.io/upload_images/1076653-989e4903cbee5866.png)

### 最后测试 github 是否连接成功

```Plain
$ssh -T git@github.com
```

### 如果显示：

```Plain
Are you sure you want to continue connecting (yes/no)?  ##输入yes##
```

### 接下来如果正常的话，会出现如下提示：

```Plain
Hi ZyjEugene! You've successfully authenticated, but GitHub does not
provide shell access.
```

### 如果出现如下提示，则说明有权限问题：

```Plain
Permission denied (publickey)....
```

### 如果有权限问题的情况下，你对项目执行 push 操作的时候，会得到如下提示：

```Plain
Warning: Permanently added the RSA host key for IP address '192.30.252.129' to the list of known hosts.
Permission denied (publickey).
fatal: Could not read from remote repository.

>Please make sure you have the correct access rights
and the repository exists.
```

## 权限问题：

`**原因**`：生成了多套 git ssh 密钥，并且都 Github 和客户端连接。通常一台电脑生成一个 ssh 不会有这个问题，当一台电脑生成多个 ssh 的时候，就可能遇到这个问题。`**解决步骤如下**`：  
1、查看系统 ssh-key 代理，执行如下命令  

```Plain
$ ssh-add -l
```

以上命令如果输出 `The agent has no identities`. 则表示没有代理。如果系统有代理，可以执行下面的命令清除代理:

```Plain
$ ssh-add -D
```

2、然后将你新创建的 ssh 添加代理，执行命令如下：

```Plain
$ ssh-add ~/.ssh/id_rsa
```

注：`id_rsa` 你的公私钥名称

3、你会得到如下提示：

```Plain
2048 8e:71:ad:88:78:80:b2:d9:e1:2d:1d:e4:be:6b:db:8e /Users/Eugene/.ssh/id_rsa (RSA)
```

4、测试 ssh

```Plain
ssh -T git@github.com
```

你若得到如下提示，表示这个 ssh 公钥已经获得了权限

```Plain
Hi ZyjEugene! You've successfully authenticated, but github does not provide shell access.
```

问题到此解决。

## 结束

鸣谢：[Pro Git 简体中文版](https://links.jianshu.com/go?to=http%3A%2F%2Fiissnan.com%2Fprogit%2F)[廖雪峰 Git 教程](https://links.jianshu.com/go?to=http%3A%2F%2Fwww.liaoxuefeng.com%2Fwiki%2F0013739516305929606dd18361248578c67b8067c8c017b000)

链接与资源：[猴子都能懂的 Git 教程](https://links.jianshu.com/go?to=http%3A%2F%2Fbacklogtool.com%2Fgit-guide%2Fcn%2Freference%2F)[Git - 简明指南](https://links.jianshu.com/go?to=http%3A%2F%2Frogerdudler.github.io%2Fgit-guide%2Findex.zh.html)

最后欢迎留言指正，谢谢🙏！ > 本文由简悦 SimpRead 转码