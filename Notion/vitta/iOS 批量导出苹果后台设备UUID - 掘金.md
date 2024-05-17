[不知蜕变的挣扎](https://juejin.im/user/57762ce12e958a22d8906d50)

2019年09月05日阅读 5

# iOS 批量导出苹果后台设备UUID

# 工具：

1.Google Chrome 浏览器

2.需要导出设备的苹果账号

# 步骤

# 1.使用Google Chrome进入需要导出设备的列表页

[1_3](https://www.notion.soiOS%20%E6%89%B9%E9%87%8F%E5%AF%BC%E5%87%BA%E8%8B%B9%E6%9E%9C%E5%90%8E%E5%8F%B0%E8%AE%BE%E5%A4%87UUID%20-%20%E6%8E%98%E9%87%91.resources/1_3)

# 2.右键网页，点击检查

[1](https://www.notion.soiOS%20%E6%89%B9%E9%87%8F%E5%AF%BC%E5%87%BA%E8%8B%B9%E6%9E%9C%E5%90%8E%E5%8F%B0%E8%AE%BE%E5%A4%87UUID%20-%20%E6%8E%98%E9%87%91.resources/1)

# 3.点击Sources,新建一个文件

[1_5](https://www.notion.soiOS%20%E6%89%B9%E9%87%8F%E5%AF%BC%E5%87%BA%E8%8B%B9%E6%9E%9C%E5%90%8E%E5%8F%B0%E8%AE%BE%E5%A4%87UUID%20-%20%E6%8E%98%E9%87%91.resources/1_5)

# 4.写入代码

```Plain
jsvar list = document.querySelectorAll(".infinite-scroll-component .row");
var cout = 0;
list.forEach(row=>{
    var children = row.children;
    var uuid = children[1].innerText;
//     var name = children[0].innerText; //名称
//     var type = children[2].innerText; //类型
    console.log(uuid + ' ' + 'Name'+cout + ' ' + 'ios');
    cout++;
}
);
复制代码
```

[1_1](https://www.notion.soiOS%20%E6%89%B9%E9%87%8F%E5%AF%BC%E5%87%BA%E8%8B%B9%E6%9E%9C%E5%90%8E%E5%8F%B0%E8%AE%BE%E5%A4%87UUID%20-%20%E6%8E%98%E9%87%91.resources/1_1)

# 5.点击运行

[1_4](https://www.notion.soiOS%20%E6%89%B9%E9%87%8F%E5%AF%BC%E5%87%BA%E8%8B%B9%E6%9E%9C%E5%90%8E%E5%8F%B0%E8%AE%BE%E5%A4%87UUID%20-%20%E6%8E%98%E9%87%91.resources/1_4)

# 6.在log中获取需要的数据

[1_2](https://www.notion.soiOS%20%E6%89%B9%E9%87%8F%E5%AF%BC%E5%87%BA%E8%8B%B9%E6%9E%9C%E5%90%8E%E5%8F%B0%E8%AE%BE%E5%A4%87UUID%20-%20%E6%8E%98%E9%87%91.resources/1_2)

# 7.复制到文件中即可，然后按照苹果的要求导入即可，可参考链接:[导入设备](https://www.jianshu.com/p/fed39cef248a)

[1_6](https://www.notion.soiOS%20%E6%89%B9%E9%87%8F%E5%AF%BC%E5%87%BA%E8%8B%B9%E6%9E%9C%E5%90%8E%E5%8F%B0%E8%AE%BE%E5%A4%87UUID%20-%20%E6%8E%98%E9%87%91.resources/1_6)