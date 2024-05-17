具体如下：

```Plain
class Demo1 extends StatefulWidget {
  @override
  _Demo1State createState() => _Demo1State();
}

class _Demo1State extends State<Demo1> {
  GlobalKey _key = GlobalKey();
  num height = 0;

  @override
  Widget build(BuildContext context) {
    return Container(
      key: _key,
      height: height == 0 ? 100 : height,
      child: ...,
    );
  }

  @override
  void didChangeDependencies() {
    WidgetsBinding.instance.addPostFrameCallback(_getContainerHeight);
    super.didChangeDependencies();
  }

  @override
  void didUpdateWidget(Demo1 oldWidget) {
    WidgetsBinding.instance.addPostFrameCallback(_getContainerHeight);
    super.didUpdateWidget(oldWidget);
  }

  _getContainerHeight(_){
    height = _key.currentContext.size.height;
  }
}

复制代码
```

为什么在这两个方法增加事件绑定，可以参考[这里](https://link.juejin.cn/?target=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000015211309)，这里不再累述。 > 本文由简悦 SimpRead 转码