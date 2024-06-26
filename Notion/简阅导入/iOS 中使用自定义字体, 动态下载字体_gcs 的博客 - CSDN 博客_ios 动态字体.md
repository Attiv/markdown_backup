在 iOS 的开发中经常遇到需要使用一些自定义的字体文件，比如仿宋_GB2312、方正小标宋_GBK 等。之前我们为了使用这些自定义的字体，在应用的资源包中放入这些字体文件。因为字体文件通常比较大，有的一个字库就达到 10M 以上（拿方正小标宋_GBK 这个字库来说就有 13M 之多），这样打包后的 ipa 文件的体积就可能会变得很大，对于只有个别的模块需要特殊的字体样式的应用来说很不划算，那么在 iOS6.0 以后苹果就开放了动态加载字体的权限。下面就 iOS 中使用字体的这两种方式进行介绍。

**使用静态字体**

1、将字体文件拷贝到项目工程中，在 Info.plist 文件中添加 Fonts provided by application 的配置项，其中每一个 Item 对应的是字体文件的名称，如 DS-DIGI.TTF。

[![](https://img-blog.csdnimg.cn/img_convert/0f7362b3f27819e944e66586d81c73c0.png)](https://img-blog.csdnimg.cn/img_convert/0f7362b3f27819e944e66586d81c73c0.png)

2、使用时直接按照如下方式即可：

_textLabel1.font = [UIFont fontWithName:@“DS-Digital” size:40];

效果如下：

[![](https://img-blog.csdnimg.cn/img_convert/97d12cc88155795e2d4a9fd99032c744.png)](https://img-blog.csdnimg.cn/img_convert/97d12cc88155795e2d4a9fd99032c744.png)

3、其他说明：

- (UIFont _)fontWithName:(NSString_ )fontName size:(CGFloat)fontSize; 这个方法中需要指定的 fontName 不是前面设置的字体文件的文件名，而应该是字体的名称，如何获取字体的名称可以通过如下方式：

（1）打印出当前所有可用的字体，查找对应的字体名称

```Plain
- (void)printAllFonts {

    NSArray *fontFamilies = [UIFont familyNames];

    for (NSString *fontFamily in fontFamilies) {
        NSArray *fontNames = [UIFont fontNamesForFamilyName:fontFamily];
        NSLog (@"%@: %@", fontFamily, fontNames);
    }

}
```

（2）通过 Mac 自带的字体册查看字体的名称

直接双击字体即可打开字体册，如果系统没有安装该字体按照要求安装即可，然后可以在字体的详细信息中找到对应的字体的名称：

[![](https://img-blog.csdnimg.cn/20210224184212539.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQ2MDA2MjY=,size_16,color_FFFFFF,t_70)](https://img-blog.csdnimg.cn/20210224184212539.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQ2MDA2MjY=,size_16,color_FFFFFF,t_70)

**使用动态字体**

**1、动态下载自定义的字体**

在网易新闻 iOS 客户端中可以使用自定义的字体，对于未下载的字体可先下载然后安装下次就能自动设置为该字体，效果如下：

[![](https://img-blog.csdnimg.cn/img_convert/4509974a39d48adc60e83d324915a342.png)](https://img-blog.csdnimg.cn/img_convert/4509974a39d48adc60e83d324915a342.png)

下面就该功能简单介绍实现的步骤

（1）下载指定的字体文件到本地

第一次进入该页面会自动到服务器上获取可使用的字体的列表，示例如下：

```Plain
[{
"fontTitle": "华康圆体",
"regularName": "DFYuanW3-GB",
"boldName": "DFYuanW5-GB",
"author": "华康科技",
"date": "2012-10-11",
"fileUrl": "http://xxxx/font/dfgb_y.zip",
"fileSize": "3.3MB",
"previewUrl": "http://yyyy/font/ios_yuanti.png"
}]
```

上面的内容指明了字体的名称，下载地址等信息，从上面的内容可以看出下载回来的字体文件是一个 zip 压缩包，再使用前还需要进行解压处理。

1）下载字体文件

```Plain
- (NSString *)downloadZipFile:(NSString *)fileUrl toPath:(NSString *)path {

    NSError *error = nil;
    NSURL *url = [NSURL URLWithString:fileUrl];
    NSString *fileName = [url lastPathComponent];
    NSData *data = [NSData dataWithContentsOfURL:url options:0 error:&error];

    if(!error) {

        NSString *zipPath = [path stringByAppendingPathComponent:fileName];
        [data writeToFile:zipPath options:0 error:&error];
        if(!error) {
            return zipPath;
        }
    }
    return nil;
}
```

2）解压 zip 压缩包

iOS 中解压 zip 压缩文件非常方便，使用 ZipArchive 这个开源项目按照如下的方式即可快速解压 zip 文件。

```Plain
- (NSString *)expandZipFile:(NSString *)src toPath:(NSString *)desc {

    ZipArchive *za = [[ZipArchive alloc] init];

    if ([za UnzipOpenFile:src]) {

        BOOL ret = [za UnzipFileTo:desc overWrite:YES];//解压文件
        if(ret){
            NSString *zipName = [src lastPathComponent];//获取zip文件的文件名
            [[NSFileManager defaultManager] removeItemAtPath:zipPath error:nil];//删除zip压缩包
            zipName = [zipName substringToIndex:[zipName rangeOfString:@".zip"].location];//获取解压到的文件夹
            return [self.downloadPath stringByAppendingPathComponent:zipName];
        }
    }

    return nil;
}
```

ZipArchive 项目地址：https://github.com/mattconnolly/ZipArchive

（2）注册指定路径下的字体文件

下载回来的字体文件如果不做处理是不能直接使用的，使用前需要先注册然后才能使用，注册方式如下：

```Plain
需要先引入\#import <CoreText/CoreText.h>，CoreText框架。
- (void)registerFont:(NSString *)fontPath {

    NSData *dynamicFontData = [NSData dataWithContentsOfFile:fontPath];
    if (!dynamicFontData){
        return;
    }

    CFErrorRef error;
    CGDataProviderRef providerRef = CGDataProviderCreateWithCFData((__bridge CFDataRef)dynamicFontData);
    CGFontRef font = CGFontCreateWithDataProvider(providerRef);
    if (! CTFontManagerRegisterGraphicsFont(font, &error)){
        //注册失败
        CFStringRef errorDescription = CFErrorCopyDescription(error);
        NSLog(@"Failed to load font: %@", errorDescription);
        CFRelease(errorDescription);
    }
    CFRelease(font);
    CFRelease(providerRef);
}

// 注册方式2,使用URL
 NSString *imgFilePath = [filePath path];
 NSURL *fontUrl = [NSURL fileURLWithPath:imgFilePath];
 CGDataProviderRef fontDataProvider =  CGDataProviderCreateWithURL((__bridge CFURLRef)fontUrl);
 CGFontRef fontRef = CGFontCreateWithDataProvider(fontDataProvider);
 //the next line is relevant part
 [UIFont familyNames];
 CGDataProviderRelease(fontDataProvider);
 CTFontManagerRegisterGraphicsFont(fontRef, NULL);
 NSString *fontName = CFBridgingRelease(CGFontCopyPostScriptName(fontRef));
 label.font = [UIFont fontWithName:fontName size:24];
```

> 在调用注册 CTFontManagerRegisterGraphicsFont 前最好调下 [UIFont familyNames]; 苹果内部的一个 bug.
> 
> [ios - CGFontCreateWithDataProvider hangs in airplane mode - Stack Overflow](https://stackoverflow.com/questions/24900979/cgfontcreatewithdataprovider-hangs-in-airplane-mode)

（3）判断字体是否加载

在使用字体文件前最好是先判断字体是否已经被加载过了，判断方式如下：

```Plain
- (BOOL)isFontDownloaded:(NSString *)fontName {

    UIFont* aFont = [UIFont fontWithName:fontName size:12.0];
    BOOL isDownloaded = (aFont && ([aFont.fontName compare:fontName] == NSOrderedSame || [aFont.familyName compare:fontName] == NSOrderedSame));
    return isDownloaded;
}
```

（4）其他说明

经测试注册过的字体在应用关闭后下次开启应用，判断字体是否加载时返回为 NO，为了保证正常使用需要每次启动应用的时候先遍历一遍字体文件夹将里面的字体文件都再次注册一遍即可。参考代码如下：

```Plain
//注册fonts目录下面的所有字体文件
    NSArray *ary = [[NSFileManager defaultManager] contentsOfDirectoryAtPath:self.downloadPath error:nil];
    for (NSString *p1 in ary) {
        NSString *t1 = [self.downloadPath stringByAppendingPathComponent:p1];
        NSArray *ary1 = [[NSFileManager defaultManager] contentsOfDirectoryAtPath:t1 error:nil];
        for (NSString *p1 in ary1) {

            NSString *t2 = [t1 stringByAppendingPathComponent:p1];
            if([t2 rangeOfString:@".ttf"].location != NSNotFound) {
                [self registerFont:t2];
            }
        }
    }
```

**2、动态下载苹果提供的字体**

大多数的中文字体是有版权的，在应用中加入特殊中文字体还需要处理相应的版权问题。从 iOS6 开始，苹果就支持动态下载中文字体到系统中。

（1）苹果支持下载的字体列表

1）iOS6 字体列表：http://support.apple.com/zh-cn/HT202599

2）iOS7 字体列表：http://support.apple.com/zh-cn/HT5878

（2）官方提供的示例代码

访问 https://developer.apple.com/library/ios/samplecode/DownloadFont/Introduction/Intro.html 下载示例程序。针对示例程序简单介绍如下：

1）判断字体是否已经被下载过

```Plain
UIFont* aFont = [UIFont fontWithName:fontName size:12.];

if (aFont && ([aFont.fontName compare:fontName] == NSOrderedSame || [aFont.familyName compare:fontName] == NSOrderedSame)) {
// 字体已经被加载过，可以直接使用
return;

}
```

2）下载字体

```Plain
// 根据字体的PostScript名称构建下载字体所需的参数：

    //使用字体的PostScript名称构建一个字典
    NSMutableDictionary *attrs = [NSMutableDictionary dictionaryWithObjectsAndKeys:fontName, kCTFontNameAttribute, nil];
    //根据上面的字典创建一个字体描述对象
    CTFontDescriptorRef desc = CTFontDescriptorCreateWithAttributes((__bridge CFDictionaryRef)attrs);

    //将字体描述对象放到一个数组中
    NSMutableArray *descs = [NSMutableArray arrayWithCapacity:0];
    [descs addObject:(__bridge id)desc];
    CFRelease(desc);

    // 下载字体文件：
    _block BOOL errorDuringDownload = NO;
    CTFontDescriptorMatchFontDescriptorsWithProgressHandler( (__bridge CFArrayRef)descs, NULL,  ^(CTFontDescriptorMatchingState state, CFDictionaryRef progressParameter) {
        //下载的进度
        double progressValue = [[(__bridge NSDictionary *)progressParameter objectForKey:(id)kCTFontDescriptorMatchingPercentage] doubleValue];

        if (state == kCTFontDescriptorMatchingDidBegin) {
            dispatch_async( dispatch_get_main_queue(), ^ {
                //开始匹配
                NSLog(@"Begin Matching");
            });

        } else if (state == kCTFontDescriptorMatchingDidFinish) {

            dispatch_async( dispatch_get_main_queue(), ^ {
                if (!errorDuringDownload) {
                    //字体下载完成
                    NSLog(@"%@ downloaded", fontName);
                    //TODO:在此修改UI控件的字体样式
                }

            });

        } else if (state == kCTFontDescriptorMatchingWillBeginDownloading) {

            //开始下载
             NSLog(@"Begin Downloading");
             dispatch_async( dispatch_get_main_queue(), ^ {
                //TODO:在此显示下载进度提示
            });

        } else if (state == kCTFontDescriptorMatchingDidFinishDownloading) {

            //下载完成
            NSLog(@"Finish downloading");
            dispatch_async( dispatch_get_main_queue(), ^ {
                //TODO:在此修改UI控件的字体样式，隐藏下载进度提示
            });

        } else if (state == kCTFontDescriptorMatchingDownloading) {

            //正在下载
            NSLog(@"Downloading %.0f%% complete", progressValue);
            dispatch_async( dispatch_get_main_queue(), ^ {
                //TODO:在此修改下载进度条的数值
            });

        } else if (state == kCTFontDescriptorMatchingDidFailWithError) {

            //下载遇到错误，获取错误信息
            NSError *error = [(__bridge NSDictionary *)progressParameter objectForKey:(id)kCTFontDescriptorMatchingError];
            NSLog(@"%@", [error localizedDescription]);
            //设置下载错误标志
            errorDuringDownload = YES;
        }

            return YES;

    });
```

（3）说明

1）使用动态下载中文字体的 API 可以动态地向 iOS 系统中添加字体文件，这些字体文件都是下载到系统的目录中（目录是 / private/var/mobile/Library/Assets/com_apple_MobileAsset_Font/），所以并不会造成应用体积的增加，而且可以在多个应用中共享。

2）如何获取字体的 PostScript 和 FontName？可以通过 Mac 系统自带的字体册来查看。具体请参考前面的步骤。 > 本文由简悦 SimpRead 转码