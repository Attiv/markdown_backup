> 本文由 简悦 SimpRead 转码， 原文地址 https://www.jianshu.com/p/307427e6d990

[![](https://upload.jianshu.io/users/upload_avatars/1928848/26ef9693e906.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/96/h/96/format/webp)](https://upload.jianshu.io/users/upload_avatars/1928848/26ef9693e906.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/96/h/96/format/webp)

0.5832016.07.29 14:37:45 字数 315 阅读 8,459

### 1. MARK

我们知道, 在 OC 中我们可以使用 pragma mark 添加一些说明, 能够快速定位到相应的代码,

> 例如: \#pragma mark - 说明文字

那么在 swift 中怎么实现类似的功能呢?  
其实也很简单, 只要在需要添加说明的地方加上如下格式的注释:  

> // MARK: - 说明文字, 带分割线  
> // MARK: 说明文字, 不带分割线  

MARK 一定要大写, 例如:

```Plain
public func someFunc1()  {
        
    }
```

在类视图中就会出现刚刚添加的文本注释, 并且有一条分割线隔开

[![](http://upload-images.jianshu.io/upload_images/1928848-d8e93289f0c02cf2.png)](http://upload-images.jianshu.io/upload_images/1928848-d8e93289f0c02cf2.png)

MARK

### 2. TODO

是在编写一个类的时候, 一些功能可能需要以后添加或者补全, 这时需要一个标记, 用于提醒, 可使用 TODO 关键字添加注释:

> TODO: 需要提醒的文字

这时, 在类视图中就会出现需要提醒的文字:

[![](http://upload-images.jianshu.io/upload_images/1928848-0be1e021397c185f.png)](http://upload-images.jianshu.io/upload_images/1928848-0be1e021397c185f.png)

TODO

### 3. FIXME

有时候在编程的过程中, 会有一些小的 bug, 不紧急也不影响程序的运行, 可以暂时不予处理, 稍后需要修改, 其用法类似 TODO, 只是语义有所区别:

> FIXME: 需要修改 bug 的相关说明

[![](http://upload-images.jianshu.io/upload_images/1928848-49de243f820a1184.png)](http://upload-images.jianshu.io/upload_images/1928848-49de243f820a1184.png)

FIXME

以上就是在 swift 中经常使用的在类视图添加

“每一滴汗水都滋润着脚下的土地”

还没有人赞赏，支持一下

[![](https://upload.jianshu.io/users/upload_avatars/1928848/26ef9693e906.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/100/h/100/format/webp)](https://upload.jianshu.io/users/upload_avatars/1928848/26ef9693e906.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/100/h/100/format/webp)

总资产 345 (约 24.96 元) 共写了 13.0W 字获得 1,116 个赞共 524 个粉丝

### 被以下专题收入，发现更多相似内容

### 推荐阅读[更多精彩内容](https://www.jianshu.com/)

- 图解 Android Studio 技巧 | 玩转 TODO 及自定义 TODO 转载：Android 进阶之旅 在开…
    
    [![](https://upload-images.jianshu.io/upload_images/1024326-64b7ad50f92f08df?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)](https://upload-images.jianshu.io/upload_images/1024326-64b7ad50f92f08df?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)
    
- 概述在 iOS 开发中 UITableView 可以说是使用最广泛的控件，我们平时使用的软件中到处都可以看到它的影子，类似…
- 在开始之前，我们先来看看开发过程中，面对以前写的代码常会碰到的问题： 这块代码好几次用到了，应该抽出去； 这个算法…
    
    [爱码士](https://www.jianshu.com/u/243819ed1836)阅读 2
    
    [![](https://upload.jianshu.io/users/upload_avatars/4427591/52fcb7b7-d3e3-40aa-b8ef-1b8ae31ecc90?imageMogr2/auto-orient/strip%7CimageView2/1/w/48/h/48/format/webp)](https://upload.jianshu.io/users/upload_avatars/4427591/52fcb7b7-d3e3-40aa-b8ef-1b8ae31ecc90?imageMogr2/auto-orient/strip%7CimageView2/1/w/48/h/48/format/webp)
    
    [![](https://upload-images.jianshu.io/upload_images/4427591-c2be5c86866e1d67.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)](https://upload-images.jianshu.io/upload_images/4427591-c2be5c86866e1d67.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)
    
- MARK 类似 OC 中 pragma mark - xxx，添加一些注释说明，能够快速定位到相应的代码 MARK: 注释说明…
- 孤孤之子，浚浚其貌；人魂枭枭，美人求之。 孤孤之子，落落（la）其身；人魂孑孑，君子单之。 孤孤之子，渺渺其能；人…
    
    [![](https://upload-images.jianshu.io/upload_images/6788458-43541c8bba325f9d.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)](https://upload-images.jianshu.io/upload_images/6788458-43541c8bba325f9d.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)