> 本文由 简悦 SimpRead 转码， 原文地址 https://www.wikimoe.com/?post=243

[![](https://www.wikimoe.com/content/uploadfile/201808/72551535690738.jpg)](https://www.wikimoe.com/content/uploadfile/201808/72551535690738.jpg)

作者：[广树](https://www.wikimoe.com/?author=1 " eeg1412@gmail.com") _|_ 时间：2019-12-8 15:49:32 _|_ 分类 : JavaScript/jQuery/Vue

在 Element UI 里，如果点击过一次某个按钮，这个按钮就会被选择，然后这个时候按下回车就会连续触发按钮的点击事件，对一些需要服务器交互的按钮来说太过不友善。

根据官方文档，似乎禁不了这个事件，那么只能通过代码去禁止了。

```Plain
<el-button type="primary" ref="btn">按钮</el-button>
```

首先给按钮定义一个 ref。

```Plain
mounted() {
       this.$refs.btn.$el.onkeydown= (e) =>{
            let _key=window.event.keyCode;
            if(_key===13){
             return false;
            }
        }
}
```

然后通过监听回车事件来强行禁止回车事件。

赞一个 1

[![](https://www.wikimoe.com/content/templates/black_memory%20v1.1/images/donate.png)](https://www.wikimoe.com/content/templates/black_memory%20v1.1/images/donate.png)