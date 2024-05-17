1. 在 `app.dart` 里新建: `RouteObserver<PageRoute> routeObserver = RouteObserver<PageRoute>();`
2. 在用到的类里 `with RouteAware`

```Dart
class A extends State<B>
    with RouteAware {
	@override
  void initState() {
    super.initState();
  }

  @override
  void didChangeDependencies() {
    routeObserver.subscribe(this, ModalRoute.of(context) as PageRoute<dynamic>);
    super.didChangeDependencies();
  }

  @override
  void didPush() {
    // 进入到该页面
  }

  @override
  void didPopNext() {
    // 从其他页面返回到该页面
  }

  @override
  void didPushNext() {
    // 进入其他页面
  }

  @override
  void didPop() {
    // 离开该页面
  }

  @override
  void dispose() {
    routeObserver.unsubscribe(this);
    super.dispose();
  }
}
```