> 本文由 简悦 SimpRead 转码

本人是做 iOS 开发的，点击空白处取消 TextField 焦点这个需求是非常简单的，在学习 Flutter 过程中，面对这个需求走了不少弯路，现在得到了一个感觉不错的解决方案，这里和大家分享一下，也希望对小伙伴们有所帮助。

```Plain
GestureDetector(
    behavior: HitTestBehavior.translucent,
    onTap: () {
        // 触摸收起键盘
        FocusScope.of(context).requestFocus(FocusNode());
    },
    child: *******
}
复制代码
```

把上面的代码放在最外层，你自己的布局就放在 child 里面，亲测有效。