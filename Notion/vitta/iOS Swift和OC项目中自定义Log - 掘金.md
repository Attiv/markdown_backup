[zhf_Zachariah](https://juejin.im/user/5a3116cb5188253d681794f5)

2017年12月13日阅读 60

# iOS Swift和OC项目中自定义Log

> 通常在实际项目中，为了检测代码逻辑的实现是否正确，我们可能会在需要的地方进行数据打印来验证。在调试阶段我们可以这么做，但是项目发布之后还要一个一个注释掉么？想想都觉得累，那么问题来了，有没有一种方法能够让打印在Debug阶段正常打印，在Release阶段就自动“消失”呢？

- OC中的自定义Log

> 废话不多说，看代码 = = 当然名字你可以随便起，只要你认识 = =

```Plain
/***调试状态（BUG）****/
\#ifdef DEBUG
\#define ZZLog(...) NSLog(__VA_ARGS__)   //调试状态NSLog 就变为ZZLog输出
\#else
\#define ZZLog(...)                      //非调试状态输出ZZLog为空
\#endif
复制代码
```

> OC中的自定义Log就是这么简单，至少我是这么做的 = =

- Swift中的自定义Log

> 看过OC中的自定义Log,你可能觉得swift中也是这么简单，那就错了，不得不说swift的路子还是野。。。首先呢OC中的自定义Log我们写成了宏定义，会放在.h或者.pch文件中。那么问题来了，swift中没有宏定义这么一说啊，该怎么办呢？

为了解决这个问题，我们把自定义Log写成一个全局函数，像这样--

```Plain
import UIKit

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?


    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
        // Override point for customization after application launch.
        return true
    }

    func applicationWillResignActive(application: UIApplication) {
        // Sent when the application is about to move from active to inactive state. This can occur for certain types of temporary interruptions (such as an incoming phone call or SMS message) or when the user quits the application and it begins the transition to the background state.
        // Use this method to pause ongoing tasks, disable timers, and throttle down OpenGL ES frame rates. Games should use this method to pause the game.
    }

    func applicationDidEnterBackground(application: UIApplication) {
        // Use this method to release shared resources, save user data, invalidate timers, and store enough application state information to restore your application to its current state in case it is terminated later.
        // If your application supports background execution, this method is called instead of applicationWillTerminate: when the user quits.
    }

    func applicationWillEnterForeground(application: UIApplication) {
        // Called as part of the transition from the background to the inactive state; here you can undo many of the changes made on entering the background.
    }

    func applicationDidBecomeActive(application: UIApplication) {
        // Restart any tasks that were paused (or not yet started) while the application was inactive. If the application was previously in the background, optionally refresh the user interface.
    }

    func applicationWillTerminate(application: UIApplication) {
        // Called when the application is about to terminate. Save data if appropriate. See also applicationDidEnterBackground:.
    }
}


//这个位置呢就是写全局函数的地方，因为程序生命周期的原因一般写在AppDelegate里边
//全局函数 - 只要不写成某个类里边的方法 - 最好写在APPDelegate里边
func test(){
    //代码段
}

//写的不对，请提出意见，要不你来打我呀？ = =
复制代码
```

解决了这个问题我们再来看看自定义Log

> swift中的打印格式就是这么任性，除了结果什么都木有。。。

[![](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240)](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240)

> 为了打印看到的信息更加的清楚，我们这儿样做

```Plain
//获取打印所在的文件
 let file = (\#file as NSString).lastPathComponent
 print("\(file): -test")
复制代码
```

[![](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_1)](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_1)

```Plain
//获取打印所在的方法
 print("\(\#function): -test")
复制代码
```

[![](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_5)](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_5)

```Plain
//获取打印所在的行数
print("\(\#line): -test")
复制代码
```

[![](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_2)](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_2)

> 为了方便起见，把他们仨拼接起来.这样就可以清晰的看到我们所需要打印数据的地方

```Plain
print("\((\#file as NSString).lastPathComponent):[\(#function)](\(#line)) -zhf")
复制代码
```

[![](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_3)](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_3)

> 接下来重要的一步是设置Other Swift Flags

[![](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_4)](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_4)

> 结合全局函数的书写，我们就可以完成自定义Log了

```Plain
// MARK: - 注释>自定义Log
func ZHFLog<T>(message : T,file : String = \#file,funcName : String = \#function,lineNum : Int = \#line) {
    
    \#if DEBUG  //设置完成后就可以了
        
    let fileName = (file as NSString).lastPathComponent
        
    print("\(fileName):[\(funcName)](\(lineNum)) -\(message)")
        
    \#endif
}
复制代码
```

> 在上面的方法中我们添加了一个message的参数，主要是为了适应多格式的参数输入

> 测试下 - -,在Debug环境下，打印出了我们想要的结果；在release环境下，则不打印。

[![](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_6)](https://www.notion.soiOS%20Swift%E5%92%8COC%E9%A1%B9%E7%9B%AE%E4%B8%AD%E8%87%AA%E5%AE%9A%E4%B9%89Log%20-%20%E6%8E%98%E9%87%91.resources/1240_6)

> 再补充下swift的注释该怎么写

```Plain
1.// MARK: 
2.///
这种格式的注释，在写代码时会有注释提示
3.使用VVDocuments注释
复制代码
```