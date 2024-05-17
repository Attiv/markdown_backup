# 刷新数据的方法

- `widgetPerformUpdateWithCompletionHandler`
- `viewWillAppear` （调用比上面第一个频繁）

  

# 数据存储

需要使用带group的

```JavaScript
//在主应用中存储数据：
-(void)viewDidLoad
[super viewDidLoad];
self.view.backgroundColor=[UIColor yellowColor]
NSUserDefaults *sharedData = [[NSUserDefaults alloc]
initWithSuiteName:@"group.widge.testGroup"];
[sharedData setValue:@"我叫小组件"forKey:@"name"];
[sharedData synchronize];

//在widget中读取数据：
//和主应用的数据共享，获取主应用里的数据
NSUserDefaults *sharedData = [[NSUserDefaults alloc]
initwithSuiteName: @"group.widge.testGroup"];
NSString *name = [sharedData objectForKey:@"name"];
```