> 本文由 简悦 SimpRead 转码

### 在 Flutter 中没有 removeView，addView 这种方式控制 Widget Tree 中的组件

### 场景： 根据状态显示隐藏 widget

### 解决方案 1（占位）：

```Plain
Widget _buildA() {
  var content;
  if (data?.isNotEmpty) {
    //如果数据不为空，则显示Text
      content = new Text('数据不为空');
  } else {
   //当数据为空我们需要隐藏这个Text
   //我们又不能返回一个null给当前的Widget Tree
   //只能返回一个长宽为0的widget占位
      content = new Container(height:0.0,width:0.0);
  }
  return content;
}
```

### 解决方案 2(透明度)：

```Plain
class _HideAndShowPageState extends State<HideAndShowPage> {
bool visible = true;

@override
Widget build(BuildContext context) {
  return new Scaffold(
    appBar: new AppBar(
      title: new Text('widget显示与隐藏'),
      centerTitle: true,
    ),
    body: new ListView(
      children: <Widget>[
        new Padding(
          padding: const EdgeInsets.only(left: 10.0, top: 10.0, right: 10.0),
          child: new RaisedButton(
              textColor: Colors.black,
              child: new Text(visible ? '隐藏B    显示A' : '隐藏A   显示B'),
              onPressed: () {
                visible = !visible;
                setState(() {});
              }),
        ),
        new Padding(
          padding: const EdgeInsets.only(left: 10.0, top: 10.0, right: 10.0),
          child: new Stack(
            children: <Widget>[
              new TestAWidget(
                visible: visible,
              ),
              new TestBWidget(
                visible: !visible,
              ),
            ],
          ),
        ),
      ],
    ),
  );
}
}

class TestAWidget extends StatelessWidget {
final bool visible;

const TestAWidget({Key key, this.visible}) : super(key: key);

@override
Widget build(BuildContext context) {
  return AnimatedOpacity(
    duration: Duration(milliseconds: 300),
    opacity: visible ? 1.0 : 0.0,
    child: new Container(
      color: Colors.blue,
      height: 100.0,
      child: new Center(
        child: new Text('TestAWidget'),
      ),
    ),
  );
}
}

class TestBWidget extends StatelessWidget {
final bool visible;

const TestBWidget({Key key, this.visible}) : super(key: key);

@override
Widget build(BuildContext context) {
  return AnimatedOpacity(
    duration: Duration(milliseconds: 300),
    opacity: visible ? 1.0 : 0.0,
    child: new Container(
      color: Colors.green,
      height: 100.0,
      child: new Center(
        child: new Text('TestBWidget'),
      ),
    ),
  );
}
}
```

### 解决方案 3(Offstage)：

```Plain
class TestCWidget extends StatelessWidget {
 final bool visible;

 const TestCWidget({Key key, this.visible}) : super(key: key);

 @override
 Widget build(BuildContext context) {
   return new Offstage(
     offstage: visible,
     child:new Container(
       color: Colors.orange,
       height: 100.0,
       child: new Center(
         child: new Text('TestCWidget'),
       ),
     ),
   );
 }
}
```

[![](http://upload-images.jianshu.io/upload_images/2751425-45b5af208f5b415f.gif)](http://upload-images.jianshu.io/upload_images/2751425-45b5af208f5b415f.gif)

showandhide.gif

### ps：如果还有别的方案，麻烦告知下，谢谢！

### 已有项目集成到 Flutter 代码已经上传到我的 [GITHUB](https://github.com/zhujian1989/MyArchitecture)

### 知乎日报 Flutter 版代码已经上传到我的 [GITHUB](https://github.com/zhujian1989/ZhihuDailyPurifyByFlutter)

### 基础学习过程中的代码都放在 [GITHUB](https://github.com/zhujian1989/flutter_study)

# 每天学一点，学到 Flutter 发布正式版！