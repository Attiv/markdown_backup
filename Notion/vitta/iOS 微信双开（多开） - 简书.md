> 本文由 简悦 SimpRead 转码

### 微信双开思路

主要思路是修改微信的 bundle id，本文主要讲需要修改哪些 info.plist 中的 bundle id。根据以下修改逻辑，可以修改任何一个 iOS 的 ipa 包。

### 需修改的内容

1. 前提你需要从越狱机导出微信的 ipa 包。（这里不讲解这个过程，如果想了解或者想要各种应用的 ipa 包可以私信我）
2. 拿到微信 ipa 包，解压 ipa 包，会出现 Payload/WeChat，点击 WeChat 右键显示包内容，如下图： 0.png
    
    [![](http://upload-images.jianshu.io/upload_images/4898000-860bbf8bfc97699e.png)](http://upload-images.jianshu.io/upload_images/4898000-860bbf8bfc97699e.png)
    
3. 找到 WeChat 内的 info.plist, 把 Bundle identifier 的值从 com.tencent.xin 修改为 com.tencent.xina ，如下图： 1.jpg
    
    [![](http://upload-images.jianshu.io/upload_images/4898000-25968c9e9c0aff92.jpg)](http://upload-images.jianshu.io/upload_images/4898000-25968c9e9c0aff92.jpg)
    
4. 然后找到 WeChat 内的 PlugIns 文件夹中的插件，此文件夹下的所有插件的 bundle id 都需要修改，如下图： 2.png 3.jpg
    
    [![](http://upload-images.jianshu.io/upload_images/4898000-55eabf8410fd15cb.png)](http://upload-images.jianshu.io/upload_images/4898000-55eabf8410fd15cb.png)
    
    例如：我要修改 WeChatNotificationServiceExtension.appex 插件，选择此插件右键显示包内容，找到 info.plist 文件，把 Bundle identifier 的前缀值修改为主 info.plist 的 Bundle identifier。（其他插件也这样系乖）如下图修改：
    
    [![](http://upload-images.jianshu.io/upload_images/4898000-e9ed5d4fb617a2f3.jpg)](http://upload-images.jianshu.io/upload_images/4898000-e9ed5d4fb617a2f3.jpg)
    
5. 下一步，继续修改 WeChat 内的 Watch 中 WeChatWatchNative 中 info.plist 文件， 4.jpg
    
    [![](http://upload-images.jianshu.io/upload_images/4898000-f7401c0ce86f5b5f.jpg)](http://upload-images.jianshu.io/upload_images/4898000-f7401c0ce86f5b5f.jpg)
    
    如果不修改你可能会遇到一下报错：
    

```Plain
Error 0xe80000d5: The WatchKit app's Info.plist must have a WKCompanionAppBundleIdentifier key set to the bundle identifier of the companion app. AMDeviceSecureInstallApplication(0, device, url, options, install_callback, 0)
```

这个 WeChatWatchNative 的所有 info.plist 文件中的 bundle id 的前缀也需要和主应用的 bundle id 保存一直。打开 WeChatWatchNative 找到 info.plist 文件，修改里面的 bundle id，此文件需要修改 2 处，如下图：

[![](http://upload-images.jianshu.io/upload_images/4898000-71db7d028545a99f.jpg)](http://upload-images.jianshu.io/upload_images/4898000-71db7d028545a99f.jpg)

5.jpg

1. 下面还要修改 WeChatWatchNative 中的 PlugIns 文件夹下的插件 WeChatWatchNativeExtension.appex 的 info.plist 文件，

[![](http://upload-images.jianshu.io/upload_images/4898000-e14e16903bc0ee8d.jpg)](http://upload-images.jianshu.io/upload_images/4898000-e14e16903bc0ee8d.jpg)

6.jpg

打开文件 WeChatWatchNativeExtension.appex 文件，找到 info.plist 文件，修改如下图：

[![](http://upload-images.jianshu.io/upload_images/4898000-7b7ec0b4e6a3b960.jpg)](http://upload-images.jianshu.io/upload_images/4898000-7b7ec0b4e6a3b960.jpg)

7.jpg

1. 至此所有 bunlde id 修改完毕，然后进行压缩成 ipa 包。

```Plain
zip -qr WeChat.ipa Payload/ iTunesArtwork
```

1. 再把压缩成的 ipa 进行重签名，就可以安装到手机上使用了。（重签名需要了解的私信联系，笔者有空闲时间会再聊聊重签名）

```Plain
可以打开终端使用此命令安装,可以查看报错信息
ios-deploy -b wechat.ipa
```