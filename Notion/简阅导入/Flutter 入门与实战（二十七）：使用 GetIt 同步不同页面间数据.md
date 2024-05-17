- 详情页面界面构建；
- 更新详情查看次数接口实现；
- GetIt 简介；
- 使用 GetIt 注册全局对象；
- 使用 GetIt 实现页面间的数据同步。

### 详情页面

详情页面我们显示动态的标题、查看次数、图片和内容。最简单的方式是使用 Column 组件将所有内容依次包裹。但是，考虑内容实际会很长（也可能是富文本），因此使用滚动组件包裹更合适，这里还是使用 `CustomerScrollView` 来，相比普通的 `ScrollView` 来说，`CustomerScrollView` 使用 `Sliver` 子组件，滑动性能会更高也更顺畅，就如同某巧克力广告说的一样——纵享丝滑。

页面本身比较简单，就不多介绍了，具体的页面层级如下所示。关于 `CustomerScrollView`可以参考之前的文章：[Flutter 入门与实战（十二）：利用 CustomScrollView 实现更有趣的滑动效果](https://juejin.cn/post/6971427026754502664)。

- `CustomScrollView`
    - `slivers`
        - 标题：使用 `Container` 包裹以便调整布局。
        - 查看次数：和列表的查看次数类似。
        - 图片：为了避免图片占据太高的高度，将图片高度限制在 240。
        - 内容：和标题类似，只是字体调小了 2 号

以上的 `slivers` `的子组件的内容都使用SliverToBoxAdapter转换为` `Sliver`。最终界面看后面的动图即可。

### 详情查看次数更新

当我们进入详情页面时，需要向后端提交更新查看次数的接口。注意，有些应用处理是后端直接在获取详情接口时往数据库增加查看数。虽然这样可以减少请求次数，但是后端处理存在缺陷是会把调用详情接口直接当做查看详情页面进行统计，结果在其他地方获取详情时（比如编辑接口）可能导致多统计，行业黑话称之为 “**刷流量**”。

使用前端更新查看次数可以做到更精准的控制，比如我们可以设置在页面停留多长时间才是有效查看，或者滑动到页面底部才算有效查看等等。

更新查看次数的接口地址为：`http://localhost:3900/api/dynamics/view/:id`，记得拉取最新的代码运行。我们在获取详情接口成功后再进行查看次数更新。更新查看次数不是很重要的逻辑，出现错误时无需给予提醒（避免给用户造成困惑），这里只是打印异常信息，用于开发过程中排查问题。实际生产过程可以将异常信息上传到异常监控后台。

```Plain
if (response.statusCode == 200) {
  setState(() {
    _dynamicEntity = DynamicEntity.fromJson(response.data);
  });
  _updateViewCount();
}
//...

void _updateViewCount() async {
  try {
    var response = await DynamicService.updateViewCount(_dynamicEntity.id);
    if (response.statusCode == 200) {
      setState(() {
        _dynamicEntity.viewCount = response.data['viewCount'];
        GetIt.instance.get<DynamicListener>().dynamicUpdated(
              _dynamicEntity.id,
              _dynamicEntity,
            );
      });
    }
  } catch (e) {
    print(e.toString());
  }
}
复制代码
```

### GetIt 简介

`GetIt` 本身是一个容器管理插件，其最初的设计是用于完成依赖注入 DI 和 IOC 容器的功能，有点类似 Java Spring 的 Bean 容器。由于容器中的对象是全局的，因此可以用来做数据同步，也是 Flutter 官方推荐的状态管理容器之一。另一个常用的状态管理插件是 `Provider`，后面我们涉及到状态管理的时候再来讲述。

所谓的容器，本质上就是一个全局`Map`对象，可以往里面存入对象后，在需要用的时候直接取出，而不需要每个使用者都自己创建对象，也实现了对象之间的解耦。

GetIt 的基础用法很简单，如下所示。如果考虑启动时避免占用太多资源，也可以使用 lazy 懒加载的方式，懒加载时传入的是一个构建对象的方法，在取出对象的时候，如果容器中没有该对象，则使用构建对象的方法创建一个，如果已经有了就直接返回。

注意，GetIt 有很多个版本，对 Flutter 的 最低 SDK 版本有要求，我们当前使用的 SDK 版本是 2.0.6，因此最高只能选择 4.0.3 版本（最新版本是 7.1.2，需要 2.12.x 以上版本）。

```Plain
// 注册对象：一般是单例
GetIt.instance.registerSingleton<T>(T object);
// 懒加载方式注册
GetIt.instance.registerLazySingleton<T>(FactoryFunc<T> func)
// 获取容器中的对象
GetIt.instance.get<T>();
复制代码
```

### 注册动态改变监听对象

当动态新增，或者动态内容发生改变时，我们需要更新列表。最简单的方式是通知列表刷新，但是那样的增加了网络请求。我们可以直接修改列表的数据来完成列表的更新。考虑到不仅仅是动态列表页需要更新（比如动态嵌入到其他页面中），我们把动态更新的方法抽象为接口，只要是实现了对应接口的对象都可以在动态发生变化时调用对应的接口更新——即所谓的面向接口编程。

新增一个 `dynamic_listener.dart` 文件，定义一个接口抽象类`DynamicListener`。在列表页面的`_DynamicPageState`中实现对应的接口。

```Plain
import 'package:home_framework/models/dynamic_entity.dart';

abstract class DynamicListener {
  void dynamicUpdated(String id, DynamicEntity updatedDynamic);

  void dynamicAdded(DynamicEntity newDynamic);
}
复制代码
```

_DynamicPageState 使用 implements 关键字（也可以使用 with 关键字）实现 DynamicListener 接口的两个方法：

- 新增响应方法：当有新增动态时，将新增动态插入到开头处；
- 更新方法：使用新的动态替换旧的动态数据。

同时，在`initState`方法中注册自身到 GetIt 容器。

```Plain
class _DynamicPageState extends State<DynamicPage> implements DynamicListener {
    // ...

  @override
  void initState() {
    super.initState();
    // 注册到 GetIt容器
    GetIt.instance.registerSingleton<DynamicListener>(this);
  }

  void dynamicUpdated(String id, DynamicEntity updatedDynamic) {
    int index = _listItems.indexWhere((element) => element.id == id);
    if (index != -1) {
      setState(() {
        _listItems[index] = updatedDynamic;
      });
    }
  }

  void dynamicAdded(DynamicEntity newDynamic) {
    setState(() {
      _listItems.insert(0, newDynamic);
    });
  }

  // ...
}
复制代码
```

### 页面间数据更新

有了 GetIt 容器，因为可以直接从容器中获取动态列表状态管理对象，在其他页面处理就比较简单了，逻辑分别如下：

- 新增页面：新增成功后调用`dynamicAdded`方法更新列表页面；
- 编辑页面：编辑成功后调用`dynamicUpdated`方法更新列表页面；
- 详情页面：更新查看次数后调用`dynamicUpdated`方法更新列表页面。

三个页面的代码分别如下：

```Plain
//新增页面
var response = await DynamicService.post(newFormData);
if (response.statusCode == 200) {
  Dialogs.showInfo(context, '添加成功');
  GetIt.instance
      .get<DynamicListener>()
      .dynamicAdded(DynamicEntity.fromJson(response.data));
  Navigator.of(context).pop();
}
//-------------------------------------
//编辑页面
if (response.statusCode == 200) {
  Dialogs.showInfo(context, '保存成功');
  //处理成功更新后的业务
  _handleUpdated(newFormData);
  Navigator.of(context).pop();
}

// 处理更新，如果图片更新了才更新动态图片内容
void _handleUpdated(Map<String, String> newFormData) {
  _dynamicEntity.title = newFormData['title'];
  _dynamicEntity.content = newFormData['content'];
  if (newFormData.containsKey('imageUrl')) {
    _dynamicEntity.imageUrl = newFormData['imageUrl'];
  }
  GetIt.instance.get<DynamicListener>().dynamicUpdated(
      _dynamicEntity.id,
      _dynamicEntity,
  );
}

//-------------------------------------
//详情页面
void _updateViewCount() async {
  try {
    var response = await DynamicService.updateViewCount(_dynamicEntity.id);
    if (response.statusCode == 200) {
      setState(() {
        _dynamicEntity.viewCount = response.data['viewCount'];
        GetIt.instance.get<DynamicListener>().dynamicUpdated(
              _dynamicEntity.id,
              _dynamicEntity,
            );
      });
    }
  } catch (e) {
    print(e.toString());
  }
}
复制代码
```

### 运行效果

### 总结

本篇完成了整个动态管理的业务逻辑，包括了新增、删除、编辑、查看次数等功能。通过 GetIt 容器管理插件及接口定义，可以很简单快速地完成页面之间的数据同步。从整个系列也可以看到，我们在网络请求这块的代码存在如下问题：

- 重复代码很多：比如 `try...catch` 代码块；
- 暴露了 Dio 的细节；
- 界面参与了业务对象的构建，没有与业务逻辑分离。

接下来的篇章我们将逐步完成对 Dio 的封装和网络请求部分代码的重构。 > 本文由简悦 SimpRead 转码