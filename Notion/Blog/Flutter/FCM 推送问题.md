- iOS 可以后台收到推送，但是不会触发接收的事件.
    - [有说是内容需要特殊格式，待测试](https://stackoverflow.com/questions/72882308/firebasemessaging-onbackgroundmessage-is-not-invoked-when-my-app-is-on-backgroun)
- iOS 前台可以触发接收事件，但是不会显示通知
    - 可以使用flutter_local_nofity 在前台接收到通知的时候创建一个本地的
- 三星手机的推送可以是app 的icon, Pixel 的不可以
    
    - 貌似是需要一个透明背景白色的图片，然后用 [https://romannurik.github.io/AndroidAssetStudio/icons-notification.html](https://romannurik.github.io/AndroidAssetStudio/icons-notification.html) 制作icon, 具体方法可以参考 [https://github.com/flutter/flutter/issues/17941#issuecomment-622268132](https://github.com/flutter/flutter/issues/17941#issuecomment-622268132)