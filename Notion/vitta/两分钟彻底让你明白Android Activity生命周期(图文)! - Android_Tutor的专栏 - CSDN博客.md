原  
  
两分钟彻底让你明白Android Activity生命周期(图文)!

置顶 2010年07月28日 20:47:00

[android_tutor](https://me.csdn.net/Android_Tutor)

阅读数：275595 标签：

[android](http://so.csdn.net/so/search/s.do?q=android&t=blog)

[layout](http://so.csdn.net/so/search/s.do?q=layout&t=blog)

[string](http://so.csdn.net/so/search/s.do?q=string&t=blog)

[class](http://so.csdn.net/so/search/s.do?q=class&t=blog)

[encoding](http://so.csdn.net/so/search/s.do?q=encoding&t=blog)

[api](http://so.csdn.net/so/search/s.do?q=api&t=blog)

个人分类： [Android面试区](https://blog.csdn.net/Android_Tutor/article/category/656416) [Android基础教程](https://blog.csdn.net/Android_Tutor/article/category/605365)

大家好，今天给大家详解一下Android中Activity的生命周期，我在前面也曾经讲过这方面的内容，但是像网上大多数文章一样，基本都是翻译Android API，过于笼统，相信大家看了，会有一点点的帮助 ，但是还不能完全吃透，所以我今天特意在重新总结一下.

首先看一下Android api中所提供的Activity生命周期图(不明白的，可以看完整篇文章，在回头看一下这个图，你会明白的):

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_12803210018q71.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_12803210018q71.gif)

Activity其实是继承了ApplicationContext这个类，我们可以重写以下方法，如下代码:

为了便于大家更好的理解，我简单的写了一个Demo,不明白Activity周期的朋友们，可以亲手实践一下，大家按照我的步骤来。

第一步:新建一个Android工程，我这里命名为ActivityDemo.

第二步:修改ActivityDemo.java(我这里重新写了以上的七种方法，主要用Log打印),代码如下:

第三步:运行上述工程,效果图如下(没什么特别的):

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280322049kfxQ.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280322049kfxQ.gif)

核心在Logcat视窗里,如果你还不会用Logcat你可以看一下我的这篇文章 [Log图文详解(Log.v,Log.d,Log.i,Log.w,Log.e)](http://blog.csdn.net/Android_Tutor/archive/2009/12/26/5081713.aspx) ，我们打开应用时先后执行了onCreate()->onStart()->onResume三个方法，看一下LogCat视窗如下:

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280324212Y5nt.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280324212Y5nt.gif)

BACK键：

当我们按BACK键时，我们这个应用程序将结束，这时候我们将先后调用onPause()->onStop()->onDestory()三个方法，如下图所示:

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280324618Bqxb.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280324618Bqxb.gif)

HOME键:

当我们打开应用程序时，比如浏览器，我正在浏览NBA新闻，看到一半时，我突然想听歌，这时候我们会选择按HOME键，然后去打开音乐应用程序，而当我们按HOME的时候，Activity先后执行了onPause()->onStop()这两个方法，这时候应用程序并没有销毁。如下图所示:

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280325044k0c7.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280325044k0c7.gif)

而当我们再次启动ActivityDemo应用程序时，则先后分别执行了onRestart()->onStart()->onResume()三个方法，如下图所示:

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280325373Qjq7.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280325373Qjq7.gif)

这里我们会引出一个问题，当我们按HOME键，然后再进入ActivityDemo应用时，我们的应用的状态应该是和按HOME键之前的状态是一样的，同样为了方便理解，在这里我将ActivityDemo的代码作一些修改，就是增加一个EditText。

第四步:修改main.xml布局文件（增加了一个EditText),代码如下:

第五步:然后其他不变，运行ActivityDemo程序,在EditText里输入如"Frankie"字符串(如下图:)

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280326575HhRQ.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280326575HhRQ.gif)

这时候，大家可以按一下HOME键，然后再次启动ActivityDemo应用程序，这时候EditText里并没有我们输入的"Frankie"字样，如下图:

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_12803267326xiQ.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_12803267326xiQ.gif)

这显然不能称得一个合格的应用程序，所以我们需要在Activity几个方法里自己实现，如下第六步所示:

第六步修改ActivityDemo.java代码如下:

第七步:重新运行ActivityDemo程序，重复第五步操作，当我们按HOME键时，再次启动应用程序时，EditText里有上次输入的"Frankie"字样，如下图如示:

[![](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280327855y53e.gif)](https://www.notion.so%E4%B8%A4%E5%88%86%E9%92%9F%E5%BD%BB%E5%BA%95%E8%AE%A9%E4%BD%A0%E6%98%8E%E7%99%BDAndroid%20Activity%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F(%E5%9B%BE%E6%96%87)!%20-%20Android_Tutor%E7%9A%84%E4%B8%93%E6%A0%8F%20-%20CSDN%E5%8D%9A%E5%AE%A2.resources/0_1280327855y53e.gif)

OK,大功基本告成，这时候大家可以在回上面看一下Activity生命周期图，我想大家应该完全了解了Activity的生命周期了，不知道你了解了没？