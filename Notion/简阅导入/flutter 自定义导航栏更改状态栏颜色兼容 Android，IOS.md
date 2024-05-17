## flutter 自定义导航栏更改状态栏颜色兼容 Android，IOS

> flutter 下自定义导航栏更改状态栏背景颜色和字体颜色，测试 ios、Android 有效

### 前言

flutter 最近火得有些过分，做为一名后端我都想试试它。国内目前关于 flutter 的文档还是挺少的，很多问题都难以找到解决方案。最近在使用 flutter 也遇见了不少的问题，就拿更改 flutter 状态栏背景、字体颜色来说道说道，在百度、google 上随便一搜都有一大堆的文章说明如何使用 flutter 属性来实现，但是在真正自己实际开发中发现并不能达到预期的目的，ios，android 不同平台上没有真正解决实际问题。下面解决办亲测 ios、Android 有效

### 属性

- AnnotatedRegion
- AppBar

两个属性都可以达到更改状态栏的目的，但是在真机开发过程中发现 _AnnotatedRegion_ 在 ios 下无法达到预期的效果字体和颜色都没有改变，_AppBar_ 在 Android 下也不能达到预期效果。并且 _AnnotatedRegion_ 在页面上存 _在 appBar_ 下的情况下不会生效。解决办法就是通过 _Theme.of(context).platform_ 判断当前是 ios 还是 android 根据不同的平台使用不同的属性，具体代实现码如下

```Plain
Widget build(BuildContext context) {
    return AnnotatedRegion<SystemUiOverlayStyle>(   // android 更改状态栏颜色
      value: SystemUiOverlayStyle(
          statusBarColor: Colors.white,
          statusBarIconBrightness: Brightness.dark,
          systemNavigationBarColor: Colors.white,
      ),
      child: Scaffold(
        backgroundColor: Colors.white,
        appBar: PreferredSize(      //ios下更改状态栏颜色
          //判断是是否是android，是android需去掉AppBar，否则无AnnotatedRegion无效
          child: Theme.of(context).platform == TargetPlatform.android
              ? Container()
              : AppBar(backgroundColor: Colors.white, elevation: 0),
          preferredSize: Size.fromHeight(0),
        ),
        body:Text('hello world'),
      )
    )
  }
复制代码
```

> 查看源码发现 SystemUiOverlayStyle 有 dark 和 light 两个自带的属性，SystemUiOverlayStyle.dark 和 SystemUiOverlayStyle.light 在 ios 是效果的，但是只能修改状态的字体颜色但是无法修改背景颜色

上面的示例代码在 ios 黑暗模式下状态栏的字体颜色默认是白色的，关于 ios 黑暗模式的问题解决办法也有很多请自行 google > 本文由简悦 SimpRead 转码