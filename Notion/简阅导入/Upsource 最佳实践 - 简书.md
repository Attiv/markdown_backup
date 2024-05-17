### Upsource 功能介绍

### 简介

Upsource 作为 Jetbrains 公司出品的一款`Code Review`工具，通过与版本管理软件（ Git、 Mercurial、 Subversion 和 Perforce）结合，以社交化的形式，将代码予以团队成员或其他人分享、讨论。

### 主要功能

### 便捷的查看自己的项目

Upsource 主要基于版本管理软件，因此，只要项目已经交给 Upsource 管理，你就可以方便的看到你所参与的项目, 以及最近相关的 Feeds。

[![](http://upload-images.jianshu.io/upload_images/8032324-6e88461b411cce86.png)](http://upload-images.jianshu.io/upload_images/8032324-6e88461b411cce86.png)

你所贡献的项目

[![](http://upload-images.jianshu.io/upload_images/8032324-dcd7aadd7d34682a.png)](http://upload-images.jianshu.io/upload_images/8032324-dcd7aadd7d34682a.png)

相关 Feeds

### 不同的 Review 角色

在 Upsource 之中，针对`一次review`分为了 3 个不同的角色，`Author`、`Reviewer`、`Watcher`  
其中  
`Author`在创建本次 Review 时，Upsource 会自动根据代码的提交来判断，因此不可修改.

**Reviewer**：主要负责审核代码作者对该份代码的修改并留下反馈，他可以随时在该次 review 中讨论并留下意见，也可以关闭这次 review。

**Watcher**：watcher 不太需要去关心代码的细节修改，关注重点是项目的状态以及团队成员的讨论。

[![](http://upload-images.jianshu.io/upload_images/8032324-313a588ee25e60c9.png)](http://upload-images.jianshu.io/upload_images/8032324-313a588ee25e60c9.png)

review 角色

如上图所示，作为 review 的发起者，你可以点击`+`邀请团队成员或者其他人作为`reviewer`或者`watcher`，同时，你可以将`鼠标放在头像之上`，看到该成员本次 review 的进度, 如下所示

[![](http://upload-images.jianshu.io/upload_images/8032324-9540c752885761dd.png)](http://upload-images.jianshu.io/upload_images/8032324-9540c752885761dd.png)

image.png

### 简单方便的 Review 视图

以 Idea、Webstorm、Pycharm 闻名的 Jetbrains 公司，对于代码的展现方示方式自然得心应手，无论是 python、c++、c#、Java、Javascript 都可以很好的在浏览器中展现，甚至 React、Vue 这样的 DSL，也能正常的展示出来

[![](http://upload-images.jianshu.io/upload_images/8032324-787983a52782aa3d.png)](http://upload-images.jianshu.io/upload_images/8032324-787983a52782aa3d.png)

在线展示 React 代码

### 社交化的 Review 形式

在 review 中，如果您发现某一行代码实现有问题，你可以随时在该行加上注解，并`@`相关开发同学，当他做出合理的解释或者修改后，您就可以标记这行已经解决过了，已方便减少不必要的重复 review

[![](http://upload-images.jianshu.io/upload_images/8032324-80803fdfbb12d8f6.png)](http://upload-images.jianshu.io/upload_images/8032324-80803fdfbb12d8f6.png)

image.png

### Jetbrains 插件集成

如果你不喜欢在浏览器上做 Review，同时正巧你又使用的是 Jetbrains 旗下的软件进行开发任务，那么你可以天然的将 Upsource 通过插件的形式集成在你的 IDE 上  
详细说明可以在官方文档上查到，这里就不在展开：  
[https://www.jetbrains.com/help/upsource/installing-plugin.html](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.jetbrains.com%2Fhelp%2Fupsource%2Finstalling-plugin.html)

### 基于 Upsource 的 CR 实践

通过这段时间对 Upsource 的使用，我们可以通过创建 Branch Review，来对一个迭代的代码进行 Review，一个加上 Review 的开发流程如下所示。

[![](http://upload-images.jianshu.io/upload_images/8032324-cd79fd8637502561.png)](http://upload-images.jianshu.io/upload_images/8032324-cd79fd8637502561.png)

开发流程. png

### 创建项目

如果登录 Upsource 后，发现没有你自己的项目，那么，你需要自行将项目创建出来。

- 点击首页右上角的设置按钮 设置
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-9f284ffe895bb43c.png)](http://upload-images.jianshu.io/upload_images/8032324-9f284ffe895bb43c.png)
    
- 点击`Create Project` 创建项目
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-8a59d3a32d8b9a1a.png)](http://upload-images.jianshu.io/upload_images/8032324-8a59d3a32d8b9a1a.png)
    
- 输入`项目名字`、`仓库地址`、`仓库校验`方式等相关信息 输入必备信息
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-1503f8b278d01ba6.png)](http://upload-images.jianshu.io/upload_images/8032324-1503f8b278d01ba6.png)
    
- 点击 `Create Project`即可

这时，便可以看到项目已经正在导入之中, 待项目导入成功，就可以开始创建一`Review`

[![](http://upload-images.jianshu.io/upload_images/8032324-349b82500497bd69.png)](http://upload-images.jianshu.io/upload_images/8032324-349b82500497bd69.png)

image.png

### 基于 Branch 创建 Review

- 进入项目之后，点击`Branch` image.png
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-c2c6eabf2de2eff5.png)](http://upload-images.jianshu.io/upload_images/8032324-c2c6eabf2de2eff5.png)
    
- 点击本次迭代需要 Review 分支 (如 **Review** 的基础分支不是 Master, 需要自己点击 _Change default branch_ 来替换，已便能正常识别修改内容) image.png
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-5907dcc65cee8ec9.png)](http://upload-images.jianshu.io/upload_images/8032324-5907dcc65cee8ec9.png)
    
- 点击`Create Branch Review`即可 image.png
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-e4102cba66c61168.png)](http://upload-images.jianshu.io/upload_images/8032324-e4102cba66c61168.png)
    
- 这时候便可以在右侧面板上看到本次修改文件的变化，然后自行把`Reviewer`以及`Watcher`拉进`Review`中即可

[![](http://upload-images.jianshu.io/upload_images/8032324-49f5a1330febf93b.png)](http://upload-images.jianshu.io/upload_images/8032324-49f5a1330febf93b.png)

image.png

### 开始 Review

- 对有疑问的代码位置，可以点击左侧的`红笔`, 填写你的意见或者疑问并`@`者或者团队其他成员 提出疑问
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-ed8658dc13db1727.png)](http://upload-images.jianshu.io/upload_images/8032324-ed8658dc13db1727.png)
    
- 当团队成员作出合理解释或者修改后，可以点击`Resolve`来标明这个疑问已经作出回答 解决疑问
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-4453bc4e34b67471.png)](http://upload-images.jianshu.io/upload_images/8032324-4453bc4e34b67471.png)
    

### 完成 Review

当`reviewer`对该次 review 已经没有疑问了，可以通过 `Accept`或者`raise concern`来告知 review 发起人，你对这次 review 的结果，review 发起人，也可以通过看 Reviewer 头像的方式，快速了解到 Reviewer 对该次 review 的观点

[![](http://upload-images.jianshu.io/upload_images/8032324-affcefb61b90885c.png)](http://upload-images.jianshu.io/upload_images/8032324-affcefb61b90885c.png)

完成 review

[![](http://upload-images.jianshu.io/upload_images/8032324-9ef89896682fd03a.png)](http://upload-images.jianshu.io/upload_images/8032324-9ef89896682fd03a.png)

查看 review 观点

### 关闭 Review

- 当迭代即将上线，所有的文件以及提出疑问都得到了`Review`或者`解答`, 那么，我们需要将这次 Review 关闭, 点击`Close review`即可 【该操作一般为 review 发起人发起，如果该修改已上线，请记得关闭，以免对 reviewer 造成影响】 结束 review
    
    [![](http://upload-images.jianshu.io/upload_images/8032324-dc894562b9112395.png)](http://upload-images.jianshu.io/upload_images/8032324-dc894562b9112395.png)
    

### 其他

如果说，普通的`Branch Review`可能并不能很好的满足本次迭代的需求，我们也可以将某次提交，绑定到已经创建好的 Review。

- 点击想要 Review 的提交，进入页面后右上角点击`Review change`后点击`Attach to review`，随后选中已经创建好的 Review, 这样，就可以将某一些提交附着于你创建好的 Review 上了

[![](http://upload-images.jianshu.io/upload_images/8032324-4920e138531003c6.png)](http://upload-images.jianshu.io/upload_images/8032324-4920e138531003c6.png)

image.png

### 总结

Upsource 是一个比较偏向社交化的 CR 工具，可以充分利用开发的碎片时间进行，如果您的团队既想保证 CR 覆盖率，又不希望阻塞项目，那么可以考虑使用该工具来完成 CR。

如果该文能够帮您解决问题，欢迎`点赞`, 您的赞是我更新的最大动力，谢谢 > 本文由简悦 SimpRead 转码