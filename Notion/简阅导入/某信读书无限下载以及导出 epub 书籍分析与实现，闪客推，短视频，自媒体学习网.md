> 某信读书无限下载以及导出 epub 书籍分析与实现未经许可，不要转载 1 前言 wx 读书 app 是个不错的产品，用了蛮久，但最近发现其广告越来越多，免费书籍越来越少，甚至曾经看完的书，再看都收费了。

未经许可，不要转载

## 1 前言

wx 读书 app 是个不错的产品，用了蛮久，但最近发现其广告越来越多，免费书籍越来越少，甚至曾经看完的书，再看都收费了。  
于是就想把曾经看过的书籍导出保存。经过 N 天的研究，终于成功了。只要能全本下载的书籍，就可以导出。  
  
该 app 大部分代码都是使用 objective-c 语言开发，该语言是比较灵活的动态语言，因此比较好逆向。  

本文主要以技术分享为主，也顺便总结记录下经验，对于实验结果，只要肯钻研，相信大家都能实现自己的目标。

## 2 环境准备

硬件：Mac 电脑（系统：MacOS 12.0.1）、 已越狱的 iPhone6s(系统：iOS 13.6)

软件：XCode 13.1、 MonkeyDev(非越狱开发 XCode 插件)、 Sublime Text、 FinalShell(图形化 ssh 工具)、  
Hopper Disassmembler、 某信读书. ipa（已脱壳，app 版本：5.4.8）、真机调试的苹果证书  

代码：QMUI 框架 (企鹅的)、SSZipArchive(zip 解压缩开源代码)、从 ipa 中砸壳得到的头文件（非常有用, 几乎等于看到了一半源代码）

关于越狱、ipa 获取、ipa 脱壳，非越狱开发调试等，大家可自行百度。

## 3 下载书籍分析，解除每月 3 次下载限制

只有完全下载的书籍，才能导出 epub，这里也是为了更方便的导出 epub 做准备。

思路分析：  
我们知道，每月下载多于 3 次就会有弹窗限制。  
  
按照正常的程序逻辑，每次开始下载时，都应该去服务器端验证是否已超过 3 次。  
  
这里确实验证了，但是仅仅验证了次数，并没有对下载的 url 进行处理。  
  
也就是说如果对下载 url 限制的话，超过 3 次，访问下载的 url 就应该提示错误。这里并没有限制。  
  
因此，就有个漏洞：只要我们绕过下载次数的验证，就能访问到下载的 url 了，就可以下载了。  

那么为什么企鹅的工程师不在下载 url 上面进行验证呢？  
这是因为：下载书籍的操作，与读书时加载书籍的逻辑是完全一样的。  
  
具体逻辑是怎样的，我们放到后面章节。  

现在我们的策略就很清晰了：绕过下载次数的限制。  
如何绕过呢？有几种方法  
  
比如修改验证次数请求的返回值，改为不超过 3 次。  
  
每次开始下载时，直接跳过验证。  
  
这里使用直接跳过验证。（因为验证请求的返回函数，没有 hook 到）  

下面分析下载函数调用过程：新建 WeReadDev MonkeyDev 工程，拖入脱壳的 ipa 文件，导入砸壳得到的所有. h 头文件（方便搜索），运行，打开下载页面。

### 3.1 分析下载按钮点击事件，即点击调用的函数

打开带有下载按钮的页面后，使用 XCode 的 UI 界面分析工具，分析下载按钮以及页面所在的控制器（MVC 中的 C）

选中【下载到本地】按钮，然后右侧导航栏，选择倒数第 2 个工具图标，查看按钮的属性，我们主要看按钮事件名以及所属的类名，  
可以看到按钮事件的 target 在 WRReaderMoreOperationController 中，事件方法为 handleItemViewEvent  
  
如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111606-6368e8f6e40aa.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111606-6368e8f6e40aa.jpg)

接下来，我们按照点击的函数去顺腾摸瓜，找到下载的真正函数。因此打开 Hopper，把 xxx.ipa 拖进去，搜索 handleItemViewEvent 方法。  
很不幸，hopper 中，居然没有该函数。如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111609-6368e8f9e03bb.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111609-6368e8f9e03bb.jpg)

还记得砸壳出的所有头文件吗？我们去头文件中，看看有没有 handleItemViewEvent。依然没有。  
那我们搜下按钮的 target 类即：WRReaderMoreOperationController  

