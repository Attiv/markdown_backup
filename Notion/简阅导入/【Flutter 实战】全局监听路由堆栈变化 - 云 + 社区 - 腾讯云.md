> 本文由 简悦 SimpRead 转码

> 老孟导读：很多时候我们需要监听路由堆栈的变化，这样可以自定义路由堆栈、方便分析异常日志等。

监听路由堆栈的变化使用 **RouteObserver** ，首先在 **MaterialApp** 组件中添加 `navigatorObservers`：

```Dart
void main() {
  runApp(MyApp());
}

RouteObserver<PageRoute> routeObserver = RouteObserver<PageRoute>();

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      ...
      navigatorObservers: [routeObserver],
      home: HomePage(),
    );
  }
}
```

监听页面设置如下：

```Dart
class ARouteObserverDemo extends StatefulWidget {
  @override
  _RouteObserverDemoState createState() => _RouteObserverDemoState();
}

class _RouteObserverDemoState extends State<ARouteObserverDemo> with RouteAware {

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    routeObserver.subscribe(this, ModalRoute.of(context));
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        alignment: Alignment.center,
        child: RaisedButton(
          child: Text('A RouteObserver'),
          onPressed: () {
            Navigator.of(context).pushNamed('/BRouteObserver');
          },
        ),
      ),
    );
  }

  @override
  void dispose() {
    super.dispose();
    routeObserver.unsubscribe(this);
  }

  @override
  void didPush() {
    final route = ModalRoute.of(context).settings.name;
    print('A-didPush route: $route');
  }

  @override
  void didPopNext() {
    final route = ModalRoute.of(context).settings.name;
    print('A-didPopNext route: $route');
  }

  @override
  void didPushNext() {
    final route = ModalRoute.of(context).settings.name;
    print('A-didPushNext route: $route');
  }

  @override
  void didPop() {
    final route = ModalRoute.of(context).settings.name;
    print('A-didPop route: $route');
  }

}
```

其中 didPush、didPushNext、didPopNext、didPop 为路由堆栈变化的回调。

从 A 页面跳转到 ARouteObserverDemo 页面，日志输出如下：

```Dart
flutter: A-didPush route: /ARouteObserver
```

进入此页面只调用了 didPush。

从 ARouteObserverDemo 页面跳转到 BRouteObserverDemo 页面（同 ARouteObserverDemo 页面，设置了监听），日志输出如下：

```Plain
flutter: A-didPushNext route: /ARouteObserver
flutter: B-didPush route: /BRouteObserver
```

先调用了 ARouteObserverDemo 页面的 didPushNext，然后调用了 BRouteObserverDemo 页面的 didPush。

从 BRouteObserverDemo 页面执行 pop 返回 ARouteObserverDemo 页面，日志输出如下：

```Plain
flutter: A-didPopNext route: /ARouteObserver
flutter: B-didPop route: /BRouteObserver
```

先调用了 ARouteObserverDemo 页面的 didPopNext，然后调用了 BRouteObserverDemo 页面的 didPop。

上面的案例仅仅是页面级别的路由堆栈变化，如果想知道整个应用程序路由堆栈变化如何处理？

一种方法是写一个监听路由堆栈的基类，所有页面继承此基类。此方法对源代码的侵入性非常高。

还有一种方法是自定义 RouteObserver，继承 RouteObserver 并重写其中的方法：

```Plain
class MyRouteObserver<R extends Route<dynamic>> extends RouteObserver<R> {
  @override
  void didPush(Route route, Route previousRoute) {
    super.didPush(route, previousRoute);
    print('didPush route: $route,previousRoute:$previousRoute');
  }

  @override
  void didPop(Route route, Route previousRoute) {
    super.didPop(route, previousRoute);
    print('didPop route: $route,previousRoute:$previousRoute');
  }

  @override
  void didReplace({Route newRoute, Route oldRoute}) {
    super.didReplace(newRoute: newRoute, oldRoute: oldRoute);
    print('didReplace newRoute: $newRoute,oldRoute:$oldRoute');
  }

  @override
  void didRemove(Route route, Route previousRoute) {
    super.didRemove(route, previousRoute);
    print('didRemove route: $route,previousRoute:$previousRoute');
  }

  @override
  void didStartUserGesture(Route route, Route previousRoute) {
    super.didStartUserGesture(route, previousRoute);
    print('didStartUserGesture route: $route,previousRoute:$previousRoute');
  }

  @override
  void didStopUserGesture() {
    super.didStopUserGesture();
    print('didStopUserGesture');
  }
}
```

使用：

```Plain
void main() {
  runApp(MyApp());
}

MyRouteObserver<PageRoute> myRouteObserver = MyRouteObserver<PageRoute>();

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      navigatorObservers: [myRouteObserver],
      initialRoute: '/A',
      home: APage(),
    );
  }
}
```

此时从 A 页面 跳转到 B 页面，日志输出如下：

```Plain
flutter: didPush route: MaterialPageRoute<dynamic>(RouteSettings("/B", 来自A), animation: AnimationController\#6d429(▶ 0.000; for MaterialPageRoute<dynamic>(/B))),previousRoute:MaterialPageRoute<dynamic>(RouteSettings("/A", null), animation: AnimationController\#e60f7(⏭ 1.000; paused; for MaterialPageRoute<dynamic>(/A)))
```

本文分享自微信公众号 - 2020-09-17

本文参与[腾讯云自媒体分享计划](https://cloud.tencent.com/developer/support-plan)，欢迎正在阅读的你也加入，一起分享。