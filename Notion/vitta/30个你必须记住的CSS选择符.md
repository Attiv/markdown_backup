**04 January 2014**

号外号外：我的新书《React状态管理与同构实战》出版啦！！！[快点我查看](https://item.jd.com/12403508.html)

原文网址：[http://yanhaijing.com/css/2014/01/04/the-30-css-selectors-you-must-memorize/](http://yanhaijing.com/css/2014/01/04/the-30-css-selectors-you-must-memorize/)

所以你学会了基础的id，类和后代选择符，然后你就一直用它们了吗？如果是这样，你丢失了（css的）巨大的灵活性。在本文中提到的很多选择器属于CSS3规范的一部分，因此，只有在现代浏览器中才可使用。

# 1.*

* { margin: 0; padding: 0; }

对于初学者，在学习更多高级选择器之前，最先了解的选择器。

星号选择器将匹配页面里的每一个元素。很多开发者使用这个技巧将外边距和内边距重置为零。虽然在快速测试时这确实很好用，但我建议你永远不要再生产代码中使用它。它给浏览器带来大量不必要的负担。

* 也能作为子选择符使用。

\#container * { border: 1px solid black; }

这将匹配\#container div的每一个后代元素。再次强调，尽量不要使用这种技术。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/star.html)

**兼容性**

- IE6+
- Firefox
- Chrome
- Safari
- Opera

# 2.\#X

\#container { width: 960px; margin: auto; }

井号前缀允许我们选择id。这是最常见的用法，不过应该慎重使用ID选择器。

反复问自己：我一定需要id来匹配要选择的元素吗？

id选择符是唯一的，不允许重复使用。如果可能的话，先尝试使用一个标签名称，一个新的HTML5元素，甚至是一个伪类。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/id.html)

**兼容性**

- IE6+
- Firefox
- Chrome
- Safari
- Opera

# 3. .X

.error { color: red; }

现在介绍的是类选择符。id和类的不同之处在于后者可以多次使用。当你想给一组元素应用样式的时候可以使用类选择符。另外，当你紧想给特殊元素应用样式的时候才使用id。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/class.html)

**兼容性**

- IE6+
- Firefox
- Chrome
- Safari
- Opera

# 4. X Y

li a { text-decoration: none; }

下一个最常用的选择符是后代选择符。当你需要给你的选择符增加特殊性的时候你可以使用。例如，如果你只想匹配无序列表下的锚元素？此时后代选择符派上用场。

小贴士——如果你的选择符看起来像这样X Y Z A B.error，那你就错了。时刻问自己使用这高的权重是否有必要。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/descend.html)

**兼容性**

- IE6+
- Firefox
- Chrome
- Safari
- Opera

# 5. X

a { color: red; } ul { margin-left: 0; }

如果你想匹配页面上的所有的元素，根据他们的类型，而不是id或类名？显而易见，使用类型选择符。如果你需要选择所有的无序列表，请使用ul {}。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/tagName.html)

**兼容性**

- IE6+
- Firefox
- Chrome
- Safari
- Opera

# 6. X:visited and X:link

a:link { color: red; } a:visted { color: purple; }

我们使用:link伪类选择符选择所有已经被点击过的锚标签。

此外，我们也有:visited伪类选择符，正如你期望的，允许我们仅给页面上被点击过的或被访问过的锚标签应用样式。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/links.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 7. X + Y

ul + p { color: red; }

这被称作相邻选择符。它将只选择紧贴在X元素之后Y元素。上面的例子，仅每一个ul之后的第一个段落元素的文本为红色。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/adjacent.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 8. X > Y

div\#container > ul { border: 1px solid black; }

X Y和X > Y之间的不同点是后者只选择直接子代。例如，考虑如下的标记。

- List Item
- Child
- List Item
- List Item
- List Item

选择符\#container > ul将只选择id为container的div的直接子代ul。它不匹配更深层的li的子代的ul。

因此，使用子代选择符有性能上的优势。事实上，这同样适用于基于css选择器的javascript引擎。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/childcombinator.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 9. X ~ Y

ul ~ p { color: red; }

这是兄弟选择符和X + Y一样，然而，它没有约束。与相邻选择符（ul + li）仅选择前一个选择符后面的第一个元素比起来，兄弟选择符更宽泛。它会选择，我们上面例子中跟在ul后面的任何p元素。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/generalcombinator.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 10. X[title]

a[title] { color: green; }