可以看到该类是存在的，那么为什么按钮点击的方法却没有呢，原因：点击事件应该是父类的方法，因此，我们看看它的父类 QMUIMoreOperationController  
看着名字就感觉很奇怪，WR 我们可以猜测代表 WeRead, QMUI 开头的应该就是通用的类库了，大厂都会封自己的基本类库，不奇怪。如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111613-6368e8fddafce.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111613-6368e8fddafce.jpg)

那么该如何继续分析呢? 大厂的基本类库是开源的，因此我们直接拿来源代码看看，百度 QMUI，下载下来。xCode 打开 QMUI 的代码，我们全局搜索 handleItemViewEvent  
在类 QMUIMoreOperationController 中，搜索到了该方法，在该方法内部调用了一个 delegate 和一个 block, 在本读书 app 中，使用的是代 {过}{滤} 理，  
  
也就是实现了方法：didSelectItemView。 如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111616-6368e900dda9b.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111616-6368e900dda9b.jpg)

在我们的项目中，全局搜索 didSelectItemView，可以看到很多类都实现了此代 {过}{滤} 理方法。那么点击下载后，具体是哪个类调用了该方法呢。  
其实是类：WRReaderViewController ，它的父类 WRBaseReaderViewController 实现了该方法。如下图：  
  
WRReaderViewController，该类就是正在读书的页面的真正的控制器，也就是说，正在读书的页面逻辑操作，基本都由此类控制（若代码遵循 MVC 原则的话）。  
  
后面会分析为何该类为读书页面的控制类。  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111621-6368e9054bdb7.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111621-6368e9054bdb7.jpg)

现在我们知道在那个类调用了点击下载的方法了，接下来继续寻找真正下载的函数。在 hopper 中, 全局搜索 didSelectItemView，可以发现有很多个。  
我们定位到 WRBaseReaderViewController 该类中的 didSelectItemView 方法。（因为该类是读书控制类的父类）。如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111624-6368e908dd93a.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111624-6368e908dd93a.jpg)

可以看到内部调用了 handleOfflineButtonclick 方法。双击进入该方法。如下图：

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111627-6368e90b81bcd.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111627-6368e90b81bcd.jpg)

可以看到内部调用了 handleOfflineButtonClickWithScene 方法，该方法由 offlineDownloadUIHelper 获取到的对象调用。双击跳转进入：

该方法很长，我们只看关键部分，这里有 3 个主要部分： 如下图。  
下载状态函数： 该方法用来判断是否已下载本书。这里先有个大概印象，之后需要用到。  
  
downloadBookStatusWithBookId:(id)arg1 checkHasAvailableUnDownload:(Bool)arg2  

判断本月下载是否多于 3 次：这里是需要跳过的地方。

下载函数：使用此方法下载书籍。  
continueHandleOfflineRuttonClickWithNormalBookIds: comicsBookIds: targetOffline: startTips:  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111631-6368e90f47f26.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111631-6368e90f47f26.jpg)

至此，我们已经找到需要跳过的地方，以及下载的函数了。接下来开始实现无限下载。

### 3.2 根据分析的结果，实现无限下载

经过上面分析，我们清楚了下载点击时函数调用关系。那么如何跳过 3 次限制呢？

这里我们用如下思路：  
当点击按钮时，直接调用下载书籍的函数。（去掉中间的各个过程，这就绕过次数验证了）  

首先 hook 点击按钮时会调用的函数，经过上面分析，会调用很多函数。hook 哪一个呢?

这里 hook 此函数：handleOfflineButtonClickWithScene。

为什么 hook 它，因为该函数所属的实例对象，调用了真正的下载函数。也就是真正的下载函数与本函数 是属于同一个类的方法。

在分析中，我们知道该方法的实例对象 是由 offlineDownloadUIHelper 这个东西返回的。我们全局搜索下，看看它是啥。如下图：  
可以看到，其是 WROfflineDownloadUIHelper 类的对象，也就是说下载函数在 WROfflineDownloadUIHelper 类中。  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111634-6368e912acdfe.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111634-6368e912acdfe.jpg)

接下来，直接 hook WROfflineDownloadUIHelper 类的 handleOfflineButtonClickWithScene 方法，  
并且在 hook 方法内部，直接调用下载函数  
  
continueHandleOfflineRuttonClickWithNormalBookIds: comicsBookIds: targetOffline: startTips:  

关于参数的传递:  
第一个 NormalBookIds：显然是普通书籍的 id, 可以从本实例得到。  
  
第二个 comicsBookIds：猜测是漫画书的 id，忽略漫画，所以全部传空。  
  
第三个 targetOffline：传 NO，根据 Hooper 中的反汇编代码，可知传 NO  
  
第四个 startTips： 猜测是开始时的提示，这里忽略。传空。  

