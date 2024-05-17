  

使用场景：由于是版本迭代，之前用的symfony+ twig偶尔引入Vue，第二版，直接换下了twig，但是只是部分界面，老界面还是要用的，为了让客户感觉，哇，好快啊，然后采用了Quasar, 外层的框是Quasar写的，而里面套的是iframe，对之前的大佬也是佩服啊，表示并不怎么会用iframe。然后就出现了内部iframe界面更新用户信息，框架头部用户信息不更新的问题。

**几种方式**

- 三秒一刷新(不会尝试这种，如果时间紧急可以)
- webSocket (建立长链接，监听数据变化，比较菜可能需要花些时间)
- 监听storge(摸索了半天选用了这种方式)实现如下：

1. 需要更新信息的js代码处

```Plain
  localStoage.setItem(key, true)
```

1. 在你自己写的大框架vue文件里监听

```Plain
  window.addEventListener('storage', function () {
      if (localStorage.getItem('updatePic') === 'true') {
        setTimeout(() => {
          this.storageHandler()
        }, 2000)
      }
    }.bind(this), false)
```

1. 调api更新信息(头部头像，用户名等)

```Plain
    storageHandler()
```