> 本文由 简悦 SimpRead 转码

由 deb 文件得到 dylib 库后，将 dylib 库注入到二进制文件中，重新打包完成动态库附带的功能。

### 1. 获得 dylib 文件

使用 theos 建立 tweak 工程后，hook 住要改写的函数，之后编译、打包（make、make package）生成 xxxx.deb 文件，deb 文件是可以直接在越狱手机安装的。  
将该 deb 文件后缀改为. zip 文件，使用 Keka（自带的没测过）解压，解压几次后，会出现文件夹 Library/MobileSubstrate/DynamicLibraries，里面有 xxx.dylib 文件。  

### 2. 查看 dylib 文件的依赖项

使用 MAC 自带 otool 工具查看，笔者的依赖路径如下，命令为：

```Plain
otool -L /xx/xx/xxx.dylib
```

[![](http://upload-images.jianshu.io/upload_images/860988-f615cafebc734eca.png)](http://upload-images.jianshu.io/upload_images/860988-f615cafebc734eca.png)

屏幕快照 2017-04-06 下午 2.22.05.png

从图中可以看出除了 CydiaSubstrate 库，其他的都是系统自带的库。CydiaSubstrate 为越狱手机中的库文件，其在越狱手机中的路径为 / Library/Frameworks/CydiaSubstrate.framework/CydiaSubstrate，或直接通过 SSH 连接到手机搜索，命令为

```Plain
find  / -iname "CydiaSubstrate"  //搜索CydiaSubstrate
```

把 CydiaSubstrate 拷贝到电脑上，重命名为 libsubstrate.dylib

### 3. 移动 libsubstrate.dylib、xxxx.dylib 文件到 xxx.app 中

将要破解的 ipa 文件改为 zip 文件解压后，把 libsubstrate.dylib、xxxx.dylib 移动到 xxx.app 中

### 4. 修改 xxxx.dylib 文件依赖

```Plain
//loader_path固定字符串，不能更改
install_name_tool -change /Library/Frameworks/CydiaSubstrate.framework/CydiaSubstrate @loader_path/libsubstrate.dylib xxxx.dylib
```

### 5. 再次查看 xxx.app 目录下的 xxx.dylib 文件依赖项

[![](http://upload-images.jianshu.io/upload_images/860988-644cfe3241e4b2cd.png)](http://upload-images.jianshu.io/upload_images/860988-644cfe3241e4b2cd.png)

屏幕快照 2017-04-06 下午 2.33.59.png

从图中可以看出依赖项路径已被修改

### 6. 将 dylib 注入到二进制文件中

optool 工具地址：[https://github.com/alexzielenski/optool](https://github.com/alexzielenski/optool)  
直接下载是编译不过的，还要下载 ArgumentParser，地址为：  
[https://github.com/mysteriouspants/ArgumentParser](https://github.com/mysteriouspants/ArgumentParser)  
把 ArgumentParser 文件导入到 optool 工程中，编译后生成 optool 工具，之后使用 optool 工具将 dylib 文件注入到二进制文件中（可直接下载我的工程，  
[https://github.com/hzpqt/optool-](https://github.com/hzpqt/optool-)）

```Plain
./optool install -c load -p "@executable_path/xxx.dylib" -t /xxx.app/xxx   //executable_path为固定字符，不能更改
```

如果顺利的话，终端应该会输出：

[![](http://upload-images.jianshu.io/upload_images/860988-79f42ef0d0c3347d.png)](http://upload-images.jianshu.io/upload_images/860988-79f42ef0d0c3347d.png)

屏幕快照 2017-04-06 下午 2.48.53.png

### 7. 重新签名打包

笔者使用的工具是 iOS App Signer，选择好证书、授权文件后，开始打包

[![](http://upload-images.jianshu.io/upload_images/860988-89d8bf9d03af040f.png)](http://upload-images.jianshu.io/upload_images/860988-89d8bf9d03af040f.png)

屏幕快照 2017-04-06 下午 2.52.39.png

### 8. 安装 xxx.ipa 文件

[![](http://upload-images.jianshu.io/upload_images/860988-044b7b4c3d200811.png)](http://upload-images.jianshu.io/upload_images/860988-044b7b4c3d200811.png)

屏幕快照 2017-04-06 下午 2.55.00.png

如果安装成功后，点击打开出现闪退，估计就是以上路径配置有问题，可以导出崩溃日志看看。