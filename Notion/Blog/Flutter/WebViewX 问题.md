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