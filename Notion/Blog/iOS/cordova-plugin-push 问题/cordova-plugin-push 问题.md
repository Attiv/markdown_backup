- iOS 前台收不到推送问题
    - 格式要这样，加上content_available: true 才行
        
        ![[/Untitled 34.png|Untitled 34.png]]
        
    - `(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {` 里要修改, 这个前台不走
        
        ![[/Untitled 1 7.png|Untitled 1 7.png]]