被称为属性选择器，在我们上面的例子里，这只会选择有title属性的锚标签。没有此属性的锚标签将不受影像。但如果你需要更多的特性怎么办呢？呵呵……

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 11. X[href=”foo”]

a[href="[http://net.tutsplus.com](http://net.tutsplus.com/)"] { color: \#1f6053; /* nettuts green */ }

上面的代码段将给所有href属性为[http://net.tutsplus.com](http://net.tutsplus.com/)的锚标签添加样式；他们将会显示为我们的品牌绿色。所有其他的锚标签将不受影响。

注意我们将href值用引号包裹。记住，当使用javascript的css选择符引擎时也这么做。如果可能的话，尽可能使用css3选择符代替非官方的方法。

这工作的很好，但有点不够灵活。如果链接确实直接连接到Nettus+还好，但是，也许路径是到nettust的相对路径呢？在这种情况下，我们可以使用一点正则表达式语法。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes2.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 12. X[href*=”nettuts”]

a[href*="tuts"] { color: \#1f6053; /* nettuts green */ }

来了不是~这就是我们需要的代码。*号指定了包含该属性的值必须包含定义的值。就是说，这句代码包含了href值为 [nettuts.com](http://nettuts.com/)，[net.tutsplus.com](http://net.tutsplus.com/)或者[tutsplus.com](http://tutsplus.com/)。

记住这个描述过于宽泛，如果是某个锚点标签链接到某个连接中带有tuts非Envato的网站（tutsplus属于Envato旗下网站）呢？因此你需要更多特性来限制，分别使用^和&来限定字符串的开始和结束。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes3.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 13. X[href^=”http”]

a[href^="http"] { background: url(path/to/external/icon.png) no-repeat; padding-left: 10px; }

有没有想过某些网站是如何定义一个图标的链接的？我确定你肯定看到过。这些链接很容易让你跳转到另一个网站。

使用^(carat)符灰常简单啦。这个符号常常在正则表达式中表示字符串的开始。如果我们想指向所有以”http”开头的”href”属性的锚点的话，我们就可以使用类似于上面的那段代码啦。

注意啦，我们不需要搜索”http://”,完全没必要，因为我们还要包含以https://开头的链接呢。

如果我们想为所有链接到图片的链接定义样式咋办？这种情况下，我们得搜索字符串的结束了不是。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes4.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 14. X[href$=”.jpg”]

a[href$=".jpg"] { color: red; }

又来了，我们还是使用正则表达式符号，$(dolor)，来作为字符串的结束标记。这种情况下，我们就会搜索所有url以.jpg为结尾的锚点啦。记住记住这种情况下gif和png格式的图片不会被选择哦。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes5.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 15. X[data-*=”foo”]

a[data-filetype="image"] { color: red; }

回顾最近一条，我们如何能包含各种图片类型:png,jpeg,jpg,gif?很容易想到，我们能通过多个选择器来不是，像这样：

a[href$=".jpg"], a[href$=".jpeg"], a[href$=".png"], a[href$=".gif"] { color: red; }

不过，这样很蛋疼，效率极低。另一个解决办法是使用自定义属性。如果我们加了一种自己的data-filetype属性给每一个链接到图片的锚点的话呢？

[Image Link](https://www.notion.soevernote-html-snippet:///path/to/image.jpg)

这样关联后，我们就能使用标准的属性选择器来指定这些链接啦。看下面：

a[data-filetype="image"] { color: red; }

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes6.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 16. X[foo~=”bar”]

a[data-info~="external"] { color: red; } a[data-info~="image"] { border: 1px solid black; }

这儿有个鲜为人知的特殊技巧，绝对让你印象时刻。~(tilda)符，它可以帮助我们指向那些以空格隔开多个值的属性的元素（真拗口，这翻译我自己都看不懂，水平问题）

以我们第15条的自定义属性为例，上面的代码中我们创建了data-info属性，这个属性可以定义以空格分隔的多个值。这样，这个链接本身就是个icon，并且指向的也是一个图片链接，像下面这样。

[Click Me, Fool](https://www.notion.soevernote-html-snippet:///path/to/image.jpg)

有了这样适当的标记，通过使用~属性选择器的技巧，我们就可以指向任何具有着两种属性的任何一种啦。

/* Target data-info attr that contains the value "external" */ a[data-info~="external"] { color: red; } /* And which contain the value "image" */ a[data-info~="image"] { border: 1px solid black; }

很棒，不是吗？

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes7.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 17. X:checked

input[type=radio]:checked { border: 1px solid black; }

这种伪类只会匹配已经被选中的单选元素。就是这么简单。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/checked.html)

**兼容性**

- E9+
- Firefox
- Chrome
- Safari
- Opera

# 18. X:after

before和after伪元素也很蛋疼。貌似人们每天都能找到或者发明一些新办法来有效地使用它们。它们很容易控制选择器周围的内容。

很多第一次使用是因为他们需要对clear-fix进行改进。

.clearfix:after { content: ""; display: block; clear: both; visibility: hidden; font-size: 0; height: 0; } .clearfix { *display: inline-block; _height: 1%; }

这个改进使用了:after伪类元素来在元素后增加一个空间，然后清除它。这个牛X的技巧你应该收藏到工具包里，特别是当overflow:hidden方法无能为力的时候。

想看看其他创造性的用法：[访问我滴创建阴影的窍门](http://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-getting-clever-with-css3-shadows/)

通过Css3选择器的标准说明书，你应该有技巧地使用这些伪类语法——双冒号::。不过为了兼容，浏览器会接受一个双引号。

**兼容性**

- IE8+
- Firefox
- Chrome
- Safari
- Opera

# 19. X:hover

div:hover { background: \#e3e3e3; }

我去，这个你必须懂。典型的官方形式的用户触发伪类。听起来会有点迷惑，不过实际上并非如此。想在用户在某个元素上面悬停时定义个特别的样式？这个属性就是做这个的。

记住啦，较old版本的IE，只能在锚点标签后使用这个hover。

这个选择器你用得最多的情况，估计可能就是在锚点的悬停时加个border-bottom啦。

a:hover { border-bottom: 1px solid black; }

小贴士：border-bottom:1px solid black;比text-decoration:underline;好看一点哦。（真的？我去）

**兼容性**

- IE6+ (In IE6, :hover must be applied to an anchor element)
- Firefox
- Chrome
- Safari
- Opera

# 20. X:not(selector)

div:not(\#container) { color: blue; }

not伪类灰常有用。例如我要选择所有的div，除了有id为container的。上面那个代码片段就能完美的实现。

如果我想选择除了p以外的所有元素，我可以这么做：

*:not(p) { color: green; }

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/not.html)

**兼容性**

- IE9+
- Firefox
- Chrome
- Safari
- Opera

# 21. X::pseudoElement

p::first-line { font-weight: bold; font-size: 1.2em; }

我们可以使用伪元素（以::为表示）来定义元素的样式。例如第一行，第一个字符，记住啦，这种方法只能应用于同级元素才有效。

伪元素由两个冒号组成：::

**指定p的第一个字符的样式**

p::first-letter { float: left; font-size: 2em; font-weight: bold; font-family: cursive; padding-right: 2px; }

这段代码会找到所有段落，然后再从中定义这些段落的第一个字符。

这常常使用在仿报纸的文章首字母样式。

**指定p的首行样式 **

p::first-line { font-weight: bold; font-size: 1.2em; }

同样，这个::first-line伪元素会像我们期望的那样，只定义段落的第一行的样式。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/pseudoElements.html)

**兼容性**

- IE6+
- Firefox
- Chrome
- Safari
- Opera

# 22. X:nth-child(n)

li:nth-child(3) { color: red; }

想想那些没法从元素堆中选择元素的日子。nth-child伪类解决了这个问题。

请注意nth-child接收整数和变量，不过不是从0开始的，如果你想选定第二个li，使用li:nth-child(2).

我们甚至使用这个办法来选择任意的子元素。例如，我们可以用li:nth-child(4n)来完成4为倍数的所有元素的选择。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/pseudoElements.html)

**兼容性**

- IE9+
- Firefox 3.5+
- Chrome
- Safari

# 23. X:nth-last-child(n)

li:nth-last-child(2) { color: red; }

如果我有灰常多的li在ul里面，我只想要最后3个li怎么办？不必使用li:nth-child(397),你可以使用nth-last-child伪类。

这种技巧和第六条几乎一样有效，不过两者的不同之处在于它从结束开始收集，用回溯的方式进行。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/nthLast.html)

**兼容性**

- IE9+
- Firefox 3.5+
- Chrome
- Safari
- Opera

# 24. X:nth-of-type(n)

ul:nth-of-type(3) { border: 1px solid black; }

你应该有很多时候想要元素类型来选择元素而不是通过孩子。

想象一下标记5个无序列表（UL）。如果你想定义第三个ul，并且没有一个唯一的id来找到它，你就可以使用nth-of-type(3)伪类了。在上面这个代码段中，只有第三个ul才会有黑色的边框。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/nthOfType.html)

**兼容性**

- IE9+
- Firefox 3.5+
- Chrome
- Safari

# 25. X:nth-last-of-type(n)

ul:nth-last-of-type(3) { border: 1px solid black; }

没错，我们一样可以使用nth-last-of-type来从结束开始回溯这个选择器，来找到我们想要的元素

**兼容性**

- IE9+
- Firefox 3.5+
- Chrome
- Safari
- Opera

# 26. X:first-child

ul li:first-child { border-top: none; }

这个结构的伪类让我们可以选择某个元素的第一个子孩子。你通常可以使用这个办法来删除第一个或者最后一个元素的边框。

例如，你有一系列的rows，每一个都有border-top和border-bottom。这种情况下，第一行和最后一行看起来会灰常怪。

很多设计师会使用first和last类来弥补这个缺陷。相反，你可以使用这些伪类来解决这些问题。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/firstChild.html)

**兼容性**

- IE7+
- Firefox
- Chrome
- Safari
- Opera

# 27. X:last-child

ul > li:last-child { color: green; }

与first-child相反，last-child会选择父节点的最后一个子节点。

**例子：**

我们建立一些例子来示范这些类的可能的用法。我们会建立一种风格来展示。

**标记**

- List Item
- List Item
- List Item

没啥特别的，就是一个简单的序列。

**Css**

ul { width: 200px; background: \#292929; color: white; list-style: none; padding-left: 0; } li { padding: 10px; border-bottom: 1px solid black; border-top: 1px solid \#3c3c3c; }

这个样式会设置一个背景，删除浏览器默认的ul的padding值，并定义边框给每一个li来提供一点深度。

如上图所示，唯一的问题是最上面的边框和最下面的边框看起来有点儿怪。让我们来使用:first-child和:last-child来解决这个问题。

li:first-child { border-top: none; } li:last-child { border-bottom: none; }

看上图，解决了不是。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/firstChild.html)

**兼容性**

- IE9+
- Firefox
- Chrome
- Safari
- Opera

_是滴，IE8支持 first-child 不过不支持last-child。_

# 28. X:only-child

div p:only-child { color: red; }

实话说，你很可能会发现你不会经常使用only-child伪类。尽管如此，它确实有用，你应该需要它。

它可以帮助你选择是父节点的独生子（没别的孩子啦）的元素。例如，使用上面的代码，只有是div的唯一子孩子的p段落才会定义其颜色为red。

让我们来假定下面的标记。

My paragraph here.

Two paragraphs total.

Two paragraphs total.

这样，第二个div的p标签的内容不会被选中。只有第一个div的p才会被选中。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/onlyChild.html)

**兼容性**

- IE9+
- Firefox
- Chrome
- Safari
- Opera

# 29. X:only-of-type

li:only-of-type { font-weight: bold; }

这种结构的伪类有几种灰常聪明的用法。它可以选定在其父节点内没有兄弟节点的元素。例如，我们可以选择只有一个li作为其子孩子的ul。

首先，取决于你想怎样完成这一目标。你可以使用ul li，不过，这回选择所有li元素。唯一的办法是使用only-of-type。

ul > li:only-of-type { font-weight: bold; }

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/onlyOfType.html)

