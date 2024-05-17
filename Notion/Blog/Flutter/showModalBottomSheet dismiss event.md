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