# [[技术分享] CSS中的多重选择器（Multiple Selectors）包含空白或逗号](https://pjchender.blogspot.com/2015/03/cssmultiple-selectorsspace.html)

in [技术分享](https://pjchender.blogspot.com/search/label/%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB) , [网页设计学习笔记](https://pjchender.blogspot.com/search/label/%E7%B6%B2%E9%A0%81%E8%A8%AD%E8%A8%88%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98) , [CSS](https://pjchender.blogspot.com/search/label/CSS) with [没有留言](https://pjchender.blogspot.com/2015/03/cssmultiple-selectorsspace.html#comment-form)

[![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/CSS%25E9%2581%25B8%25E6%2593%2587%25E5%2599%25A8%25E5%2582%25BB%25E5%2582%25BB%25E5%2588%2586%25E4%25B8%258D%25E6%25B8%2585%25E6%25A5%259A.jpg)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/CSS%25E9%2581%25B8%25E6%2593%2587%25E5%2599%25A8%25E5%2582%25BB%25E5%2582%25BB%25E5%2588%2586%25E4%25B8%258D%25E6%25B8%2585%25E6%25A5%259A.jpg)

在HTML 中，我们有时候会对同一个标签给予多个Class 名称，像是

```Plain
<div class="one two"></div>
```

而在CSS 里面则可能同时选择多个Class，像是

```Plain
.one .two{}    /*兩個 class 中有空格*/
.one.two{}     /*兩個 class 中沒有空格*/
.one, .two{}   /*兩個 class 中出現逗號*/
```

对于初学CSS 的人来说，常常会搞不清楚这三者的差异，究竟这三者有什么不同呢？

# HTML 部分

首先，在body里面，当我们看到<div class="one two"></div>的时候，并不是表示里面有一个class叫做「one two」，在字串里的空格其实是把两个class给分开了，所以正确的意思是，这个区块（div）当中，同时包含了两个class，一个叫one，另一个则叫two。

```Plain
<div class="one two">
在這個div中，同時有兩個class，一個叫one，一個叫two
</div>
```

当我们要编辑这个class 的style 时，可以选one 或选two 其中一个，都可以编辑到这个区块。

# CSS 部分

那么为什么我们有时候会看到.one .two{ }这样子的写法呢？  
这里，我们需要进一步区别到底是.one.two{ }，.one .two{ }，或这是.one, .two{ }。乍看之下，这三者都长得很像，但实际上是有很大的不同的。  

- 第一个的one和two中间没有包含空格，这个的意思表示，某个区块必须同时具有 one和two的class时，才能被CSS所选择到到。
- 第二个的one和two中间包含空格，意思是指，我必须要是在one 里面的two，才会被选择到。
- 第三个的one 和two 中间包含逗号，意思是指class 中有one 或two，都会被编辑器所选择到。

简单来说，

**没空格表示必须同时包含才会被选取；有空格表示后面的class被镶嵌在前面的class中才会被选取；逗号则表示只要有其中一个class就会被选取到**

。

# 程式范例

让我们用下面这段HTML 语法来看个简单的例子：

```Plain
<div class="container">
    <div class="one box">只有 one</div>
    <div class="two box">只有 two</div>
    <div class="one two box">同時有 one 和 two</div>
    <div class="one box">
        <div class="two">one 裡面的 two</div>
    </div>
    <div class="two box">
        <div class="one">two 裡面的 one</div>
    </div>
</div>
```

一开始所有的box 都没有套上任何的背景色，会像是这样子：

[![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/1.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/1.png)

第一种情况，当我的CSS选择器是填入.one.two，中间没有包含空格的时候，只有同时包含有class名称为one和two的div会变色，结果如下：

[![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/2.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/2.png)

第二种情况，当我的CSS选择器.one .two，中间有包含空格时，指的是one里面又包含two的div才会变色，结果如下：

[![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/3.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/3.png)

相反的，如果我打的是.two .one，中间同样有空格的话，指的是two里面又包含one的div才会变色，结果如下：

[![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/4.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/4.png)

最后，第三种情况是写成.one,.two，中间包含有逗号，这样指的是只要包含有one或two的div都会被选择到，结果如下：

[![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/5.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/5.png)

# 自己来动手操做看看吧

这里附上codepen的连结，大家可以点选右上角的"Edit on Codepen" ，在CSS中自己测试看看，当你选择.one，.two，.one.two，.one .two，.one, .two看看会有什么不同吧！

- [HTML](https://codepen.io/PJCHENder/embed/NRqPGq?default-tab=css%2Cresult&embed-version=2&height=246&slug-hash=NRqPGq&theme-id=0&user=PJCHENder&name=cp_embed_1#html-box)
- [CSS](https://codepen.io/PJCHENder/embed/NRqPGq?default-tab=css%2Cresult&embed-version=2&height=246&slug-hash=NRqPGq&theme-id=0&user=PJCHENder&name=cp_embed_1#css-box)
- [Result](https://codepen.io/PJCHENder/embed/NRqPGq?default-tab=css%2Cresult&embed-version=2&height=246&slug-hash=NRqPGq&theme-id=0&user=PJCHENder&name=cp_embed_1#result-box)

[EDIT ON](https://codepen.io/PJCHENder/pen/NRqPGq)

`/* 輸入欲放入的 CSS 選擇器*/ .one,.two{ background-color: rgba(37,165,95,0.8); height: 100%; } /* CSS For Decoration */ html, body{ background-color: \#2C5D63; font-family: "微軟正黑體"; color: \#DFEBED; font-weight: bold; } .container{ display: flex; height: 100vh; justify-content: space-around; } .box{ width: 100px; height: 100px; margin: auto; border: 2px solid #DFEBED; border-radius: 5px; text-align: center; }`

**只有 one  
  
****  
只有 two  
  
****  
同時有 one 和 two  
  
****  
one 裡面的 two  
  
****  
two 裡面的 one  
**

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

参考资料：[CSS-TRICKS](https://css-tricks.com/multiple-class-id-selectors/)

Share: [__](https://www.facebook.com/share.php?v=4&src=bm&u=https://pjchender.blogspot.com/2015/03/cssmultiple-selectorsspace.html&t=%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F)[__](https://twitter.com/home?status=%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F%20--%20https://pjchender.blogspot.com/2015/03/cssmultiple-selectorsspace.html)[__](https://plus.google.com/share?url=https://pjchender.blogspot.com/2015/03/cssmultiple-selectorsspace.html)[__](https://pinterest.com/pin/create/button/?source_url=https://pjchender.blogspot.com/2015/03/cssmultiple-selectorsspace.html&media=https://1.bp.blogspot.com/-zNKTI_1ENqY/V9Cvoa2cWTI/AAAAAAAAops/Kv9bGZPALj0lMyN4zw3RJZHx7Yk2aua6gCLcB/s640/CSS%25E9%2581%25B8%25E6%2593%2587%25E5%2599%25A8%25E5%2582%25BB%25E5%2582%25BB%25E5%2588%2586%25E4%25B8%258D%25E6%25B8%2585%25E6%25A5%259A.jpg&description=%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F)

# Related Posts:

- [![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)
    
    [[教学] jQuery学习笔记第七堂（animate使用：制作轮拨式广告看板）](https://pjchender.blogspot.com/2015/04/jquery-animate.html)
    
- [![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)
    
    [[教学] jQuery学习笔记第六堂（制作下拉式选单效果）](https://pjchender.blogspot.com/2015/03/jquery_25.html)
    
- [![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/cross-browser-support.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/cross-browser-support.png)
    
    [跨浏览器套版列印：根据不同的浏览器载入不同的CSS](https://pjchender.blogspot.com/2015/07/css_24.html)
    
- [![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)
    
    [[教学] jQuery学习笔记第三堂（建立阅览画面：显示show、隐藏hide、切换toggle）](https://pjchender.blogspot.com/2015/03/jquery_9.html)
    
- [![](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)](https://www.notion.so%5B%E6%8A%80%E8%A1%93%E5%88%86%E4%BA%AB%5D%20CSS%E4%B8%AD%E7%9A%84%E5%A4%9A%E9%87%8D%E9%81%B8%E6%93%87%E5%99%A8%EF%BC%88Multiple%20Selectors%EF%BC%89%E5%8C%85%E5%90%AB%E7%A9%BA%E7%99%BD%E6%88%96%E9%80%97%E8%99%9F.resources/Jquery-mobile-logo.png)
    
    [[教学] jQuery学习笔记第四堂（hover语法：滑鼠移过表格时，该列产生不同格式色彩或字体）](https://pjchender.blogspot.com/2015/03/jquery-hover.html)