**兼容性**

- IE9+
- Firefox 3.5+
- Chrome
- Safari
- Opera

# 30. X:first-of-type

first-of-type伪类可以让你选择该类型的第一个兄弟节点。

**一个测试**

为了更好地理解它，让我们来测试一下啊。拷贝下面的标记到你的编辑器。

My paragraph here.

- List Item 1
- List Item 2
- List Item 3
- List Item 4

现在，别急着往下读，试试看如何能只选择’LIST ITEM 2’?如果你搞定了（或者放弃了），继续读。

**解决办法1**

有很多办法能搞定这个测试。我们回顾其中一小部分。以使用first-of-type开始。

ul:first-of-type > li:nth-child(2) { font-weight: bold; }

这个代码段本质上表示，“找到第一个无序列表，然后找到这里面的li，然后，继续使用过滤器直到找到第二个li。

**解决办法2**

另一个可行的办法是毗邻选择器。

p + ul li:last-child { font-weight: bold; }

在这个方案中，我们找到p的临近节点ul，然后找到ul的li的最后一个孩子。

**解决办法3**

我们可以随心所欲滴选择这些选择器。

ul:first-of-type li:nth-last-child(1) { font-weight: bold; }

这次，我们取到第一个ul，然后找到第一个元素，不过是从最后一个开始数。哈哈。

