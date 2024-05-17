# 解决Xcode9 Swift4下Cocoapods编译Swift第三方时报错

随着Xcode9 Swift4 的到来，一些小问题也接踵而至。许多优秀的Swift第三方框架还未来得及迎接Swift4的到来，它们还停留在swift3.x的状态，这个时候新建一个项目，使用cocoapods写上需要使用的第三方，一编译就是满屏红，如下图。

[1_1](https://www.notion.so%E8%A7%A3%E5%86%B3Xcode9%20Swift4%E4%B8%8BCocoapods%E7%BC%96%E8%AF%91Swift%E7%AC%AC%E4%B8%89%E6%96%B9%E6%97%B6%E6%8A%A5%E9%94%99%20-%20%E6%8E%98%E9%87%91.resources/1_1)

所幸，苹果每次升级Xcode都会保留上个版本的swift，以防暴乱~~

有两种解决方案 其本质都是控制编译时所使用的Swift版本

# 第一种：Xcode

Pods -> Targets -> SnapKit -> Build Settings -> Swift language version option 选择 Swift 3.2。不推荐使用该方法，一个个点效率有些低~~

[1_2](https://www.notion.so%E8%A7%A3%E5%86%B3Xcode9%20Swift4%E4%B8%8BCocoapods%E7%BC%96%E8%AF%91Swift%E7%AC%AC%E4%B8%89%E6%96%B9%E6%97%B6%E6%8A%A5%E9%94%99%20-%20%E6%8E%98%E9%87%91.resources/1_2)

# 第二种：使用Cocoapods控制

打开Podfile文件，添加并按需要修改下方代码来指定哪些第三方的Swift编译版本，接着来一次

```Plain
pod install
复制代码
```

最后再来一下编译就搞定了

```Plain
post_install do |installer|
    # 需要指定编译版本的第三方的名称
    myTargets = ['ObjectMapper', 'SnapKit']
    
    installer.pods_project.targets.each do |target|
        if myTargets.include? target.name
            target.build_configurations.each do |config|
                config.build_settings['SWIFT_VERSION'] = '3.2'
            end
        end
    end
end
复制代码
```

位置如图所示

[1](https://www.notion.so%E8%A7%A3%E5%86%B3Xcode9%20Swift4%E4%B8%8BCocoapods%E7%BC%96%E8%AF%91Swift%E7%AC%AC%E4%B8%89%E6%96%B9%E6%97%B6%E6%8A%A5%E9%94%99%20-%20%E6%8E%98%E9%87%91.resources/1)

[1_3](https://www.notion.so%E8%A7%A3%E5%86%B3Xcode9%20Swift4%E4%B8%8BCocoapods%E7%BC%96%E8%AF%91Swift%E7%AC%AC%E4%B8%89%E6%96%B9%E6%97%B6%E6%8A%A5%E9%94%99%20-%20%E6%8E%98%E9%87%91.resources/1_3)

Measure

Measure