这里使用 logos 语法进行 hook，请看代码：如下图

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111638-6368e91688595.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111638-6368e91688595.jpg)

至此，下载的次数就被去掉了，就可以无数次下载了。不过，这里我们还要做一件事，那就是 hook 下载状态。让所有书籍都可以重新下载。  
之所以如此是因为：导出 epub 书籍，我们使用的是下载的 zip 文件包的内容。  
  
而微信读书的下载逻辑是：下载某个章节的 zip 包，然后解压数据并加密后，拷贝到该书籍的缓存目录，清空 zip 文件。  
  
因此，我们每次获取 zip 包，必须重新下载。下面请看 hook 下载状态函数，如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111642-6368e91af085c.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111642-6368e91af085c.jpg)

至此，就完全可以无限次、重复的下载了。

## 4 书籍的文件结构分析

想导出书籍，我们必须弄清楚，书籍在本地是如何存放的，其数据结构是什么。了解了之后，才能知道以何种方式导出。因此本过程是必须的。

### 4.1 查看书籍的缓存文件

因为 iOS 系统有沙盒机制，应用都有自己的缓存目录。因此在 app 运行时，我们直接使用 XCode 打印出沙盒的路径。就可以看到 App 缓存在本地的所有文件内容了。

启动 XCode 运行我们的 WeReadDev 项目，app 启动后，随意打开一本书，然后点击 UI 分析工具，这样程序会暂停，我么可以使用 XCode 中集成的 lldb 调试器打印数据。

打印出目录：/var/mobile/Containers/Data/Application/DA344853-7949-44C1-89EE-B3D54897B161/Documents 如下图

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111647-6368e91f69019.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111647-6368e91f69019.jpg)

使用 FinalShell 连接设备，查看文件。有很多文件夹，最后发现发现个 Books 文件夹，里面是一对数字文件夹。随意进入个，内部是一堆 html 文件。  
/var/mobile/Containers/Data/Application/DA344853-7949-44C1-89EE-B3D54897B161/Library/254802774/Books  
  
由此，可以猜测，此处就是书籍缓存目录了。只是书籍数据是加密过的。  
  
如下图  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111652-6368e92405afa.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111652-6368e92405afa.jpg)

### 4.2 解密缓存文件

我们需要解密出缓存文件内容，然后根据内容，看如何导出文件。如何解密呢？  
根据经验，直接在项目中，全局搜索 decrypt 关键字。会发现很多相关的函数。  
  
依据函数名以及所属的类，这里我们直接定位到 所属于 WREpubFileManager 类的以下方法：  

- (id)decryptContentsOfFile:(id)arg1 forBookId:(id)arg2; 如下图：

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111656-6368e928705e6.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111656-6368e928705e6.jpg)

接下来，hook 该方法，并打印日志，然后运行 app，打开新的书籍，看是否会打印日志。  
经过测试，每次加载新的章节，就会调用该方法解密. 通过参数的值，可以确定解密的就是缓存的文件。如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111701-6368e92d13f70.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111701-6368e92d13f70.jpg)

该函数的返回值，应该就是解密后的数据。接下来就验证下数据。  
断点至该函数结束完成，打印返回值，得知类型是 NSData，二进制数据流。我们直接把它写入本地文件，然后导出查看内容。  

写了个保存文件函数，打印了导出路径：如下图

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111705-6368e93172a0b.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111705-6368e93172a0b.jpg)

用 FinalShell 访问路径，导出文件，然后查看其内容。可以发现，html 文本内容就是书籍的内容。如下图：

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111710-6368e9364824e.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111710-6368e9364824e.jpg)

由此，我们就可以拿到解密的缓存文件了。

**这里要注意下：加密的所有文件都是通过此函数来进行解密的，包括图片、css 文件等。**

### 4.3 分析文件结构以及书籍加载逻辑

书籍已经解密了，接下来简要看下文件结构。

在书籍的缓存的 Books 目录下，有很多数字的文件夹，每个数字目录代表一本书，数字就是书的 ID(解析过程略过)。  
我们来看下某书籍下的目录：有 4 个文件夹 Images、Styles、Text、Tmp 。  
  
这里直接上结论，书籍内容主要由 Text 内的 html 文件提供，另外的 Images 和 Styles 提供 html 需要的资源。Tmp 临时目录，忽略。  

书籍内容由 html 提供，可以确定，这是可以组装成 epub 文件导出的。

因此，我们只要想办法把 Images、Styles、Text 这 3 个文件夹的内容组合到一起，导出即可。

