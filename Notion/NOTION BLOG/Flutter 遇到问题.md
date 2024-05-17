---
type: Post
status: Published
date: 2023-07-07
tags:
  - 开发
category: Flutter
---
## WebView X 问题

- WebViewX 在web上层的组件不能点:

在需要点击的组件上裹上 [WebViewAware](https://github.com/adrianflutur/webviewx/blob/main/example/lib/helpers.dart)

- WebViewX 在 手机上不能滚动缩放:

```Dart
// 添加这个属性
mobileSpecificParams: MobileSpecificParams(
          mobileGestureRecognizers: Set()
            ..add(
              Factory<VerticalDragGestureRecognizer>(
                () => VerticalDragGestureRecognizer(),
              ),
            )
            ..add(
              Factory<TapGestureRecognizer>(
                () => TapGestureRecognizer(),
              ),
            )
            ..add(
              Factory<LongPressGestureRecognizer>(
                () => LongPressGestureRecognizer(),
              ),
            )),
```

  

## Flutter 3 textDirection 问题

```Dart
import 'dart:ui' as ui;

textDirection: ui.TextDirection.rtl,
```

  

## showModalBottomSheet dismiss event

```Dart
void _showModal() {
    Future<void> future = showModalBottomSheet<void>(
      context: context,
      builder: (BuildContext context) {
        return Container(height: 260.0, child: Text('I am text'));
      },
    );
    future.then((void value) => _closeModal(value));
}
void _closeModal(void value) {
// 关闭的时候会调用
    print('modal closed');
}
```

  

## Flutter SingleChildScroll 在 web 里横向不能用鼠标拖动

添加 `scrollBehavior`

```Dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      scrollBehavior: MaterialScrollBehavior().copyWith(
        dragDevices: {PointerDeviceKind.mouse, PointerDeviceKind.touch, PointerDeviceKind.stylus, PointerDeviceKind.unknown},
      ),
```

  

## Flutter html 和 canvast 字体不一样

需要加上:

```Dart
TextStyle(
    fontFeatures: const [FontFeature.proportionalFigures()],
  ),
```

## FCM 推送问题

- iOS 可以后台收到推送，但是不会触发接收的事件.
    - [有说是内容需要特殊格式，待测试](https://stackoverflow.com/questions/72882308/firebasemessaging-onbackgroundmessage-is-not-invoked-when-my-app-is-on-backgroun)
- iOS 前台可以触发接收事件，但是不会显示通知
    - 可以使用flutter_local_nofity 在前台接收到通知的时候创建一个本地的
- 三星手机的推送可以是app 的icon, Pixel 的不可以
    
    - 貌似是需要一个透明背景白色的图片，然后用 [https://romannurik.github.io/AndroidAssetStudio/icons-notification.html](https://romannurik.github.io/AndroidAssetStudio/icons-notification.html) 制作icon, 具体方法可以参考 [https://github.com/flutter/flutter/issues/17941#issuecomment-622268132](https://github.com/flutter/flutter/issues/17941#issuecomment-622268132)