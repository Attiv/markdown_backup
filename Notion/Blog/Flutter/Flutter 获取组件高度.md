```Dart
GlobalKey searchBayKey = new GlobalKey();

initState() {
  WidgetsBinding.instance.addPostFrameCallback((_) {
      _findRenderObject();
    });
}

void _findRenderObject() {
    RenderObject? renderObj = searchBayKey.currentContext?.findRenderObject();
    if (renderObj == null) {
      return;
    }
    RenderBox renderBox = renderObj as RenderBox;
    Offset? offset = renderBox?.localToGlobal(Offset.zero);

    setState(() {
      _searchAreaBottomHeight = (offset?.dy ?? 0) + (renderBox.size.height);
    });
    VLog(_searchAreaBottomHeight);
  }
```