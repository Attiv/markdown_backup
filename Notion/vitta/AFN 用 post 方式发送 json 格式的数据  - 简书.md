> 本文由 简悦 SimpRead 转码， 原文地址 https://www.jianshu.com/p/0ed19c9c4aaa

[![](https://upload.jianshu.io/users/upload_avatars/5818512/ac528289-89e7-4ba2-82f8-c222a96bccd3.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/96/h/96/format/webp)](https://upload.jianshu.io/users/upload_avatars/5818512/ac528289-89e7-4ba2-82f8-c222a96bccd3.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/96/h/96/format/webp)

2017.11.06 10:54:40 字数 48 阅读 2,084

### AFN 用 post 方式发送 json 格式的数据加上下边两句话就行了

session.requestSerializer = [AFJSONRequestSerializer serializer];  
session.responseSerializer = [AFJSONResponseSerializer serializer];  

```Plain
+ (void)postWithURLString:(NSString *)urlString parameters:(NSMutableDictionary *)parameters success:(void (^)(id responseObject))success failure:(void (^)(NSError *error))failure
{
    AFHTTPSessionManager *session = [AFHTTPSessionManager manager];

    session.responseSerializer.acceptableContentTypes = [NSSet setWithObjects:@"application/json", @"text/html", @"text/plain", nil];

    
    
    session.requestSerializer = [AFJSONRequestSerializer serializer];
    session.responseSerializer = [AFJSONResponseSerializer serializer];
    
    
    
    
    session.requestSerializer.timeoutInterval = 15;
    NSString *baseString = [NSString xxxx];
    
    [session POST:baseString parameters:parameters progress:^(NSProgress * _Nonnull uploadProgress) {
        
    } success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
        if (success) {
            success(responseObject);
        }
    } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
        if (failure) {
            failure(error);
        }
    }];
}
```

也可以这样: 但是推荐第一种方式

```Plain
+ (void)postJsonWithURLString:(NSString *)urlString parameters:(NSMutableDictionary *)parameters success:(void (^)(id responseObject))success failure:(void (^)(NSError *error))failure {
    
    NSDictionary *body = parameters;
    
    NSError *error;
    
    NSData *jsonData = [NSJSONSerialization dataWithJSONObject:body options:0 error:&error];
    
    NSString *jsonString = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
    
    
    AFURLSessionManager *manager = [[AFURLSessionManager alloc] initWithSessionConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]];
    
    NSString *baseString = [NSString stringWithFormat:@"%@%@",REQ_HOST,urlString];
    
    NSMutableURLRequest *req = [[AFJSONRequestSerializer serializer] requestWithMethod:@"POST" URLString:baseString parameters:nil error:nil];
    
    req.timeoutInterval= [[[NSUserDefaults standardUserDefaults] valueForKey:@"timeoutInterval"] longValue];
    
    [req setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
    
    [req setValue:@"application/json" forHTTPHeaderField:@"Accept"];
    
    [req setHTTPBody:[jsonString dataUsingEncoding:NSUTF8StringEncoding]];
    
    [[manager dataTaskWithRequest:req completionHandler:^(NSURLResponse * _Nonnull response, id  _Nullable responseObject, NSError * _Nullable error) {
        
        if (!error) {
            
            

            success(responseObject);

        } else {
            
            
            failure(error);
            
        }
        
    }] resume];
    
}
```

“小礼物走一走，来简书关注我”

还没有人赞赏，支持一下

[![](https://upload.jianshu.io/users/upload_avatars/5818512/ac528289-89e7-4ba2-82f8-c222a96bccd3.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/100/h/100/format/webp)](https://upload.jianshu.io/users/upload_avatars/5818512/ac528289-89e7-4ba2-82f8-c222a96bccd3.jpg?imageMogr2/auto-orient/strip%7CimageView2/1/w/100/h/100/format/webp)

总资产 2 (约 0.21 元) 共写了 3524 字获得 24 个赞共 4 个粉丝

### 被以下专题收入，发现更多相似内容

### 推荐阅读[更多精彩内容](https://www.jianshu.com/)

- 原文来自：http://www.cnblogs.com/Mike-zh/p/5167017.html 流程梳理 今…
- 1、登录（文本输入、按钮交互、基于网络的交互） 2、刷新界面：（表视图） 1 > 小部分应用程序数据来源于本地 2 > 更…
    
    [炙冰](https://www.jianshu.com/u/0e8895b3ea5e)阅读 1
    
    [![](https://upload.jianshu.io/users/upload_avatars/3018546/8238ac9139e5?imageMogr2/auto-orient/strip%7CimageView2/1/w/48/h/48/format/webp)](https://upload.jianshu.io/users/upload_avatars/3018546/8238ac9139e5?imageMogr2/auto-orient/strip%7CimageView2/1/w/48/h/48/format/webp)
    
    [![](https://upload-images.jianshu.io/upload_images/3018546-b6a49504428bb6d2.png?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)](https://upload-images.jianshu.io/upload_images/3018546-b6a49504428bb6d2.png?imageMogr2/auto-orient/strip%7CimageView2/1/w/300/h/240/format/webp)
    
- 后台是 Java，今天他们要求和上传 Json 到服务器，方法如下： iOS 如何用 post 方式上传 son 数据 — AS…
- 218.241.181.202 wxhl60 123456 192.168.10.253 wxhl66 wxhl6…
- AFN 简介 目前国内开发网络应用使用最多的第三方框架 是专为 Mac OS & iOS 设计的一套网络框架 对 N…