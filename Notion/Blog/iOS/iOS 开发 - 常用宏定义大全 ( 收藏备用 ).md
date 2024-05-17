在工作中, 很多小伙伴都会在PCH文件定义一些常用的宏，但是又怕写这些简单的宏浪费时间，又有时候忘记怎么定义了怎么办？本人在工作中也是如此。所以在这里给大家分享一些常用的宏定义，喜欢的小伙伴可以直接在项目中使用（持续更新）！

为了大家使用方便，请到GitHub - 宏定义头文件下载 ！

**GitHub地址：**

[https://github.com/luran2358/LRMacroDefinition](https://github.com/luran2358/LRMacroDefinition)

# 1获取屏幕宽度与高度

\#define SCREEN_WIDTH [UIScreen mainScreen].bounds.size.width

\#define SCREENH_HEIGHT [UIScreen mainScreen].bounds.size.height

根据一个网友(脱离语言)提醒, 如果**支持横屏**可以用下面的宏:

\#if __IPHONE_OS_VERSION_MAX_ALLOWED >= 80000 // 当前Xcode支持iOS8及以上

\#define SCREEN_WIDTH ([[UIScreen mainScreen] respondsToSelector:@selector(nativeBounds)]?[UIScreen mainScreen].nativeBounds.size.width/[UIScreen mainScreen].nativeScale:[UIScreen mainScreen].bounds.size.width)

\#define SCREENH_HEIGHT ([[UIScreen mainScreen] respondsToSelector:@selector(nativeBounds)]?[UIScreen mainScreen].nativeBounds.size.height/[UIScreen mainScreen].nativeScale:[UIScreen mainScreen].bounds.size.height)

\#define SCREEN_SIZE ([[UIScreen mainScreen] respondsToSelector:@selector(nativeBounds)]?CGSizeMake([UIScreen mainScreen].nativeBounds.size.width/[UIScreen mainScreen].nativeScale,[UIScreen mainScreen].nativeBounds.size.height/[UIScreen mainScreen].nativeScale):[UIScreen mainScreen].bounds.size)

\#else

\#define SCREEN_WIDTH [UIScreen mainScreen].bounds.size.width

\#define SCREENH_HEIGHT [UIScreen mainScreen].bounds.size.height

\#define SCREEN_SIZE [UIScreen mainScreen].bounds.size

\#endif

# 2获取通知中心

\#define LRNotificationCenter [NSNotificationCenter defaultCenter]

# 3设置随机颜色

\#define LRRandomColor [UIColor colorWithRed:arc4random_uniform(256)/255.0 green:arc4random_uniform(256)/255.0 blue:arc4random_uniform(256)/255.0 alpha:1.0]

# 4设置RGB颜色/设置RGBA颜色

\#define LRRGBColor(r, g, b) [UIColor colorWithRed:(r)/255.0 green:(g)/255.0 blue:(b)/255.0 alpha:1.0]

\#define LRRGBAColor(r, g, b, a) [UIColor colorWithRed:(r)/255.0 green:(r)/255.0 blue:(r)/255.0 alpha:a]

// clear背景颜色

\#define LRClearColor [UIColor clearColor]

# 5自定义高效率的 NSLog

项目开发中，我们会在许多地方加上Log，但是发布的时候又不想用这些Log，我们也不可能一个一个的删除，所以自定义Log是必然的！

\#ifdef DEBUG

\#define LRLog(...) NSLog(@"%s 第%d行 \n %@\n\n",__func__,__LINE__,[NSString stringWithFormat:__VA_ARGS__])

\#else

\#define LRLog(...)

\#endif

# 6弱引用/强引用

\#define LRWeakSelf(type) __weak typeof(type) weak#\#type = type;

\#define LRStrongSelf(type) __strong typeof(type) type = weak#\#type;

# 7设置 view 圆角和边框

\#define LRViewBorderRadius(View, Radius, Width, Color)\

\

[View.layer setCornerRadius:(Radius)];\

[View.layer setMasksToBounds:YES];\

[View.layer setBorderWidth:(Width)];\

[View.layer setBorderColor:[Color CGColor]]

# 8由角度转换弧度 由弧度转换角度

\#define LRDegreesToRadian(x) (M_PI * (x) / 180.0)

\#define LRRadianToDegrees(radian) (radian*180.0)/(M_PI)

# 9设置加载提示框（第三方框架：Toast）

此宏定义非常好用，但是小伙伴需要CocoaPods导入第三方框架：Toast( [https://github.com/scalessec/Toast](https://github.com/scalessec/Toast) )

**使用方法如下：**

LRToast(@"网络加载失败");

\#define LRToast(str) CSToastStyle *style = [[CSToastStyle alloc] initWithDefaultStyle]; \

[kWindow makeToast:str duration:0.6 position:CSToastPositionCenter style:style];\

kWindow.userInteractionEnabled = NO; \

dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(0.6 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{\

kWindow.userInteractionEnabled = YES;\

});\

# 10设置加载提示框（第三方框架：MBProgressHUD）

此宏定义同上一个类似，如下图：

// 加载

\#define kShowNetworkActivityIndicator() [UIApplication sharedApplication].networkActivityIndicatorVisible = YES

// 收起加载

\#define HideNetworkActivityIndicator() [UIApplication sharedApplication].networkActivityIndicatorVisible = NO

// 设置加载

\#define NetworkActivityIndicatorVisible(x) [UIApplication sharedApplication].networkActivityIndicatorVisible = x

\#define kWindow [UIApplication sharedApplication].keyWindow

\#define kBackView for (UIView *item in kWindow.subviews) { \

if(item.tag == 10000) \

{ \

[item removeFromSuperview]; \

UIView * aView = [[UIView alloc] init]; \

aView.frame = [UIScreen mainScreen].bounds; \

aView.tag = 10000; \

aView.backgroundColor = [[UIColor blackColor] colorWithAlphaComponent:0.3]; \

[kWindow addSubview:aView]; \

} \

} \

\#define kShowHUDAndActivity kBackView;[MBProgressHUD showHUDAddedTo:kWindow animated:YES];kShowNetworkActivityIndicator()

\#define kHiddenHUD [MBProgressHUD hideAllHUDsForView:kWindow animated:YES]

\#define kRemoveBackView for (UIView *item in kWindow.subviews) { \

if(item.tag == 10000) \

{ \

[UIView animateWithDuration:0.4 animations:^{ \

item.alpha = 0.0; \

} completion:^(BOOL finished) { \

[item removeFromSuperview]; \

}]; \

} \

} \

\#define kHiddenHUDAndAvtivity kRemoveBackView;kHiddenHUD;HideNetworkActivityIndicator()

# 11获取view的frame/图片资源

//获取view的frame（不建议使用）

//\#define kGetViewWidth(view) view.frame.size.width

//\#define kGetViewHeight(view) view.frame.size.height

//\#define kGetViewX(view) view.frame.origin.x

//\#define kGetViewY(view) view.frame.origin.y

//获取图片资源

\#define kGetImage(imageName) [UIImage imageNamed:[NSString stringWithFormat:@"%@",imageName]]

# 12获取当前语言

\#define LRCurrentLanguage ([[NSLocale preferredLanguages] objectAtIndex:0])

# 13使用 ARC 和 MRC

\#if __has_feature(objc_arc)

// ARC

\#else

// MRC

\#endif

# 14判断当前的iPhone设备/系统版本

//判断是否为iPhone

\#define IS_IPHONE (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPhone)

//判断是否为iPad

\#define IS_IPAD (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad)

//判断是否为ipod

\#define IS_IPOD ([[[UIDevice currentDevice] model] isEqualToString:@"iPod touch"])

// 判断是否为 iPhone 5SE

\#define iPhone5SE [[UIScreen mainScreen] bounds].size.width == 320.0f && [[UIScreen mainScreen] bounds].size.height == 568.0f

// 判断是否为iPhone 6/6s

\#define iPhone6_6s [[UIScreen mainScreen] bounds].size.width == 375.0f && [[UIScreen mainScreen] bounds].size.height == 667.0f

// 判断是否为iPhone 6Plus/6sPlus

\#define iPhone6Plus_6sPlus [[UIScreen mainScreen] bounds].size.width == 414.0f && [[UIScreen mainScreen] bounds].size.height == 736.0f

//获取系统版本

\#define IOS_SYSTEM_VERSION [[[UIDevice currentDevice] systemVersion] floatValue]

//判断 iOS 8 或更高的系统版本

\#define IOS_VERSION_8_OR_LATER (([[[UIDevice currentDevice] systemVersion] floatValue] >=8.0)? (YES):(NO))

# 15判断是真机还是模拟器

\#if TARGET_OS_IPHONE

//iPhone Device

\#endif

\#if TARGET_IPHONE_SIMULATOR

//iPhone Simulator

\#endif

# 16沙盒目录文件

//获取temp

\#define kPathTemp NSTemporaryDirectory()

//获取沙盒 Document

\#define kPathDocument [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject]

//获取沙盒 Cache

\#define kPathCache [NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) firstObject]

# 17GCD 的宏定义

很多小伙伴都非常烦写GCD的方法，所以在此定义为宏使用更加方便简洁！如下图：

//GCD - 一次性执行

\#define kDISPATCH_ONCE_BLOCK(onceBlock) static dispatch_once_t onceToken; dispatch_once(&onceToken, onceBlock);

//GCD - 在Main线程上运行

\#define kDISPATCH_MAIN_THREAD(mainQueueBlock) dispatch_async(dispatch_get_main_queue(), mainQueueBlock);

//GCD - 开启异步线程

\#define kDISPATCH_GLOBAL_QUEUE_DEFAULT(globalQueueBlock) dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), globalQueueBlocl);

# 宏与const 的使用

很多小伙伴在定义一个常量字符串，都会定义成一个宏，最典型的例子就是服务器的地址。在此所有用宏定义常量字符的小伙伴以后就用const来定义吧！为什么呢 ？我们看看：

- **宏的用法：** 一般字符串抽成宏，代码抽成宏使用。
- **const用法：**一般常用的字符串定义成const（对于常量字符串苹果推荐我们使用const）。
- **宏与const区别：**

1. 编译时刻不同，宏属于预编译 ，const属于编译时刻
2. 宏能定义代码，const不能，多个宏对于编译会相对时间较长，影响开发效率，调试过慢，const只会编译一次，缩短编译时间。
3. 宏不会检查错误，const会检查错误

通过以上对比，我们以后在开发中如果定义一个常量字符串就用const，定义代码就用宏。我们来看看如何使用const，列举实际项目使用方法如下图：

在上图本人只是简单定义几个常量字符串，我们创建一个类只要在.h和.m中包含\#import <Foundation/Foundation.h>就可以，然后再.h文件声明一个字符串，在.m中实现就可以了，最后把这个类导入PCH文件中，我们就可任意的发挥啦！

有意思啊

**还要错过关注我?**

**长按二维码**

关注的不仅仅是技术