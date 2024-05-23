# Flutter MobX  使用

1. 在 `pubspec.yaml` 中加入:
  ```
  dependencies:
    mobx: ^2.0.7+4
    flutter_mobx: ^2.0.6+1
  
  dev_dependencies:
    build_runner: ^2.2.0
    mobx_codegen: ^2.0.7
  ```
  
2. `flutter pub get`
3. 创建一个 store 文件
 ```
 import 'package:mobx/mobx.dart';

// Include generated file
// 必须有，为了生成 .g 文件
part 'counter.g.dart';

// This is the class used by rest of your codebase
// .g 文件会生成 _$Counter
class Counter = _Counter with _$Counter;

final Counter count = Counter();
// The store-class
abstract class _Counter with Store {
  @observable
  int value = 0;

  @action
  void increment() {
    value++;
  }
}
```
> 要注意文件名，有可能会生成不了 .g 文件, 有错误也不会生成
4. 执行 `flutter pub run build_runner build`， 会生成 .g 文件
5. 使用的时候直接 `count.`
6. 组件里使用
 ```
       Observer(
              builder: (_) => Text(
                    '${counter.value}',
                    style: Theme.of(context).textTheme.headline4,
                  ),
            ),
```
这样就会自动刷新数据了
    