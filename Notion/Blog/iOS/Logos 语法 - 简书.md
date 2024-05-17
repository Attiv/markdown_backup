### // Tweak.xm

### 1. 预处理指令

### %hook

指定需要 hook 的 class，必须以 %end 结尾

```Plain
%hook SpringBoard
- (void)_menuButtonDown:(id)down
{
    NSLog(@"你好");
    %orig;//call the original _menuButtonDown;
}
%end
```

这段代码的意思是勾住 (hook) _SpringBoard_ 类里的__menuButtonDown:_ 函数，先将一句话写入 _syslog_ , 再执行函数的原有操作。

### %log

该指令在 %hook 内部使用，将函数的类名、参数等信息写入 syslog。

```Plain
%hoot SpringBoard
- (void)_menubuttonDown:(id)down
{
    %log((NSString *)@"iOSRE",(NSString *)@"Debug");
    %orig;//call the original _menuButtonDown;
}
%end
```

### %orig

该指令在 _%hook_ 内部使用，执行被勾住 (hook) 的函数的原始代码。例如：

```Plain
%hook SpringBoard
- (void)_menuButtonDown:(id)down
{
    NSLog(@"你好");
    %orig; //
}
%end
```

如果去掉 _%orig_ 那么原始函数不会执行。

```Plain
hook SpringBoard
- (void)_menuButtonDown:(id)down
{
    NSLog(@"你好");
}
%end
```

还可以利用 _%orig_ 更改原始行数的参数。

```Plain
%hook SBLockScreenDateViewController
- (void)setCustomSubtitleText:(id)arg1 withColor:(id)arg2
{
    %orig(@"Re",arg2);
}
%end
```

这个方法会改变锁屏界面的日期显示.

### %group

该指令用于将 * %hook _分组，便于代码管理及按条件初始化分组，必须以_ %end_ 结尾；一个_ %group _可以包含多个_ %hook _, 所有不属于某个自定义_ group _的_ %hook _会被隐式归类到_ %group_ungroupes * 中。用法如下：

```Plain
%group iOS7Hook
%hook iOS7Class
- (id)iOS7Method {
     id result = %orig;
     NSLog(@"This class & method only exist in iOS 7.");
     return result;
 } %end
%end // iOS7Hook

%group iOS8Hook
%hook iOS8Class
- (id)iOS8Method {
   id result = %orig;
   NSLog(@"This class & method only exist in iOS 8."); return result;
 }
%end
%end // iOS8Hook
```

### %init

该指令用于初始化某个 * %group _, 必须在_ %hook _或_ %ctor * 内调用; 如果带参数, 则初始化指定的 group, 如果不带参数, 则初始化 __ungrouped_ , 如下:

```Plain
\#ifndef kCFCoreFoundationVersionNumber_iOS_8_0
\#define kCFCoreFoundationVersionNumber_iOS_8_0 1140.10 \#endif
%hook SpringBoard
- (void)applicationDidFinishLaunching:(id)application {
    %orig;
    %init; // Equals to %init(_ungrouped)
    if (kCFCoreFoundationVersionNumber >= kCFCoreFoundationVersionNumber_iOS_7_0 && kCFCoreFoundationVersionNumber < kCFCoreFoundationVersionNumber_iOS_8_0)
      %init(iOS7Hook);
    if (kCFCoreFoundationVersionNumber >= kCFCoreFoundationVersionNumber_iOS_8_0)
      %init(iOS8Hook);
}
%end
```

只有调用了 %init, 对应的 %group 才能起作用, 切 切 !

### %ctor

_tweak_ 的 * constructor * 完成初始化工作；如果不显式定义, Theos 会自动生成一个 *%ctor _, 并在其中调用_ %init(_ungrouped) *。因此,

```Plain
%hook SpringBoard
- (void)reboot {
    NSLog(@"If rebooting doesn't work then I'm screwed.");
    %orig;
}
%end
```

可以成功生效, 因为 Theos 隐式定义了如下内容:

```Plain
%ctor
{
    %init(_ungrouped);
}
```

而

```Plain
%hook SpringBoard
- (void)reboot{
     NSLog(@"If rebooting doesn't work then I'm screwed.");
     %orig;
}
%end

%ctor
{
    // Need to call %init explicitly!
}
```

里的 _%hook_ 无法生效，因为这里显示定义了 _%ctor_ ，却没有调用 _%init_ ，_%group(__ungrouped)_ _不起作用。_%ctor_ 一般可以用来初始化 _%group_ , 以及进行 MSHookFunction 等操作。

注意, _%ctor_ 不需要以 _%end_ 结尾 。

### %new

在 _%hook_ 内部使用, 给一个现有 _class_ 加新函数, 功能与 _class_addMethod_ 相同。它的用法如下:

```Plain
%hook SpringBoard
%new
- (void)namespaceNewMethod {
     NSLog(@"We've added a new method to SpringBoard.");
}
%end
```

### %c

该指令的作用等同于 _objc_getClass_ 或 _NSClassFromString_, 即动态获 一个类的定义, 在 _%hook_ 或 _%ctor_ 内使用。

### %subclass

### %config

> 本文由简悦 SimpRead 转码