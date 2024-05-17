## HookWidget

一般在 `Widget` 中 `class xxx extends HookWidget`

```Dart
class A extends HookWidget {
  A({
    Key? key,
    required this.b,
  }) : super(key: key);

  final String b;

  @override
  Widget build(BuildContext context) {

	}
}
```

## useState

`useState` 用来给变量赋值, 使用的时候用 `value` 就可以 ，省去了 `setState`, 需要放在 `build` 里，不然会报错

```Dart
  @override
  Widget build(BuildContext context) {
		final counter = useState(0); // 默认是0
		return Text(counter.value.toString());
	}
```

因为这个变量 `counter` 是在 `build` 里声明的，所以需要用到这个变量的方法需要在 `build` 里定义

```Dart
  @override
  Widget build(BuildContext context) {
		final counter = useState(0); 
		void _addCounter() {
			counter.value++;
		}
		return Text(counter.value.toString());
	}
```

  

## useContext

```Dart
class MyWidget extends HookWidget {
  Widget build() {
    BuildContext context = useContext() 
    return Container()
  }
}
```

  

## useEffect

类似 `init`

`useEffect` 的第二个参数是一个可选的列表，用于指定依赖项。如果依赖项列表为空，那么 `useEffect` 只会在 `widget` 首次构建时执行一次。如果依赖项列表不为空，那么 `useEffect`会在任何一个依赖项发生变化时重新执行

`useEffect` 的返回值是一个可选的函数，用于清理作用。当 `useEffect` 重新执行或 `widget` 销毁时，清理函数会被调用

```Dart
class MyWidget extends HookWidget {
  Widget build() {
    useEffect(() {
		  // 这里写副作用代码，如根据 count 的值更新标题
		  document.title = 'You clicked $count times';
			return () {
			// 类似dealloc
		    subscription.cancel();
		  };
			}, [count]); // 依赖于 count 的变化
    return Container()
  }
}
```