但是因为 Text 文件夹内，有许多章节的 html，无法确定章节的顺序，以及索引等数据，因此直接使用解密的缓存文件导出 epub，可能会造成书籍数据混乱。

所以要想准确的组装数据，还需要找到带有章节索引信息的的数据。这就是下面 4.4 部分需要描述的内容。

继续之前，先分析下书籍的加载逻辑。

经测试得知。阅读图书时，书籍内容的加载逻辑是：

a、每次加载一个 zip 数据包，该数据包中包含不定章节内容，可能含有 1 个章节，也可能多个。  
b、获取到 zip 数据包后，解压数据，此时的数据是未加密的。然后对数据加密，缓存至书籍的缓存目录。  
  
c、读书时，先从本地缓存目录查找，若不存在就去下载 zip 包。  

注意：一开始打开图书时，会预先加载部分 zip 数据。

**下载逻辑与阅读时的加载逻辑类似。**  
因为点击了下载按钮后，也是先去本地缓存目录看有没有，若没有就下载 zip，然后加密数据，缓存。  
  
因此下载也是一个 zip，一个 zip 的获取。  
  
也就是说 下载其实就是 一起把书籍所有章节全部缓存到本地。  
  
与你直接看完一本书，是一个道理。  

### 4.4 寻找书籍的源文件（下载的 zip 文件）

zip 文件是猜测的，因为数据要在互联网上传输，一定需要压缩。还有 epub 文件本身就是 zip 的压缩方式。

起初的思路是直接 hook 解压的方法，因为 zip 一定需要解压，但是试了几个，都没有找到解压的函数。

后来又想到，解压文件一定会用到写入文件的方法，因此，我们 hook 写入文件的方法。看是否可以找到解压 zip 的函数。  
如下图，我 hook 了 NSData 的所有写入文件的方法，果然写入文件的操作，都被抓到了。同时还有个意外收获。  
  
就在某个文件写入前，有一个函数吸引了注意，如下：  

[WRBookNetwork processEpubZipAtPath:book:chapterUids:chaptersStr:isFromReview:]

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111714-6368e93a91ca7.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111714-6368e93a91ca7.jpg)

看名字 processEpubZipAtPath， 有 epub 有 zip，猜测就是源文件了。因此在头文件搜索，果然搜到了。

这里去 hopper 中，看了下该函数的伪代码，发现其内部确实是对 zip 进行了解压操作，然后加密文件，拷贝至书籍目录。  
在 hopper 中，可以看到解压用的是 SSZipArchive 三方类库。稍后我们解压和导出 epub 时也就用它了。  

直接 hook 该函数，看看传进来的参数都是什么。运行，断点在该 hook 的函数，打印参数：  
可以知道，第一个参数就是 zip 文件路径，第二个参数是 WRBook 对象。使用 FinalShell 访问路径，导出文件，改为 zip 打开。如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111719-6368e93f18d59.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111719-6368e93f18d59.jpg)

关于密码的获取，是在 hopper 中发现的，因为这里要解压文件，所以密码肯定在相关的参数中，这里直接公布答案：密码是 WRBook 类的 epubPassword 方法返回的。  
因此，我们直接在 XCode 刚才的断点处，直接执行代码： [((WRBook*)arg2) epubPassword] ，可以看到返回了一个字符串：hi7GPj12y  
  
使用该值，成功的解压了刚才的 zip，可以看到，zip 内的文件结构与书籍缓存的类似，但是多了一个 info.txt 文件，如下图：  