[查看例子](http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/firstOfType.html)

**兼容性**

- IE9+
- Firefox 3.5+
- Chrome
- Safari
- Opera

# 结论

如果你仍在为解决old浏览器的缺陷而纠结，如IE6。在使用这些新的选择器方面，你仍然需要非常小心。不过，别因为这个阻碍了你对这些新玩意儿的学习。别虐待自己。确保关注这里的兼容性列表。应一方面，你可以使用 Dean Edward’s excellent IE9.js script 来为旧浏览器提供新的选择器支持。（我去。cool）

其次，当使用javascript库时，如流行的jQuery，最好尽可能使用这些css3本身的选择器而不是使用库的自定义方法/选择器。这能让你的代码更快哦，因为这些选择器引擎本身就能被浏览器解析，而不是用这些库选择器。

感谢阅读，希望你能学到一两个技巧。

# 译者注

本文问翻译文章，原文为“[The 30 CSS Selectors you Must Memorize](http://net.tutsplus.com/tutorials/html-css-techniques/the-30-css-selectors-you-must-memorize/)”

原文网址：[http://yanhaijing.com/css/2014/01/04/the-30-css-selectors-you-must-memorize/](http://yanhaijing.com/css/2014/01/04/the-30-css-selectors-you-must-memorize/)

关注微信公众号**颜海镜**

**赞赏支持**微信扫一扫

我的新书《React状态管理与同构实战》，深入解读前沿同构技术，感谢大家支持

**限量签名版，可指定寄语，附赠小惊喜，****点击获取**

京东：[https://item.jd.com/12403508.html](https://item.jd.com/12403508.html)

当当：[http://product.dangdang.com/25308679.html](http://product.dangdang.com/25308679.html)

[知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议](http://creativecommons.org/licenses/by-nc-sa/4.0/)

# 开源项目

- [zepto.fullpage](https://github.com/yanhaijing/zepto.fullpage) 专注于移动端的fullPage.js
- [template.js](https://github.com/yanhaijing/template.js) 一款javascript模板引擎，简单，好用。
- [变色方块](https://github.com/yanhaijing/inverter) 是一款休闲益智小游戏，适合所有人群。
- [查看更多](http://yanhaijing.com/myProject/)
- [css](https://yanhaijing.com/categories/#css-ref)[18](https://yanhaijing.com/categories/#css-ref)
- [css](https://yanhaijing.com/tags/#css-ref)[19](https://yanhaijing.com/tags/#css-ref)
- [← Previous](https://yanhaijing.com/javascript/2013/12/28/demystifying-this-in-javascript/)
- [Archive](https://yanhaijing.com/archive/)
- [Next →](https://yanhaijing.com/javascript/2014/01/05/exploring-the-abyss-of-null-and-undefined-in-javascript/)

[justjavac](http://justjavac.com/)on 13 May 2014

好长啊。

[颜海镜](http://yanhaijing.com/)on 13 May 2014

还没搞完呢，锚点还没加呢 完整教程这是 挤眼

[CrispElite](http://t.qq.com/lun549936800)on 17 May 2014

注释都写了你还说不解释 哈哈

[颜海镜](http://yanhaijing.com/)on 17 May 2014

呵呵

[大叔夜5郎](http://www.douban.com/people/61412889/)on 19 May 2014

顶一个！超赞的！ 作者不但技术过关 ， 而且描述清晰！！！ good

[幽潭莲花](http://weibo.com/2632496527)on 19 May 2014

我想说 我和作者是认识的， 不但代码写得好 而且还是大帅哥哦。

[鏾步的魚](http://weibo.com/wsluyu2011)on 19 May 2014

赞

[颜海镜](http://yanhaijing.com/)on 19 May 2014

鼓掌

[颜海镜](http://yanhaijing.com/)on 19 May 2014

害羞

[yanlinpu](http://t.qq.com/Y---L---P)on 29 May 2014

思考

[颜海镜](http://yanhaijing.com/)on 30 May 2014

呵呵

[颜海镜](http://yanhaijing.com/)on 05 Jun 2014

全面兼容多种中断了，手机上也能阅读

[张驰Terry](http://weibo.com/terrychinaz)on 05 Jun 2014

赞赞赞

[回眸是谁人](http://weibo.com/isayme)on 12 Jun 2014

果然又涨姿势了

[戴夏清](http://t.qq.com/gelin8)on 12 Jun 2014

织

[戴夏清](http://t.qq.com/gelin8)on 12 Jun 2014

神马

[颜海镜](http://yanhaijing.com/)on 13 Jun 2014

加油

[颜海镜](http://yanhaijing.com/)on 13 Jun 2014

呵呵

[颜海镜](http://yanhaijing.com/)on 04 Jul 2014

赞一个 互粉

[颜海镜](http://yanhaijing.com/)on 05 Jul 2014

呵呵

[颜海镜](http://yanhaijing.com/)on 10 Jul 2014

赞

[zhj](http://drownincodes.sinaapp.com/)on 11 Jul 2014

“表达式产生值。他们通常位于赋值操作的邮编”<-错别字请修正

[zhj](http://drownincodes.sinaapp.com/)on 11 Jul 2014

“有很多符合赋值操作符”<-再次错别字

[颜海镜](http://yanhaijing.com/)on 12 Jul 2014

thanks 已更改，见 http //[yanhaijing.com/basejs/](http://yanhaijing.com/basejs/)

[人长的实在可以吗](http://weibo.com/2437413481)on 12 Jul 2014

第三部分在这里：高效jQuery的奥秘 链接失效。

另外 JavaScript DOM 高级程序设计与 JavaScript DOM 编程艺术 也是两本好的书，里面的设计理念非常值得推崇。

[人长的实在可以吗](http://weibo.com/2437413481)on 12 Jul 2014

一个人的思想往往能让你走的更远。现在很少能找到高质量持续稳定更新的博客了。

[颜海镜](http://yanhaijing.com/)on 13 Jul 2014

感谢支持，博主会继续努力的 兔子

[颜海镜](http://yanhaijing.com/)on 13 Jul 2014

首先改写你的阅读，并提出宝贵意见，以更正，多谢，另外提到的两本书一非常不错

[颜海镜](http://yanhaijing.com/)on 18 Jul 2014

太开心 赞一个 织 扩散

[星夜](https://yanhaijing.com/css/2014/01/04/the-30-css-selectors-you-must-memorize/)on 25 Jul 2014

楼主，请问：function Dog(name){

Animal.call(this,name);

}

Animal.call这个是什么意思？？？？？

谢谢你

[颜海镜](http://yanhaijing.com/)on 25 Jul 2014

call是js中函数特有的方法，可以改变函数的this上下文

[星夜](https://yanhaijing.com/css/2014/01/04/the-30-css-selectors-you-must-memorize/)on 25 Jul 2014

原来如此，谢谢，本文写的通俗易懂，讲的很细。赞一个

[颜海镜](http://yanhaijing.com/)on 27 Jul 2014

感谢支持 同样可以改变this上下文的还有 apply，和es5 新增的 bind，jquery中有proxy

[颜海镜](http://yanhaijing.com/)on 29 Jul 2014

http //[yanhaijing.com/inverter](http://yanhaijing.com/inverter) 我在变色方块小游戏中，逆天用了14次点击，通过了第4关，你，你，你快快来挑战我吧 颜海镜

[颜海镜](http://yanhaijing.com/)on 29 Jul 2014

http //[yanhaijing.com/inverter](http://yanhaijing.com/inverter) 我在变色方块小游戏中，逆天用了33次点击，通过了第5关，你，你，你快快来挑战我吧 颜海镜 可怜

[GitHub家园](http://weibo.com/githubchina)on 29 Jul 2014

http //[yanhaijing.com/inverter](http://yanhaijing.com/inverter) 我在变色方块小游戏中，逆天用了1次点击，通过了第1关，你，你，你快快来挑战我吧 颜海镜

[邬畏畏](http://weibo.com/wsoft)on 07 Aug 2014

思考 又要开始了解掌握新标准的东东了，所以工程师要配备营养师、养生医师、运动教练。

[颜海镜](http://yanhaijing.com/)on 07 Aug 2014

嗯，哈哈

[观心自在](http://www.guanxinzizai.com/62.htm)on 14 Aug 2014

http //[yanhaijing.com/inverter](http://yanhaijing.com/inverter) 我在变色方块小游戏中，逆天用了1次点击，通过了第20关，你，你，你快快来挑战我吧 可怜

[颜海镜](http://yanhaijing.com/)on 14 Aug 2014

亲 改的数据吧 弱