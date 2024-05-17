> 没有导出的后顾之忧时，Notion 就变得更可爱了。

### **Matrix 精选**

[Matrix](https://sspai.com/matrix) 是少数派的写作社区，我们主张分享真实的产品体验，有实用价值的经验与思考。我们会不定期挑选 Matrix 最优质的文章，展示来自用户的最真实的体验和观点。

文章代表作者个人观点，少数派仅对标题和排版略作修改。

没有导出的后顾之忧时，Notion 就变得更可爱了。

## 痛点

介绍了 Roam Research 后，有小伙伴问我是否用过 Notion。

用过。

刚才找了找，还有来自于 2017 年 5 月的 Notion 笔记记录。

简单看了一下，这三年多以来，我用 Notion 写了不少笔记，也采集了很多网页内容。

[![](https://cdn.sspai.com/2020/07/17/article89eb470dbecd11f0232a9f78c2e6d8ef)](https://cdn.sspai.com/2020/07/17/article89eb470dbecd11f0232a9f78c2e6d8ef)

但是，我算不上 Notion 的重度用户。因为有个痛点，我从来也没有解决。就是**导出**。

我用笔记工具，很多时候都需要输出成文章发布。发布的时候，我得用 Markdown。

很不幸，在 Notion 上，这个过程，从来就没有痛快过。

虽然 Notion 从很早就提供 Markdown 导出，还包括子页面。但是导出来的结果，总是无法令我满意。

[![](https://cdn.sspai.com/2020/07/17/articlea95fa21604696905fabf598b55889752)](https://cdn.sspai.com/2020/07/17/articlea95fa21604696905fabf598b55889752)

例如子页面仅仅是指实质的上下层级关系，而链接的页面不包含在导出结果中。

[![](https://cdn.sspai.com/2020/07/17/article4c79633fffa505bd41cf86b2d9d007ea)](https://cdn.sspai.com/2020/07/17/article4c79633fffa505bd41cf86b2d9d007ea)

因为喜欢卡片式笔记，拼接移动，我是希望 notion 能够像 Scrivener 一样，输出的时候把这些卡片拼完整输出的。

但是，这基本上做不到。

导出的标题，只要是中文，就都是「无标题」(Untitled)。

[![](https://cdn.sspai.com/2020/07/17/article2af0a2b75409deabd9918bd08b55f7ad)](https://cdn.sspai.com/2020/07/17/article2af0a2b75409deabd9918bd08b55f7ad)

内嵌照片，要么因为是链接，导出过程根本就没有下载。

[![](https://cdn.sspai.com/2020/07/17/articlebec99e3f77e9f079cbcef5e475f83433)](https://cdn.sspai.com/2020/07/17/articlebec99e3f77e9f079cbcef5e475f83433)

要么下载之后，也无法正常在 Markdown 编辑器里面显示。

[![](https://cdn.sspai.com/2020/07/17/articleae8d76ea8b1d7c574d105e5ba72162bd)](https://cdn.sspai.com/2020/07/17/articleae8d76ea8b1d7c574d105e5ba72162bd)

有的就没有按照图片来对待：

[![](https://cdn.sspai.com/2020/07/17/articlef37482c275bf3d9cb22e696150e19e08)](https://cdn.sspai.com/2020/07/17/articlef37482c275bf3d9cb22e696150e19e08)

而即便是被下载下来的图片，有的也没有合适的扩展名。

[![](https://cdn.sspai.com/2020/07/17/articlef80023da7508cc23ef34dbe207c0387c)](https://cdn.sspai.com/2020/07/17/articlef80023da7508cc23ef34dbe207c0387c)

但是如果预览，你会发现它就是张图啊！

[![](https://cdn.sspai.com/2020/07/17/articlede69d5f88c63766d74eb39e05d9ee874)](https://cdn.sspai.com/2020/07/17/articlede69d5f88c63766d74eb39e05d9ee874)

由于不能在输出的时候，保持完整性和可用性，我就不敢再把更多的笔记迁移进来，同时也不愿意在 Notion 上写更多的文章了。

## 解决

前些日子，我因为写研究报告的需要，从 Notion 里批量导出一些笔记，放入「第二大脑」里面进行处理。

上网查资料的时候，我突然发现了[这个 Github 项目](https://github.com/echo724/notion2md)，叫做 `notion2md`。

[![](https://cdn.sspai.com/2020/07/17/article2740f7eb6ecf70aadf4cc564bf18dd26)](https://cdn.sspai.com/2020/07/17/article2740f7eb6ecf70aadf4cc564bf18dd26)

它已经做成了 Python 的软件包，可以调用 Notion 的 API，帮助用户导出为更妥帖的 markdown 格式。

你只需要使用：

```Plain
pip install notion2md
```

安装之后，就能执行：

```Plain
python -m notion2md
```

你需要指定输出文件名称，自己的 `token_v2` 身份验证信息，以及来源 notion 链接，就能在本地输出导出的 Markdown 结果了。

[![](https://cdn.sspai.com/2020/07/17/articlefc7af35d2860fcbd5eb55cf90cd33a81)](https://cdn.sspai.com/2020/07/17/articlefc7af35d2860fcbd5eb55cf90cd33a81)

但是，这个工具，有以下几个问题：

首先，你需要安装 Python 和依赖模块；

其次，对于每一个要导出的单元，你都需要重新执行一遍。作为单一文章输出，这还好。但是如果你是打算进行数据备份或者迁移，那就太麻烦了；

另外，你需要在后期手动进行图片路径的处理，删去多余层级。这应该是一个 bug。

正因为如此有上述的问题，所以目前该工具的 Github 页面上，只有寥寥 4 颗 star，其中一颗还是我打上去的。

[![](https://cdn.sspai.com/2020/07/17/article350a8bee2dfad0ab4e460ff77f623a5a)](https://cdn.sspai.com/2020/07/17/article350a8bee2dfad0ab4e460ff77f623a5a)

我希望的是，把上述问题解决，而且最好做成 Web App ，这样大家都可以直接拿来即用。

## 改进

经过半天的折腾，我终于用 Python 和 Streamlit 完成了这个制作过程。然后又花时间做了个使用说明出来。

[![](https://cdn.sspai.com/2020/07/17/articlec6b01287e60d4cbd195367b9628fbc77)](https://cdn.sspai.com/2020/07/17/articlec6b01287e60d4cbd195367b9628fbc77)

这个[项目的 Github 页面在这里](https://github.com/wshuyi/demo-notion-markdown-exporter)。

你只需要按照上面列出的步骤，一步步来就行。考虑到部分同学阅读英文不是很流畅，我这里翻译了一份中文步骤给你。

## 步骤

请按照以下简单步骤操作。

第一步，[打开这个链接](http://notion-to-markdown.herokuapp.com/)，你会看到 App 界面。

[![](https://cdn.sspai.com/2020/07/17/articleb01189c90084787612ca5d84d1f13354)](https://cdn.sspai.com/2020/07/17/articleb01189c90084787612ca5d84d1f13354)

第二步，获取你的`token_v2`(你的身份认证码)，并将其输入到第一个文本框中。你可以通过[阅读这个图文教程](https://www.redgregory.com/notion/2020/6/15/9zuzav95gwzwewdu1dspweqbv481s5)来学习如何取得你的 token。

第三步，将**所有要导出的页面**都移动或者链接到一个新页面。例如我这里新建了一个「准备输出」。

[![](https://cdn.sspai.com/2020/07/17/article9d59339a894007591c975f041625cce9)](https://cdn.sspai.com/2020/07/17/article9d59339a894007591c975f041625cce9)

第 4 步，复制新页面的链接，粘贴到第二个文本框中，然后按回车键。

[![](https://cdn.sspai.com/2020/07/17/article34a033d7e044f8a0328914a367d3761b)](https://cdn.sspai.com/2020/07/17/article34a033d7e044f8a0328914a367d3761b)

第五步，你会看到一个名为 “export” 的新按钮出现。点击它。

[![](https://cdn.sspai.com/2020/07/17/article1874897772efac9fd919eb95d0995754)](https://cdn.sspai.com/2020/07/17/article1874897772efac9fd919eb95d0995754)

第 6 步，运行一会儿 (视你要导出的内容多少，尤其是图片大小等因素而定)，当你看到网页上显示了一个名为「点击下载」的新链接，点击它并下载压缩文件。解压后，你会发现所有的 Markdown 文件以及图片。

[![](https://cdn.sspai.com/2020/07/17/articlef834dc2965b4e6a10526602487681852)](https://cdn.sspai.com/2020/07/17/articlef834dc2965b4e6a10526602487681852)

这是子文件夹下面的图片：

[![](https://cdn.sspai.com/2020/07/17/article31ba9d52e65cf884b01c1c22afc47b35)](https://cdn.sspai.com/2020/07/17/article31ba9d52e65cf884b01c1c22afc47b35)

第七步 (可选)，将解压后的文件夹拖到 Obsidian 或者 Zettlr 的根目录下，然后正常浏览图文。

[![](https://cdn.sspai.com/2020/07/17/article9e8b09c9dcc3da95a23c6b7127b2c27d)](https://cdn.sspai.com/2020/07/17/article9e8b09c9dcc3da95a23c6b7127b2c27d)

所有页面的标题，都被保留为 Markdown 文件的名称，对中文同样支持。这样你在后面依照标题建立双向链接，就会变得非常容易。

另外说明一下，因为 API 的功能限制，目前该 App 尚不能准确处理 Notion 的 database (数据库)，而只能对普通的页面 (Page) 进行导出。

不过各种 Media 类型都是可以处理的。只不过只有图片进行了本地化输出，其余的类型，例如视频、pdf 等都保留了原先的链接。你可以通过链接跳转访问。

对于我来说，主要是写论文和图文类教程，因此这些其他类型的多媒体数据，本来也是不需要输出的，所以刚好合适。

## 感受

有了这个比较靠谱的批量导出功能以后，我觉得 **Notion 变得更加可爱**了。

至少，我写东西的时候，可以不用考虑将来导出之后一通检查、调整、修改名称等等繁琐问题了。没有了后顾之忧，用起来感觉更加轻松愉快。

我可以更加随心所欲在 Notion 里面采集和进行快速记录，并且进行卡片笔记的撰写和整合。

## 已知问题

经过多位来自于全球各地的小伙伴帮我测试后，发现运行起来功能比较正常。

[![](https://cdn.sspai.com/2020/07/17/articlee2208df42b4618fa6a5d2791bbccf109)](https://cdn.sspai.com/2020/07/17/articlee2208df42b4618fa6a5d2791bbccf109)

目前主要反馈得来的问题，是连接可能不稳定。

没办法，咱们用的是 Heroku **免费托管**，没交钱。人一多，并发就会是个问题。而且不同电信运营商的连接可靠性也无法保障。

好在源代码我在 [前面的 Github 链接](https://github.com/wshuyi/demo-notion-markdown-exporter) 那里都给了你，所以你可以利用它在本机或者自己的私有服务器上搭建服务。

如果你要尝试自己运行服务，可以参考 [我的这份教程](http://mp.weixin.qq.com/s?__biz=MzIyODI1MzYyNA==&mid=2653540719&idx=1&sn=226b8ffaa92d7b21a81d3d3bda28ba6b&chksm=f389bbb8c4fe32ae1c192fa5c2888b54057b6ecb02bf63c20ea5930fa204c792bf33b24f0fbd&token=2147203406&lang=zh_CN#rd) 快速了解 Streamlit 的使用方法。

祝使用愉快！

## 延伸阅读

你可能也会对以下话题感兴趣。点击链接就可以查看。

- [如何快速写作论文初稿？](https://sspai.com/post/57073)
- [如何用卡片法写论文？](https://sspai.com/post/59314)
- [如何高效实践卡片式写作？](https://sspai.com/post/59109)
- [Roam Reserach 到底好在哪儿？](https://sspai.com/post/60787)
- [如何交互可视化你的卡片式笔记网络？](https://sspai.com/post/59951)

> 下载少数派 客户端 、关注 少数派公众号 ，了解更妙的数字生活 🍃

> 想申请成为少数派作者？冲！ 本文由简悦 SimpRead 转码