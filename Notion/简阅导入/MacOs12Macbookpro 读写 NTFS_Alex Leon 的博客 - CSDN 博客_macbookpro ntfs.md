新买了 Macbook Pro M1 Pro，系统是 macOS 12.0，默认可以 NTFS 格式的读移动硬盘（U 盘），但是不能写

```Plain
brew install ntfs-3g
```

出现下列错误：

```Plain
Error: ntfs-3g has been disabled because it requires FUSE!
```

正确的安装方法如下：

```Plain
brew tap gromgit/homebrew-fuse
brew install --cask macfuse
brew install ntfs-3g-mac
```

如何使用呢？

```Plain
diskutil list
//找到需要挂载的移动硬盘
sudo /System/Volumes/Data/opt/homebrew/bin/ntfs-3g /dev/disk6s1 /Volumes/NTFS -olocal -oallow_other -o auto_xattr
```

注意：需要安全权限，并重启机器。  
可以读写移动硬盘了！  

> 参考原文链接：https://blog.csdn.net/Ericohe/article/details/121595911 本文由简悦 SimpRead 转码