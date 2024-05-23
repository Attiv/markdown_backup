

- **Array+Ex.swift**
  - [`func randomItem() -> Element?`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/Array%2BEx.swift#L14) - 从数组中随机获取一个元素。
    ```swift
    let randomElement = yourArray.randomItem()
    ```

  - [`func subArray(from index: Int, length: Int) -> [Element]`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/Array%2BEx.swift#L29) - 获取数组的子数组，指定起始索引和长度。
    ```swift
    let subArray = yourArray.subArray(from: startIndex, length: subArrayLength)
    ```

- **Date+Ex.swift**
  - [`func string(_ dateFormat: String = "yyyy-MM-dd HH:mm:ss") -> String`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/Date%2BEx.swift#L17) - 将日期转换为字符串，可指定日期格式。
    ```swift
    let dateString = yourDate.string("yyyy-MM-dd")
    ```

- **Dictionary+Ex.swift**
  - [`func jsonString() -> String?`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/Dictionary%2BEx.swift#L13) - 将字典转换为 JSON 字符串。
    ```swift
    if let jsonString = yourDictionary.jsonString() {
        print(jsonString)
    }
    ```

- **String+Ex.swift**
  - [`var isBlank: Bool`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/String%2BEx.swift#L10) - 检查字符串是否为空。
    ```swift
    if yourString.isBlank {
        print("String is blank.")
    }
    ```

  - [`func toDate(_ dateFormat: String = "yyyy-MM-dd HH:mm:ss") -> Date?`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/String%2BEx.swift#L16) - 将字符串转换为日期。
    ```swift
    if let date = yourString.toDate("yyyy-MM-dd") {
        print(date)
    }
    ```

- **UIApplication+Ex.swift**
  - [`class func call(_ phone: String)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UIApplication%2BEx.swift#L11) - 拨打电话。
    ```swift
    UIApplication.call("123-456-7890")
    ```

- **UIColor+Ex.swift**
  - [`convenience init(hexString: String, alpha: CGFloat = 1.0)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UIColor%2BEx.swift#L22) - 通过十六进制字符串创建颜色。
    ```swift
    let color = UIColor(hexString: "#FF0000")
    ```

- **UINavigationController+Ex.swift**
  - [`func popToViewController(ofClass: AnyClass, animated: Bool = true) -> Bool`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UINavigationController%2BEx.swift#L14) - 弹出到指定类型的视图控制器。
    ```swift
    let didPop = navigationController.popToViewController(ofClass: YourViewController.self)
    ```

- **UIView+Ex.swift**
  - [`func addTapGesture(target: Any, action: Selector)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UIView%2BEx.swift#L11) - 为视图添加点击手势。
    ```swift
    yourView.addTapGesture(target: self, action: #selector(handleTap))
    ```

  - [`func addGradientLayer(startColor: UIColor, endColor: UIColor, startPoint: CGPoint, endPoint: CGPoint)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UIView%2BEx.swift#L27) - 为视图添加渐变图层。
    ```swift
    yourView.addGradientLayer(startColor: UIColor.red, endColor: UIColor.blue, startPoint: CGPoint(x: 0, y: 0), endPoint: CGPoint(x: 1, y: 1))
    ```

- **UIViewController+Ex.swift**
  - [`func showAlert(title: String?, message: String?, actions: [UIAlertAction])`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UIViewController%2BEx.swift#L11) - 显示警告弹窗。
    ```swift
    let alert = UIAlertController(title: "Title", message: "Message", preferredStyle: .alert)
    let action = UIAlertAction(title: "OK", style: .default, handler: nil)
    self.showAlert(title: "Title", message: "Message", actions: [action])
    ```

- **WKWebView+Ex.swift**
  - [`func loadUrl(_ url: String)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/WKWebView%2BEx.swift#L14) - 加载网页 URL。
    ```swift
    yourWebView.loadUrl("https://www.example.com")
    ```

- **UIControl+Ex.swift**
  - [`func addAction(for controlEvents: UIControl.Event, action: @escaping () -> Void)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UIControl%2BEx.swift#L12) - 为控件添加动作回调。
    ```swift
    yourControl.addAction(for: .touchUpInside) {
        print("Control tapped")
    }
    ```

- **UILabel+Ex.swift**
  - [`func setLineSpacing(lineSpacing: CGFloat, lineHeightMultiple: CGFloat)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UILabel%2BEx.swift#L14) - 设置标签的行间距和行高倍数。
    ```swift
    yourLabel.setLineSpacing(lineSpacing: 10, lineHeightMultiple: 1.5)
    ```

- **UIScrollView+Ex.swift**
  - [`func scrollToTop(animated: Bool)`](https://github.com/shang1219178163/SwiftExpand/blob/master/Sources/SwiftExpand/Extensions/UIScrollView%2BEx.swift#L12) - 滚动到滚动视图的顶部。
    ```swift
    yourScrollView.scrollToTop(animated: true)
    ```