[![](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111724-6368e9442be39.jpg)](https://www.shanketui.com/wp-content/uploads/2022/11/20221107111724-6368e9442be39.jpg)

从 info.txt 的文件内容就可以确定，该文件就是 html 文件的索引信息（相当于书籍的目录），有了索引信息，有了书籍内容，就可以完整的导出书籍了。

### 4.5 小结

我们重新梳理下书籍的加载（下载）逻辑。

a、点击下载按钮  
b、去本地缓存目录查找是否存在。  
  
c、不存在，开始下载 zip  
  
d、解压 zip 文件到临时目录  
  
c、加密解压后的文件，缓存至书籍目录 (不包括索引文件)  
  
e、清空临时目录内容  

至此，我们已经完全清楚书籍文件的来源，结构，加解密过程。那么如何导出 epub 文件呢？  
思路如下：  
  
在步骤 d 中，我们拷贝 zip 文件以及密码到指定目录，  
  
然后把书籍的所有的 zip 数据解压合并，根据 info.txt 创建索引信息，组装成 epub 格式，导出。  

## 5 导出 epub

我们知道书籍的存储结构了，也知道缓存文件在哪，那么我们只要将书籍的所有源文件整合到一起，然后保存文件即可

### 5.1 epub 文件格式概述

由于我们想组装成 epub，需要先了解下其格式。

**a、mimetype**

每一个 epub 电子书均包含一个名为 mimtype 的文件，内容固定为：application/epub+zip，用以表示是 epub 的文件格式。

**b、META-INF（文件夹，包含一个文件 container.xml）**

用于存放容器信息，主要用于告诉阅读器，电子书的根文件（rootfile）的路径和打开格式，内容可以一般固定不变，除非改变了 OEBPS 目录名。

**c、OEBPS（文件夹，包含 images 文件夹、很多 html 文件、css 文件和 content.opf 文件等）**

OEPBS 目录用于存放 OPF 文档、CSS 文件、NCX 文档。

OPF 文档是 epub 的核心文件，且是一个标准的 xml 文件，依据 OPF 规范，此文件的根元素为 由五部分组成：、、、、

NCX 文件是 epub 电子书的又一个核心文件，用于制作电子书的目录，其文件的命名通常为 toc.ncx。ncx 文件也是一个 xml 文件。ncx 代表 “Navigation Center eXtended”，意思大致就是导航文件，这个文件与目录有直接的关系。

mimetype 和 META-INF 的内容，我们固定写死，不用修改。  
我们要修改的文件主要是 opf 和 ncx 的内容。  

下面请看完整的 Epub 文件结构示意图：

### 5.2 在页面上添加导出按钮

我们可以在下载书籍时，拿到书籍的所有章节的 zip 文件，但我们还需要一个导出 zip 的入口。  
因此我们就在书籍页面的右上角添加一个 export 按钮。  
  
添加方式是：hook 读书控制器类 WRReaderViewController 的 viewDidAppear 方法，当该方法调用时，在页面上添加一个按钮。  

新建类 EpubExportView ，写成单例模式，添加按钮以及导出的事件都在此类中完成。看下效果图。

### 5.3 下载书籍时，保存所有章节的 zip 包

这里其实就比较简单了，在我们 hook 的 processZip 的函数中，复制 zip 文件以及密码进行保存。如下图：

### 5.4 构建 epub 书籍文件的内容

_首先解压所有的 zip 文件，并移动到指定 data 目录。_

前文提到在 app 内使用了三方的解压工具 SSZipArchive，因此我们也使用它。去网上找到其代码找到函数原型，动态调用。  
我们肯定没办法直接调用原 app 内的函数，缺少声明，编译器会报错。又因为解压的函数参数过多，不方便使用 oc 的动态调用方法。  
  
因此，这里直接使用 oc 消息转发机制，使用 c 语言的调用方式。请看下图：  

_组装 epub 内容_

可以看到，我们已经将所有文件都解压到 data 目录了。  
因为每个 zip 包的目录下，都有 3 个文件夹和 1 个 info.txt 文件，因此我们需要把多个 zip 中的各文件夹合并到一起。  
  
在合并过程中，info.txt 文件不需要进行操作，仅仅记录下各个 info 文件所在的路径。稍后会根据所有 info.txt 创建 epub 内容。  
  
然后，再将这 3 个文件夹移动到 epub 的 OEBPS 目录中。  

移动完成后，根据 info.txt 文件创建 ncx 和 opf 文件。

这里我写了一个 EpubCreator 类来进行操作。如下图：

### 5.5 导出 epub 文件

内容组装完成，接下来压缩导出文件。  
这里直接使用 SSZipArchive 类的压缩方法，直接将准备好的 epub 内容进行压缩成 epub 文件。  

这里是导出到了指定目录，那么如果是在非越狱的机器上，如何查看导出的书籍呢？  
答案：在 XCode 中，公开文档目录，通过文件 App 访问。  

过程就不赘述了，看下效果图吧。

### 5.6 小结

每次下载书籍前，最好清空下原有缓存，避免个别章节没有下到。  
导出的过程，基本上就是正向开发。没有什么难点，相对的难点可能是 解压和压缩的代码调用了。  

## 6 总结

其实，很久之前就砸壳了该 app，逆向了几张壁纸，也解密了文章缓存，但对于导出还是耗费了些时间。  
特别是对于书籍源文件的获取。以及还原书籍下载的逻辑，也是耗费了不少脑细胞。  

希望本文对于技术学习的朋友可以有所帮助。

因本人水平有限，若有错误之处，欢迎指出！谢谢大家！

未经许可，禁止转载 > 本文由简悦 SimpRead 转码