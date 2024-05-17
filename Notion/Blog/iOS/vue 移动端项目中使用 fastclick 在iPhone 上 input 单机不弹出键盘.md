> 本文由 简悦 SimpRead 转码

1、在 vue 项目中安装 fastclick 插件

```Plain
npm install --save fastclick
```

2、在 main.js 中引入并绑定到 body

```Plain
import  FastClick  from  'fastclick'

FastClick.attach(document.body);
```

3、在项目中安装 fastclick 成功后测试会遇到以下问题：

- os input 点击不灵敏  
    解决方法：  
    [vue 项目中使用 fastclick 时 ios input 点击不灵敏](https://www.jianshu.com/p/0df7a6f48c8a)

```Plain
FastClick.prototype.focus = function (targetElement) {
  var length;

  var deviceIsWindowsPhone = navigator.userAgent.indexOf("Windows Phone") >= 0;
  var deviceIsIOS = /iP(ad|hone|od)/.test(navigator.userAgent) && !deviceIsWindowsPhone;  
    //兼容处理:在iOS7中，有一些元素（如date、datetime、month等）在setSelectionRange会出现TypeError    
    //这是因为这些元素并没有selectionStart和selectionEnd的整型数字属性，所以一旦引用就会报错，因此排除这些属性才使用setSelectionRange方法
  if ( deviceIsIOS && targetElement.setSelectionRange && targetElement.type.indexOf('date') !== 0 && targetElement.type !== 'time' && targetElement.type !== 'month' && targetElement.type !== 'email') { 
    length = targetElement.value.length; 
    targetElement.setSelectionRange(length, length);//修复bug ios 11.3不弹出键盘，这里加上聚焦代码，让其强制聚焦弹出键盘    
    targetElement.focus(); 
  } else { 
    targetElement.focus(); 
  }
}
```

- os 软键盘关闭后 页面不会回弹  
    解决方法：  
    [解决 IOS 中 input 失焦后，页面上移，点击不了问题](https://segmentfault.com/a/1190000018028182?utm_source=tag-newest)

```Plain
var u = navigator.userAgent;
      var flag;
      var timer;
      var isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/);
      if (isIOS) {
        document.body.addEventListener('focusin', () => {  //软键盘弹起事件
          flag = true;
          clearTimeout(timer);
        })
        document.body.addEventListener('focusout', () => { //软键盘关闭事件
          flag = false;
          if (!flag) {
            timer = setTimeout( ()=> {
              window.scrollTo({ top: 0, left: 0, behavior: "smooth" })//重点  =======当键盘收起的时候让页面回到原始位置(这里的top可以根据你们个人的需求改变，并不一定要回到页面顶部)
            }, 200);
          } else {
            return false;
          }
        })
      } else {
        return false;
      }
```