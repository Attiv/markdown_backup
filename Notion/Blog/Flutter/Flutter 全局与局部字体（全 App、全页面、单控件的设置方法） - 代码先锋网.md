> Flutter 全局与局部字体（全 App、全页面、单控件的设置方法），代码先锋网，一个为软件开发程序员提供代码片段和技术文章聚合的网站。

项目里需要单独替换几个页面的字体。于是找到了全局指定字体的方法，参考文章：[Flutter 指定字体（全局指定、局部指定）](https://blog.csdn.net/emdd2016/article/details/93312143)，该文章提到了三种替换方法：

> ①全局替换，在 MaterialApp 的 theme 属性中，指定 fontFamily。  
> ②单个替换，单独在 Text 的 style 中指定 fontFamily。  
> ③多处替换，定义公共 TextStyle , 调用它的 copyWith 方法。  

为了方便理解，在此搬运一下：**1. 全局配置— 就在主题 theme 中配置**

```Plain
MaterialApp(
  theme: ThemeData(
      fontFamily: "PingFang", // 统一指定应用的字体。
      primarySwatch: Colors.green,
      primaryColor: Colors.white),
      。。。
```

**2. 局部配置—指定 TextStyle 中的 fontFamily**

```Plain
TextStyle(
    fontFamily:"PingFang", // 指定该Text的字体。
    fontSize: SizeUtil.getFontSize(Dimens.font_sp12),
    color: CustomColors.colorPrimary,
    fontWeight: FontWeight.bold)
```

**3. 如果多处用到指定的字体，但又不是全局用到， 你可以定义一个公共的 textStyle . 如：**

```Plain
var textFontStyle  = TextStyle(
    fontFamily:"PingFang", // 指定该Text的字体。
)

用到的地方用 .copyWith 这个方法, 如：
Text(
    "显示我想要的字体",
    style: textFontStyle.copyWith(
        fontSize: 18.0,
        color: Colors.red,
        fontWeight: FontWeight.bold,
        ),
    )

TextStyle的copyWith如下：

 TextStyle copyWith({
    bool inherit,
    Color color,
    Color backgroundColor,
    String fontFamily,
    List<String> fontFamilyFallback,
    double fontSize,
    FontWeight fontWeight,
    FontStyle fontStyle,
    double letterSpacing,
    double wordSpacing,
    TextBaseline textBaseline,
    double height,
    Locale locale,
    Paint foreground,
    Paint background,
    List<ui.Shadow> shadows,
    TextDecoration decoration,
    Color decorationColor,
    TextDecorationStyle decorationStyle,
    double decorationThickness,
    String debugLabel,
  })
```

我们项目是需要替换几个页面，不是全 App，第一种方法直接 pass。第二种和第三种差不多，都是需要给每个 Text 控件设置字体，区别只是第三种不用每次指定字体名称。我们页面里面 Text 控件蛮多的，每个指定，也有较大的工作量。**那么，有没有单独指定某个页面的字体的方法呢？**  
以下是几种尝试：  

## 1、在页面外包裹 Theme() 控件（无效）

全局指定的方法很眼熟，那么直接在某一块控件外，包裹一个 Theme 控件，不就和在 MaterialApp 中指定的一样吗？想到这里，我不得不佩服我的机智，这么简单的方法，居然只被我一个人想出来！  
于是我兴冲冲的去尝试了，在 Column 控件外包裹 Theme，在 Theme 中指定字体，期待这整个 Column 控件都变成我指定的字体。代码如下：  

```Plain
@override
  Widget build(BuildContext context) {
    return Theme(
      data: ThemeData(
        fontFamily: "MaoTi",
      ),
      child: Column(
        children: <Widget>[
          Row(
            children: <Widget>[
              Text("12345"),
              Text("678910"),
            ],
          ),
        ],
      )
    );
  }
```

然而，该方法无效，Text 的字体并没有随之改变！

## 2、在页面外包裹 MaterialApp 控件（某些全局设定会冲突）

MaterialApp 也是一个控件，在整个页面外嵌套一层 MaterialApp，然后在该 MaterialApp 的 theme 属性中设置 fontFamily。代码如下：

```Plain
@override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        fontFamily: "MaoTi",
      ),
      home: RealPage(),
    );
  }
```

该方法是有效的，字体确实改变了。不过，之前的一些全局配置，比如滑动控件的波纹效果、配置的首选颜色等，被 MaterialApp 层拦截了，页面中使用的是 Flutter 默认的 MaterialApp 配置，没有使用整个 App 入口指定的配置。需要把这些全局配置重新指定一遍，才能达到一致的效果。

## 3. 在 Scaffold 外包裹 Theme 控件

为啥在 MaterialApp 的 theme 指定有效，直接在控件外包裹 Theme 控件却无效了？我感到很奇怪。查看源码，源码里也是直接用 Theme 包裹着 child 控件啊？真是太神奇了！  
我注释掉部分代码，希望找到让 Text 字体生效的控件，经过 fromwork 层绕了一圈，发现生效的控件居然不在 fromwork 层，而是从外面传进去的！！！又经过一番排查，终于锁定，令 theme 生效的控件是 Scaffold。  
  
验证发现，字体是否生效与 MaterialApp 没有半毛钱关系，只与 Scaffold 有关。而 Scaffold 几乎是每个页面都有的，在它外层包裹 Theme，指定 fontFamily, 即可达到单独设置某个页面的效果。而且，它不会阻隔 MaterialApp 中指定的全局配置，完美！  

```Plain
@override
  Widget build(BuildContext context) {
    return Theme(
      data: ThemeData(
        fontFamily: "MaoTi",
      ),
      child: Scaffold(
          body:
          Column(
            children: <Widget>[
              Row(
                children: <Widget>[
                  Text("12345"),
                  Text("678910"),
                ],
              ),
            ],
          )
      ),
    );
  }
```

Theme 结合 Scaffold，能指定页面级别的 Text 控件字体。但是，如果页面中有使用富文本，或者自定义的 Text 控件，字体不会生效，还得在 style 中单独设置。在 MaterialApp 的 theme 属性中指定 fontFamily，同样会有这个问题。因为字体只和 Scaffold 有关，和 MaterialApp 没有关系。

```Plain
@override
  Widget build(BuildContext context) {
    return Theme(
      data: ThemeData(
        fontFamily: "MaoTi",
      ),
      child: Scaffold(
          body:
          Center(child: Column(
            children: <Widget>[
              Row(
                children: <Widget>[
                  // 富文本，ThemeData中的指定无效，需在TextStyle中单独指定
                  RichText(
                      text: TextSpan(
                          text: "123456",
                        style: TextStyle(color: Colors.blue,fontSize: 30,fontFamily: "MaoTi",)
                      )),
                  // 自定义文本，同上。能不能通过改变自定义方法来使用Theme字体不太清楚，我们项目中的自定义字体需单独指定
                  CustomText("123456",style: TextStyle(color: Colors.red,fontFamily: "MaoTi",),)
                ],
              ),
            ],
          )
          )
      ),
    );
  }
```

字体的指定，从大到小，目前有以下几种方法：

> ①全 App，在 MateralApp 中指定，只要每个页面都有 Scaffold，需注意一下富文本和自定义文本。  
> ②全页面，Theme 结合 Scaffold 使用，同样需注意富文本和自定义文本。  
> ③多处使用，定义公共 TextStyle，调用 copyWith 方法。  
> ④单个控件，直接在 TextStyle 中设置 fontFamily。  

技术是在不断发展的，我当前使用的版本是 1.9，或许后面高的版本会有更多的使用方法，又或者现在我遇到的问题在高版本并不会用到，这篇文章只能提供一个思路，给大家参考，感谢阅读！  
最后，也谢谢 [@emdd2016](https://blog.csdn.net/emdd2016) 大大，他的文章给我指了一个验证的方向。本文只提供了使用字体的方法，引入字体的方法网上太多，不再赘述，可以自行查找。  

_参考文章：_[_https://blog.csdn.net/emdd2016/article/details/93312143_](https://blog.csdn.net/emdd2016/article/details/93312143) > 本文由简悦 SimpRead 转码