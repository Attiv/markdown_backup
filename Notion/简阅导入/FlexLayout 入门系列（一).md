大概是在 4 月底入的坑吧，当时看[掘金有文章介绍 Flexbox](https://juejin.cn/post/6844903541295808525) 在移动端有了一个实现，就是 `Facebook` 的 `yoga`，而 `iOS` 对应的实现叫做 `YogaKit`。

原来 `Flexbox` 布局方式在 `web` 端比较流行，仔细研读该文，发现布局方式是`盒子模型`的概念，好奇之下又读了[一篇 yoga 的教程](https://juejin.cn/post/6844903491165487118)（`Raywenderlich` 出品，必属精品），对着教程做下来发现很有意思，但是语法还是稍显繁琐。

然后不知怎么的又发现了一个 `YogaKit` 的封装实现（`Swift` 的)，叫做 [**FlexLayout**](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2FlayoutBox%2FFlexLayout)，看了它的使用 Demo，一时无语凝噎，相见恨晚！

> 本篇先不讲任何原理的东西，只是演示 3 个 Demo 让大家直观感受一下它是怎样的。

### 示例 1

先从一个官方小 Demo 开始吧，如下图所示:

用 `FlexLayout` 来布局需要多少代码呢？

```Plain
view.addSubview(rootFlexContainer)
rootFlexContainer.flex.padding(12).define { flex in
    flex.addItem().direction(.row).define { flex in
        flex.addItem(imageView).width(100).aspectRatio(of: imageView)
        flex.addItem().paddingLeft(12).grow(1).shrink(1).define { flex in
            flex.addItem(segmentedControl).marginBottom(12).grow(1)
            flex.addItem(label)
        }
    }
    // 分隔线
    flex.addItem().height(1).marginTop(12).backgroundColor(.lightGray)
    flex.addItem(bottomLabel).marginTop(12)
}
复制代码
```

### 示例 2

剁手党都很熟悉了，这是淘宝首页的搜索框点击后的界面。搜索框，`tab page` 什么的就先忽略了，单讲 **历史搜索** 以下的核心布局代码:

```Plain
rootFlexContainer.flex.padding(10).define { flex in
    // 历史搜索，垃圾桶
    flex.addItem().direction(.row).justifyContent(.spaceBetween).define { flex in
        flex.addItem(histLabel)
        flex.addItem(delButton)
    }
    // 搜索过的标签
    flex.addItem().direction(.row).wrap(.wrap).marginBottom(15).define { flex in
        for btn in historyTagButtons {
            flex.addItem(btn).marginRight(10).paddingHorizontal(12).marginTop(10)
        }
    }
    // 搜索发现，眼睛
    flex.addItem().direction(.row).justifyContent(.spaceBetween).define { flex in
        flex.addItem(disLabel)
        flex.addItem(seeButton)
    }
    // 搜索发现的标签
    flex.addItem().direction(.row).wrap(.wrap).marginBottom(15).define { flex in
        for btn in discoverTagButtons {
            flex.addItem(btn).marginRight(8).paddingHorizontal(12).marginTop(10)
        }
    }
}
复制代码
```

效果图：

怎么样？如你所见，全是按钮，我可没有用 `UICollectionView` 这个大杀器来布局哦，因为这里根本没有重用的场景，用它也并不能起到节省内存的效果。

### 示例 3

来给【百词斩】卖一波广告，坐公交等公交的时候背几个单词，充分利用碎片时间学习呀！

骚年，你的 `UIStackView` 是否早已饥渴难耐了？来看看核心布局代码：

```Plain
// 注意Flexbox的 marginTop, marginBottom 百分比指的是superview的宽度百分比
// 每次用它俩的百分比都会导致莫名的坑, 所以暂不建议使用marginTop, marginBottom的百分比方法
// 这里折中使用屏幕高度百分比来计算值
rootFlexContainer.flex.alignItems(.center).define { flex in
    flex.addItem(logoImgV).width(30%).marginTop(ScreenHeight * 0.18).aspectRatio(1)
    flex.addItem().grow(1).shrink(1) // 占位弹簧
    flex.addItem().justifyContent(.center).width(73%)
        .height(24%).marginBottom(ScreenHeight * 0.1).define { flex in
        flex.addItem(wechatBtn).height(buttonHeight).marginBottom(10)
        flex.addItem(qqBtn).height(buttonHeight).marginBottom(10)
        flex.addItem().direction(.row).height(buttonHeight).define { flex in
            flex.addItem(phoneBtn).width(62%).marginRight(10)
            flex.addItem(loginBtn).grow(1)
        }
    }
    flex.addItem(otherBtn).marginBottom(20)
}
复制代码
```

效果是这样的：

苹果爸爸审核要求没有安装第三方的时候，第三方相关的按钮要隐藏，假设要隐藏微信该怎么做呢？增加一个方法来隐藏按钮，并模拟调用：

```Plain
override func viewDidLoad() {
    super.viewDidLoad()
    navigationController?.setNavigationBarHidden(true, animated: false)
    configUI()
    DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
        // ...模拟: 检查到设备没有安装微信...
        self.hideButton(self.wechatBtn)
    }
    DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
        // ...模拟: 产品经理突然说不开放注册了, 只准登录...
        self.hideButton(self.phoneBtn)
    }
}

func hideButton(_ btn: UIButton) {
    btn.flex.isIncludedInLayout = false
    btn.isHidden = true
    view.setNeedsLayout()
    UIView.animate(withDuration: 0.3) {
        self.view.layoutIfNeeded()
    }
}
复制代码
```

效果：

有没有心动的感觉？  
3 个  
`Demo` 的[完整代码你可以去 github](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdarkhandz%2FFlexLayoutDemo) 里看个清清楚楚明明白白真真，注意我为了简化 `Demo` 达到演示的效果，并没有去处理动态按钮数量的问题，什么圆角性能，`safeArea` 的处理也很 ugly，一切只为了演示布局相关的～

To be continue… > 本文由简悦 SimpRead 转码