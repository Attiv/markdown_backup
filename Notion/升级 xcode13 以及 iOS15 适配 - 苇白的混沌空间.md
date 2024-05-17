> 升级了 xcode13 之后，就不得不面对 iOS15 适配的问题。

升级了 xcode13 之后，就不得不面对 iOS15 适配的问题。收集了市面上常见的坑，以及自己遇到的坑做个记录。

## iOS 15.0 适配

### TableView 适配

苹果在 UITableView 新增 sectionHeaderTopPadding API

```Plain
@property (nonatomic) CGFloat sectionHeaderTopPadding API_AVAILABLE(ios(15.0), tvos(15.0), watchos(8.0));
```

根据注释，这个 TopPadding 是应用于每个 SectionHeader 之上，如果不管他的话，工程中在每个 section header 之上都会出现一块空白的 margin。  
在 tableivew 的基类方法里头添加一下代码可以解决。  

```Plain
if (@available(iOS 15.0, *)) {
    _tableView.sectionHeaderTopPadding = 0;
}
```

### TabBar 适配 [(来自 coenen 简书)](https://www.jianshu.com/p/40c2675a5f49)

tabbar 背景颜色设置失效，字体设置失效，阴影设置失效问题  
背景色设置失效，需要用 UITabBarAppearance 来设置  

```Plain
if (@available(iOS 13.0, *)) {
    UITabBarAppearance * appearance = [[UITabBarAppearance alloc] init];

    appearance.backgroundColor = [UIColor whiteColor];
    self.tabBar.standardAppearance = appearance;
    if (@available(iOS 15.0, *)) {
        self.tabBar.scrollEdgeAppearance = appearance;
    }
}
```

### 导航栏适配 [(来自 coenen 简书)](https://www.jianshu.com/p/40c2675a5f49)

iOS 15 中，导航栏的问题比较明显，调试之后发现是 UINavigationBar 部分属性的设置在 iOS 15 上是无效的，查看导航栏特性 API，苹果对导航栏的性能做了优化，默认情况下，如果导航栏与视图没有折叠，导航栏的背景透明，如果系统检测到有重叠的话，会变成毛玻璃的效果。  
note：UINavigationBarAppearance 是 iOS 13 更新的 API，  
  
iOS 15 navigationBar 的相关属性设置要通过实例 UINavigationBarAppearance 来实现。  
  
在 iOS 13 UINavigationBar 新增了 scrollEdgeAppearance 属性，但在 iOS 14 及更早的版本中此属性只应用在大标题导航栏上。在 iOS 15 中此属性适用于所有导航栏。  

```Plain
if (@available(iOS 13.0, *)) {
    UINavigationBarAppearance *appearance = [[UINavigationBarAppearance alloc] init];
    [appearance setBackgroundColor:[UIColor pageBackgroundColor]];
    [appearance setBackgroundImage:[self imageWithColor:[UIColor pageBackgroundColor]]];
    [appearance setShadowImage:[self imageWithColor:[UIColor pageBackgroundColor]]];
    appearance.titleTextAttributes = @{NSFontAttributeName:[UIFont systemFontOfSize:18.0f weight:UIFontWeightSemibold],NSForegroundColorAttributeName: [UIColor blackColor]};
    [[UINavigationBar appearance] setScrollEdgeAppearance: appearance];
    [[UINavigationBar appearance] setStandardAppearance:appearance];
}
```

### UISheetPresentationController [(来自 YungFan 的掘金文章)](https://juejin.cn/post/6987960384397262879)

增加 UISheetPresentationController，通过它可以控制 Modal 出来的 UIViewController 的显示大小，且可以通过拖拽手势在不同大小之间进行切换。只需要在跳转的目标 UIViewController 做如下处理：

```Plain
if let presentationController = presentationController as? UISheetPresentationController {

       presentationController.detents = [.medium(), .large()]

       presentationController.prefersGrabberVisible = true
}
```

### URLSession 推出支持 async/await 的 API，包括获取数据、上传与下载。[(来自 YungFan 的掘金文章)](https://juejin.cn/post/6987960384397262879)

```Plain
let session = URLSession.shared

let (data, response) = try await session.data(from: url)

let (localURL, _) = try await session.download(from: url)

let (_, response) = try await session.upload(for: request, from: data)
```

### UIButton 支持更多配置 [(来自 YungFan 的掘金文章)](https://juejin.cn/post/6987960384397262879)

```Plain
let plain = UIButton(configuration: .plain(), primaryAction: nil)
plain.setTitle("Plain", for: .normal)

let gray = UIButton(configuration: .gray(), primaryAction: nil)
gray.setTitle("Gray", for: .normal)

let tinted = UIButton(configuration: .tinted(), primaryAction: nil)
tinted.setTitle("Tinted", for: .normal)

let filled = UIButton(configuration: .filled(), primaryAction: nil)
filled.setTitle("Filled", for: .normal)
```

### UIImage 新增了几个调整尺寸的方法 [(来自 YungFan 的掘金文章)](https://juejin.cn/post/6987960384397262879)

```Plain
UIImage(named: "sv.png")?.preparingThumbnail(of: CGSize(width: 200, height: 100))

UIImage(named: "sv.png")?.prepareThumbnail(of: CGSize(width: 200, height: 100)) { image in

}

await UIImage(named: "sv.png")?.byPreparingThumbnail(ofSize: CGSize(width: 100, height: 100))
```

## Xcode 13

### 卡顿问题

升级完 Xcode13 之后，小伙伴们都遇到了运行或者编译卡死的问题，本以为是 13.0 的问题，于是升级了 13.1，但是 13.1 仍然有这个问题。  
仔细观察了编译过程，由于新版 Xcode13 指定使用新编译系统，而新编译系统加入了 nullbility 的检查，我们的工程在编译过程中出现了大量的 warning（几万个），于是猜测是不是由于 warning 太多引起 Xcode 卡顿，点击 warning list，Xcode 直接卡死。所以正是因为 warning 太多导致。发现了问题之后就好解决了。  

1. 针对于主工程，在主工程的 build setting 中找到 Other Warning Flags 添加`$(inherited) -Wno-nullability-completeness -Wno-unused-parameter`可以忽略主工程的 warning
    
    [![](https://i.loli.net/2021/11/18/gyJNTHKdlVYq9rE.png)](https://i.loli.net/2021/11/18/gyJNTHKdlVYq9rE.png)
    
2. 针对 pods 工程，在 podfile 中加入`inhibit_all_warnings!`忽略 pods 工程中的警告。

这两步做完之后，直接把 warning 从 4 万多个减少到 1000 个左右。这 1000 多个是由于 swift 混编引起的 warning，目前搜了全网没有找到很好的解决办法。