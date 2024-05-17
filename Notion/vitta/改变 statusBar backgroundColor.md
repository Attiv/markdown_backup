具体看[简书](http://www.jianshu.com/p/5c09c2700038)

```Plain
//设置状态栏颜色
- (void)setStatusBarBackgroundColor:(UIColor *)color {

    UIView *statusBar = [[[UIApplication sharedApplication] valueForKey:@"statusBarWindow"] valueForKey:@"statusBar"];
    if ([statusBar respondsToSelector:@selector(setBackgroundColor:)]) {
        statusBar.backgroundColor = color;
    }
}

- (void)viewDidLoad {
    [super viewDidLoad];

    [self setStatusBarBackgroundColor:[UIColor redColor]];
    self.view.backgroundColor = [UIColor yellowColor];
}
```