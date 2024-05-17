> 本文由 简悦 SimpRead 转码

[![](https://cdn.iosre.com/user_avatar/iosre.com/nerosir/45/5136_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/nerosir/45/5136_2.png)

# 写在前面：

# 此教极其适合像我这样的菜鸡食用 常人移步庆哥官方: [一条命令完成砸壳 658](http://www.alonemonkey.com/2018/01/30/frida-ios-dump) github:[frida-ios-dump 408](https://github.com/AloneMonkey/frida-ios-dump)

## ios 端配置：

- 打开 cydia 添加源：`https://build.frida.re`
- 打开刚刚添加的源 安装 [Frida 280](https://www.frida.re/docs/ios)
- 安装完成！检查是否工作可以可在手机终端运行 `frida-ps -U` 查看

## mac 端配置：

- 安装 [Homebrew 149](https://brew.sh/)
- 安装 python: `brew install python`
- 安装 wget: `brew install wget`
- 安装 pip:
    - `wget https://bootstrap.pypa.io/get-pip.py`
    - `sudo python get-pip.py`
- 安装 usbmuxd：`brew install usbmuxd`
- 清理残留: `rm ~/get-pip.py`

Ps: 使用`brew install xxx`如果一直卡在`Updating Homebrew…` 可以`control + z`结束当前进程 再新开一个终端安装 此时可以跳过更新

## 安装 frida for mac：

- 终端执行：
    - `sudo pip install frida`
- 假如报以下错误：
    - `Uninstalling a distutils installed project (six) has been deprecated and will be removed in a future version. This is due to the fact that uninstalling a distutils project will only partially uninstall the project.`
- 使用以下命令安装：
    - `sudo pip install frida –upgrade –ignore-installed six`

## 配置 frida-ios-dump 环境：

- 从 Github 下载工程：`sudo mkdir /opt/dump && cd /opt/dump && sudo git clone https://github.com/AloneMonkey/frida-ios-dump`
- 安装依赖：`sudo pip install -r /opt/dump/frida-ios-dump/requirements.txt --upgrade`
- 修改 dump.py 参数：`vim /opt/dump/frida-ios-dump/dump.py`  
    找到如下几行 (32~35)：  
    

```Plain
User = 'root'
      Password = 'alpine'
      Host = 'localhost'
      Port = 2222
```

```Plain
按需修改 如把Password 改成自己的
   ps:如果不习惯vim 用访达打开/opt/dump/frida-ios-dump/dump.py手动编辑。
```

- 设置别名：
    
    - 在终端输入：`vim ~/.bash_profile`
    - 在末尾新增下面一段：`alias dump.py="/opt/dump/frida-ios-dump/dump.py"`
    
    ## 注意：以上的 / opt/dump 可以按需更改 。
    
- 使别名生效：`source ~/.bash_profile`

## Enjoying and using it !

- 打开终端 设置端口转发:`iproxy 2222 22`
- command + n 新建终端执行一键砸壳 (QQ):`dump.py QQ`

好了 现在在终端 ls 查看刚刚的成果吧~

[![](https://cdn.iosre.com/user_avatar/iosre.com/zhang/45/7903_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/zhang/45/7903_2.png)

原作者发过贴了。在 [http://bbs.iosre.com/t/topic/10890/6 974](http://bbs.iosre.com/t/topic/10890/6)

[![](https://cdn.iosre.com/user_avatar/iosre.com/nerosir/45/5136_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/nerosir/45/5136_2.png)

[![](http://cdn.iosre.com/images/emoji/twitter/joy.png?v=6)](http://cdn.iosre.com/images/emoji/twitter/joy.png?v=6)

原作不适合菜鸡食用

好吧 这理由很牵强 假装自己没发

[![](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)

[![](http://cdn.iosre.com/user_avatar/iosre.com/nerosir/40/5136_1.png)](http://cdn.iosre.com/user_avatar/iosre.com/nerosir/40/5136_1.png)

nerosir:

> frida-ps -U

你好，ios 中用 cydia 安装了 frida 后，执行命令，显示：-sh: frida-ps: command not found，为什么提示无此命令行？（确认 cydia 已安装好了 Frida（11.0.3 版）的）

[![](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)

是的，我是输入了您上面写的命令的，mac 上 ssh 到 ios 上执行命令 frida-ps -U 如下：

[WX20180518-104135@2x.png770×144 19.9 KB](https://www.notion.so//cdn.iosre.com/uploads/default/original/2X/f/fd6280ddc6b0b879177c8815e14d2cc9f5248669.png) 后面我又在 ios 上直接安装了 terminal，然后执行 frida-ps -U，也是显示 command not found

[![](http://cdn.iosre.com/uploads/default/original/2X/f/fd6280ddc6b0b879177c8815e14d2cc9f5248669.png)](http://cdn.iosre.com/uploads/default/original/2X/f/fd6280ddc6b0b879177c8815e14d2cc9f5248669.png)

[![](https://cdn.iosre.com/user_avatar/iosre.com/zhang/45/7903_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/zhang/45/7903_2.png)

他忘了说在 Mac 上用 pip 装 frida

[![](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/x/85e7bf/45.png)](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/x/85e7bf/45.png)

这是 Mac 上用的 = =， -U 是指 usb 设备，，

[![](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)

[![](http://cdn.iosre.com/letter_avatar_proxy/v2/letter/p/22d042/40.png)](http://cdn.iosre.com/letter_avatar_proxy/v2/letter/p/22d042/40.png)

pyczd:

> frida-ps -U

谢谢！可以了！

[![](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/p/22d042/45.png)

是的，是的，谢谢！现在可以了！

[![](https://cdn.iosre.com/user_avatar/iosre.com/bigsen/45/5476_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/bigsen/45/5476_2.png)

确实适合菜鸟，很详细

[![](https://cdn.iosre.com/user_avatar/iosre.com/bigsen/45/5476_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/bigsen/45/5476_2.png)

请问 执行 python 脚本的时候提示： File “./dump.py”, line 21, in from scp import SCPClient ImportError: No module named scp

pip install SCPClient 也没用，到底什么原因。

[![](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/c/22d042/45.png)](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/c/22d042/45.png)

你应该 `pip install scp`。更准确地是 `pip install -r requirements.txt` 把所有的东西都装上。

---

下面到挖墙脚时间。

我后来写了一个只依赖 frida 和 node.js 的，一条命令安装

`npm install -g bagbak; bagbak 应用`

[![](https://github.githubassets.com/favicon.ico)](https://github.githubassets.com/favicon.ico)

[GitHub 12](https://github.com/ChiChou/bagbak)

### [ChiChou/bagbak 12](https://github.com/ChiChou/bagbak)

Yet another frida based iOS dumpdecrypted, works on iOS 13 with checkra1n and supports decrypting app extensions - ChiChou/bagbak

[![](https://cdn.iosre.com/user_avatar/iosre.com/bigsen/45/5476_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/bigsen/45/5476_2.png)

感谢，我试下。

[![](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/l/8c91f0/45.png)](https://cdn.iosre.com/letter_avatar_proxy/v4/letter/l/8c91f0/45.png)

mac 终端输入 pip install frida  
提示：  
  
Could not fetch URL  
[https://pypi.python.org/simple/frida/: 14](https://pypi.python.org/simple/frida/:) There was a problem confirming the ssl certificate: [SSL: TLSV1_ALERT_PROTOCOL_VERSION] tlsv1 alert protocol version (_ssl.c:661) - skipping  
Could not find a version that satisfies the requirement frida (from versions:)  
  
No matching distribution found for frida  

我翻墙了还是访问不了这个网站，不知道啥问题呢？

[![](https://cdn.iosre.com/user_avatar/iosre.com/alonemonkey/45/55_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/alonemonkey/45/55_2.png)

[github.com/pypa/pip 41](https://github.com/pypa/pip/issues/5236)

### [Issue: Problem Confirming the SSL Certificate - OSX 41](https://github.com/pypa/pip/issues/5236)

opened by [melsener](https://github.com/melsener) on [2018-04-15 41](https://github.com/pypa/pip/issues/5236) closed by [melsener](https://github.com/melsener) on [2018-04-16 41](https://github.com/pypa/pip/issues/5236)

```Plain
Pip version: pip 9.0.1
Python version: Python 3.5.2 and Python 2.7.10 installed
Operating system: OSX - 10.13.4
Description:
I've tried to install Keras (keras.io) and...
```

T: support

[![](https://cdn.iosre.com/user_avatar/iosre.com/yuzhouheike/45/5371_2.png)](https://cdn.iosre.com/user_avatar/iosre.com/yuzhouheike/45/5371_2.png)

上面的两个命令一个都不成功吗?