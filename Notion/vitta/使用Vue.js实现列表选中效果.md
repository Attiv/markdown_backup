# [使用Vue.js实现列表选中效果](http://xlbd.me/vue-js-selected-highlight/)

__[小蘿蔔丁](http://xlbd.me/author/xiaoluoboding/)__3 years ago(2016-04-25)__[Vue.js](http://xlbd.me/tag/vue/)

实际项目中，我们会遇到很多类似的需求，一个列表，需要点击其中一条高亮显示。熟悉JQuery的同学说这个太简单了。可以给这个选中的element设置一个active的class。配合Css样式，让active有选中高亮效果。但是谁说一定要用到jQuery呢。

最近在做的项目中，我尝试脱离JQuery，绕过JQuery，我所接触的大部分项目中好像不使用JQuery无法进行开发一样。它确实给开发者提供了太多便利。以至于大部分web网站都依赖它运行着。据[w3Techs统计](http://w3techs.com/technologies/details/js-jquery/all/all)，JQuery的市场份额高达94.9%，是时候脱离JQuery的束缚了。使用Vue.js更简洁，快速地实现。

选中效果实现的核心实现逻辑是拷贝一份当前状态作为快照。比对列表的**快照**和**当前**的唯一索引，如果相同则视为选中。

### **Demo**

[![](https://www.notion.so%E4%BD%BF%E7%94%A8Vue.js%E5%AE%9E%E7%8E%B0%E5%88%97%E8%A1%A8%E9%80%89%E4%B8%AD%E6%95%88%E6%9E%9C.resources/selected-highlight.gif)](https://www.notion.so%E4%BD%BF%E7%94%A8Vue.js%E5%AE%9E%E7%8E%B0%E5%88%97%E8%A1%A8%E9%80%89%E4%B8%AD%E6%95%88%E6%9E%9C.resources/selected-highlight.gif)

### **使用Vue.js实现**

<divid="app">

<divclass="collection">

<ahref="#!"class="collection-item"

v-for="gameName in gameNames"

@click="selected(gameName)"

:class="{active: activeName == gameName}">{{gameName}}</a>

</div>

</div>

newVue({

el: "\#app",

data: {

gameNames: ['魔兽世界', '暗黑破坏神Ⅲ', '星际争霸Ⅱ', '炉石传说', '风暴英雄',

'守望先锋'

],

activeName: ''

},

methods: {

selected: function(gameName) {

this.activeName = gameName

}

}

})

**发表于：****2016-04-25****作者：小蘿蔔丁**

躲在静好的时光里，认真地学习着遗忘，一个人也要清醒决绝地走下去。

[Github](https://github.com/xiaoluoboding)[新浪微博](http://weibo.com/17064042)[SegmentFault](https://segmentfault.com/u/xlbd)[掘金专栏](https://juejin.im/user/5624b5fa60b296e5979b7284/posts)