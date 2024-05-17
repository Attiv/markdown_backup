# iOS逆向 <MonkeyDev 笔记>

[![](https://www.notion.soiOS%E9%80%86%E5%90%91%20%3CMonkeyDev%20%E7%AC%94%E8%AE%B0%3E.resources/96)](https://www.notion.soiOS%E9%80%86%E5%90%91%20%3CMonkeyDev%20%E7%AC%94%E8%AE%B0%3E.resources/96)

[farmerly](https://www.jianshu.com/u/0c4811039261)

__

关注

2018.10.08 11:43 字数 101 阅读 154评论 0喜欢 0

### **CaptainHook**

假如class-dump后找到了头文件，并且知道了属性和方法  
例如拿到的方法如下所示(此方法不在文件中，存在与ipa包中):  

```Plain
CustomViewController ：UIViewController
@property (nonatomic, copy) NSString* newProperty;
+ (void)classMethod;
- (NSString*)getMyName;
- (void)newMethod:(NSString*) output;
```

- CHDeclareClass 申明类可以调用属性和方法

```Plain
CHDeclareClass(CustomViewController)
```

- 进行对方法和属性的调用（请仔细阅读class-dump中的属性和方法，以下是如何调用）

```Plain
//方法已经明确写出了传什么
# optimization  当前self或者其他
\#return_type  需要传入什么类型
\#class_type  传入哪一个类
\#name  属性名称
CHOptimizedMethod0(<\#optimization#>, <\#return_type#>, <\#class_type#>, <\#name#>)

CHOptimizedMethod0(self, NSString*, CustomViewController, getMyName){
//需要实现的代码
}
CHDeclareMethod1(void, CustomViewController, newMethod, NSString*, output){
//需要实现的代码
}
CHOptimizedClassMethod0(self, void, CustomViewController, classMethod){
//需要实现的代码
}
CHOptimizedMethod(0, self,  NSString*, CustomViewController, newProperty) 
{  
//需要实现的代码
}
//需要实现的代码就是，你对以上传入属性值进行修改的，需要返回就returen，不需要则调用父类，或者直接不做任何操作
```

```Plain
//添加新的属性
CHPropertyRetainNonatomic(CustomViewController, NSString*, 
newProperty, setNewProperty);
```

- 构造函数(CHConstructor)

```Plain
CHConstructor{
//装载类
    CHLoadLateClass(CustomViewController);
//类名称 类方法
    CHClassHook0(CustomViewController, getMyName);
    CHClassHook0(CustomViewController, classMethod);
//类名称 属性
    CHHook0(CustomViewController, newProperty);
    CHHook1(CustomViewController, setNewProperty);
}
```