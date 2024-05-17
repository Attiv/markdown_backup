  

## 介绍

无障碍服务是一种应用，可提供界面增强功能，来协助残障用户或可能暂时无法与设备进行全面互动的用户完成操作。Android 使用 TallBack 来辅助无障碍阅读，iOS 使用 Voice Over.  
在原生系统里二者对无障碍服务的开发支持比较完善，而 Flutter 对于无障碍开发的支持还只是一些基础功能(目前在 iOS16 上有很多问题), 对于朗读触发焦点管理是不支持的，官方issue 里的说法是暂时没有打算支持。  

下面介绍下常用的三个组件：  
  
[Semantics](https://api.flutter.dev/flutter/widgets/Semantics-class.html) (主要用这个)  
  
[MergeSemantics](https://api.flutter.dev/flutter/widgets/MergeSemantics-class.html) (checkbox 这种组合的多用)  
  
[ExcludeSemantics](https://api.flutter.dev/flutter/widgets/ExcludeSemantics-class.html) (不读的时候用)

## Semantics 常用属性

`label`: 点击读的提示  
  
`image`: 是否是图片，以此类推  
  
`explicitChildNodes`: 是否强制显示子组件的语义 (Row, Column使用，不然读不到子组件)  
  
`excludeSemantics`: 是否排除子组件的语义, 设置为 `true` 后不再读子组件。  
  
`container`: 是否再引入一个新的语义节点.  
  
`enabled`: 是否可用  
  
`checked`: CheckBox 是否被勾选  
  
`button`: 是否是一个按钮  
  
`slider`: 是否是个 slider  
  
`link`: 是否是个link  
  
`header`: 是否是标题  
  
`textField`: 是否是textField  
  
`readOnly`: 是否只读  
  
`focusable`: 是否可聚焦  
  
`focused`: 是否聚焦  
  
`scopesRoute`: 是否是声明路由名  
  
`namesRoute`: 是否包含路由的语义标签  
  
`sortKey`排序, `sortKey: OrdinalSortKey(2),` ~~可以使用这种方式让默认发声，~~(有些情况会生效，很多时候不生效，不确定具体原因，如果有了解的望告知)  
  
`...`: 剩余的一些可以参考源码，不是很常用  
  
`child`: 子组件

> 使用 Focus() 和 autofucos 是没有办法自动发声的，输入框可以用 focusNode.

### 无障碍焦点管理替代办法

> 这种方法也会出现不工作的情况，而且在Android 13上是不支持的(只在Android 13 上测试过),目前看来 Flutter 对无障碍的支持只是基础的朗读内容

```Plain
import 'package:flutter/scheduler.dart';
  final FocusNode _tempNode = FocusNode();
  FocusScopeNode _focusScopeNode;
   @override
  void initState() {
    super.initState();
    SchedulerBinding.instance.addPostFrameCallback((_) {
      _focusScopeNode = FocusScope.of(context);
      _focusScopeNode.requestFocus(_tempNode);
    });
  }

 @override
  Widget build(BuildContext context) {
  Focus(
                            child: _widget,
                            focusNode: _tempNode,
                          ),
  }
```

## 最后

要开发无障碍，首先要使用无障碍。在使用无障碍功能的过程中体验了不同的使用方式，打开了另一种思路，也发现了设计对于无障碍也是有需求的：

1. 确保文字和背景的颜色有足够高的对比度  
    (根据  
    [WCAG](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) 标准，文字和背景色的对比度至少是 4.5:1；如果是大于等于 24 px/ 19 px bold 的文字，对比度至少是 3:1 )
2. 别只依靠颜色传达信息  
    (比如：同时使用「颜色区分 + 标签 + 说明」，来表明哪个是错误状态。)  
    
3. 等等

无论是 App 开发还是 Web 开发，还是希望大家多多考虑视觉障碍用户，多多支持无障碍功能。