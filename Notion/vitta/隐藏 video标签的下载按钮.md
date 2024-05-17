在 `cordova-plugin-inappbrowser`插件中隐藏 `Android` 的 `webView`里的 `<video>`标签：

```Plain
 let webView = window.cordova.InAppBrowser.open(fileUrl, '_blank', 'location=yes,enableViewportScale=yes')
    if (window.device.platform === 'Android') {
      webView.addEventListener('loadstop', function () {
        webView.executeScript({ code: 'var videos = document.getElementsByTagName(\\'video\\');' +
        'HTMLCollection.prototype.toArray=function(){return [].slice.call(this); };' +
       'videos.toArray().forEach(function(item){item.controlsList.add(\\'nodownload\\');});' }, function (param) {
          console.log(param)
          console.log('回调')
        })
      })
    }
```