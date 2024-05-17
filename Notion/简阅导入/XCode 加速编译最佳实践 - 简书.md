> 前言：近期对 XCode 加速编译做了一些研究，对网上的加快 XCode 编译速度的方法进行了总结，同时自己也举一反三写了个脚本优化提速，我想这篇文章应该是你看到的最全的 XCode 加速编译的解决方案。

## 0x00 将 Debug Information Format 改为 DWARF

在 project 相应 Target 的 Build Settings 中，找到 Debug Information Format 这一项，将 Debug 时的 DWARF with dSYM file 改为 DWARF。

[![](http://upload-images.jianshu.io/upload_images/11452136-4e4eea0caffb4454.png)](http://upload-images.jianshu.io/upload_images/11452136-4e4eea0caffb4454.png)

设置 DWARF

> 注意：dSYM 文件是保存 16 进制函数地址映射信息的中转文件，我们调试的 symbols 都会包含在这个文件中，如果你在调试过程中发现函数堆栈无法显示，或者你需要使用 Profile 工具分析 app，你可能需要重新开启 Debug 为 DWARF with dSYM file。

## 0x01 将 Build Active Architecture Only 改为 Yes

在 project 相应 Target 的 Build Settings 中，找到 Build Active Architecture Only 这一项，将 Debug 时的 No 改为 Yes。

[![](http://upload-images.jianshu.io/upload_images/11452136-14e83d804ba2314d.png)](http://upload-images.jianshu.io/upload_images/11452136-14e83d804ba2314d.png)

将 Build Active Architecture Only 改为 Yes

这一项设置的是是否仅编译当前架构的版本号，假设为 No，会编译全部架构的版本号。须要注意的是，此选项在 Release 模式下必须为 No。否则公布的 ipa 在部分设备上将不能执行。

## 0x02 增加 XCode 执行的线程数

可以根据自己 Mac 的性能，更改线程数设置 5：

```Plain
defaults write com.apple.Xcode PBXNumberOfParallelBuildSubtasks 5
```

另外也有一个设置可以开启：

```Plain
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES
```

XCode 默认使用与 CPU 核数相同的线程来进行编译，但由于编译过程中的 IO 操作往往比 CPU 运算要多，因此适当的提升线程数可以在一定程度上加快编译速度。

至此，你可能觉得与网上搜到的有关 XCode 加速编译的文章并无不同，不过，精彩的往往在后面，**下面让我隆重介绍一个独特的方案：**

## 0x03 优化 Copy Pod Resources

如果你的项目使用了 CocoaPod, 并且项目中使用 CocoaPod 引用了很多第三方库，以及公司项目也是以组件的形式通过 CocoaPod 进行组件化拆分。那么你一定会遇到和我一样的问题，那就是 Copy Pod Resources 花费大量的时间：

[![](http://upload-images.jianshu.io/upload_images/11452136-cbec8404168c09a3.png)](http://upload-images.jianshu.io/upload_images/11452136-cbec8404168c09a3.png)

Copy Pod Resources 花费时间

上图是一个中等大小的项目，可以看到 Build 的时间总共耗时 42.5s，而 Copy Pod Resources 却花费了 34.3s，可见优化 Copy Pods Resources 带来的收益是相当可观的。

我们知道 Copy Pods Resources 是用于将 pod 库中的资源文件拷贝到 app 目录下，因此如果文件越多越大，耗时自然就越长。更重要的是，Pod 下的资源文件，通常情况下，在我们 pod update 后，不会发生改变，如果每次 Build 都去 copy，实属浪费。因此我的解决方案是：

> 仅在 pod update 后，Build 才进行 copy resources 操作，避免每次 Build 都去 copy

**要达到此目的，你仅需要如下两步操作：**

1. 在工程的根目录下创建文件`copy_pod_resources_once.patch`并填入以下代码：

```Plain
set -e

# Add This To Copy Resource only once
NONCE_FILE="${TARGET_BUILD_DIR}/${UNLOCALIZED_RESOURCES_FOLDER_PATH}/../copyresources-done-\#Time#.nonce"
if [ -f "$NONCE_FILE" ]; then
    printf "$NONCE_FILE \n"
    printf "already copied resources"
    exit 0
else
    touch "$NONCE_FILE"
fi
```

1. 在 podfile 中加入如下代码，其中你需要把`YourProjectName`替换为你自己的工程名：

```Plain
post_install do |installer|
    copy_pods_resources_path = "Pods/Target Support Files/Pods-YourProjectName/Pods-YourProjectName-resources.sh"
    text = File.read(copy_pods_resources_path)
    string_onceCopy = File.read("copy_pod_resources_once.patch")
    string_time = Time.now.strftime("%Y%m%d%H%M%S")
    string_onceCopy = string_onceCopy.gsub("\#Time#", string_time)
    text = text.gsub("set -e", string_onceCopy)
    File.open(copy_pods_resources_path, "w") {|file| file.puts text}
end
```

重新 pod update 后，第一次 Build 时间不变，第二次 Build 的时间会大幅缩短：

[![](http://upload-images.jianshu.io/upload_images/11452136-8a8630561dea938a.png)](http://upload-images.jianshu.io/upload_images/11452136-8a8630561dea938a.png)

优化 Copy Pods Resources 后

上述方法是我参考[这里](https://stackoverflow.com/questions/20649298/xcode-custom-shell-scripts-are-slowing-down-the-compiling-time)举一反三得到的升级版，各位看官有兴趣不妨一试，如有问题欢迎私信或留言。当然你也可以使用如下配置达到类似效果：

[![](http://upload-images.jianshu.io/upload_images/11452136-d4b26a22864b5574.png)](http://upload-images.jianshu.io/upload_images/11452136-d4b26a22864b5574.png)

设置 Copy Pods Resources

不过，这个设置需要在之前已经 Build 成功后再勾选上，否则会出现资源没有 Copy 导致的 app 资源丢失，也有可能出现崩溃。

## 0x04 使用 CCache

> CCache 的原理是通过把项目的源文件用 ccache 编译器编译，然后缓存编译生成的信息，从而在下一次编译时，利用这个缓存加快编译的速度，目前支持的语言有：C、C++、Objective-C、Objective-C++，但是如果找不到 ccache 编译器，那么还是会选择 clang 编译器来编译源文件。  
> CCache 的使用方法这里不再赘述，配置有些许麻烦，但是如果你的项目代码量较大，效果还是很显著的，您可以参考这边文章： ccache - 让 Xcode 编译速度飞起来  

上述的每一个方法或多或少都会带来副作用，大家在使用时需要根据项目的实际情况酌情选择，最后对上述所有方法做一个汇总：

|方案|原理|加速效果|使用场景|
|---|---|---|---|
|[[将 Debug Information Format 改为 DWARF]]|修改 XCode 配置，不生成 dSYM 文件|✨✨✨|所有|
|[[将 Build Active Architecture Only 改为 Yes]]|修改 XCode 配置，仅编译当前架构|✨✨|所有|
|[[增加 XCode 执行的线程数]]|修改 XCode 配置，利用 CPU 多核|✨|所有|
|[[优化 Copy Pod Resources]]|针对资源，优化 Copy Pods Resources|✨✨✨✨|pod 库资源文件较多、较大|
|[[使用 CCache]]|针对代码，缓存编译信息|✨✨✨✨|源文件较多|

  
  

> 本文由简悦 SimpRead 转码