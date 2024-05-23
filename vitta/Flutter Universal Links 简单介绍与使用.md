# Flutter Universal Links 简单介绍与使用

## 介绍
Universal Link, URL Schemes 是 iOS 系统中用于从外部打开 app 进行跳转的一种方式; AppLink 和 DeepLink 则是 Android 系统中用于从外部打开 app 进行跳转的方式。

### URL Schemes
URL Schemes 是 iOS9 之前一直在使用的跳转方式，可以在 App 间跳转，也可以通过在 Safari 中输入 `schema://` 进行跳转。这种方式会在网页中显示一个: `在 APPName 中打开链接吗` 的弹窗，如果未找到对应的 schemes url, 则会提示 `Safari浏览器打不开该网页，因为网址无效。`。 需要在 `info.plist` 里配置app 的 scheme url
### Universal Link
Universal Link 是 iOS9 之后出现的新技术，必须通过 `https://` 进行跳转。如果在手机中找到要跳转的 app, 则会在顶部显示个是否打开app 的条幅；如果未找到app, 则正常显示该网页。这种方式除了需要在 xcode 中对项目进行配置外，还需要创建一个 `apple-app-site-association` 文件上传到项目的服务器上。
### DeepLink
DeepLink 是在 Android 上类似于 iOS 上URL Schemes 的方式。DeepLink 可以让用户进入到指定的 Activity, 系统可能会弹出一个选择可以处理此类链接的应用列表。
### AppLink
AppLink 是在 Android 上类似于 iOS 上Universal Link 的方式, 可以直接从网站打开app 而无需用户选择，AppLink 也是需要创建一个文件上传到服务器。

## 使用
### 安装
> 这里介绍下 [uni_link](https://pub.dev/packages/uni_links)插件的使用.
 
 `flutter pub add uni_links`
### 配置
#### URL Scheme
 修改 `ios/Runner/Info.plist`
```
<?xml ...>
<!-- ... other tags -->
<plist>
<dict>
  <!-- ... other tags -->
  <key>CFBundleURLTypes</key>
  <array>
    <dict>
      <key>CFBundleTypeRole</key>
      <string>Editor</string>
      <key>CFBundleURLName</key>
      <string>[ANY_URL_NAME]</string>
      <key>CFBundleURLSchemes</key>
      <array>
        <string>[YOUR_SCHEME]</string>
      </array>
    </dict>
  </array>
  <!-- ... other tags -->
</dict>
</plist>
```
此时就可以使用 `YOUR_SCHEME://ANYTHING` 打开app
#### Universal Link
1. 创建 `com.apple.developer.associated-domains` entitlement 文件
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <!-- ... other keys -->
  <key>com.apple.developer.associated-domains</key>
  <array>
    <string>applinks:[YOUR_HOST]</string>
  </array>
  <!-- ... other keys -->
</dict>
</plist>
```
2. 创建 `apple-app-site-association` 文件，无后缀，内容是个`json`格式,类似这种
```
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "TEAMIDSHSAUX.com.test.bundle",
                "paths": [ "*" ]
            }
        ]
    }
}
```
3. 将上面生成好的 apple-app-site-association 上传到 web server
4. 等待生效(有时很久有时很快，最长24h)， 可以在 `https://search.developer.apple.com/appsearch-validation-tool/` 官方网站查看状态.
> 需要把 app 删掉重装.
> 需要把 app 删掉重装.
> 需要把 app 删掉重装.
5. 在safari 中打开你配置的域名就可以了
#### APPLinks 和 Deep Links
1. 修改 ` android/app/src/main/AndroidManifest.xml` 文件
```
<manifest ...>
  <!-- ... other tags -->
  <application ...>
    <activity ...>
      <!-- ... other tags -->

      <!-- Deep Links -->
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <!-- Accepts URIs that begin with YOUR_SCHEME://YOUR_HOST -->
        <data
          android:scheme="[YOUR_SCHEME]"
          android:host="[YOUR_HOST]" />
      </intent-filter>

      <!-- App Links -->
      <intent-filter android:autoVerify="true">
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <!-- Accepts URIs that begin with https://YOUR_HOST -->
        <data
          android:scheme="https"
          android:host="[YOUR_HOST]" />
      </intent-filter>
    </activity>
  </application>
</manifest>
```
2. AppLink 的话还需要 上传 `/.well-known/assetlinks.json` 文件到服务器(`https://domain.name/.well-known/assetlinks.json`)
```
[{
        "relation": [
            "delegate_permission/common.handle_all_urls"
        ],
        "target": {
            "namespace": "android_app",
            "package_name": "fr.smarquis.applinks",
            "sha256_cert_fingerprints": [
                "6B:41:26:A6:1E:D8:BD:91:D3:8B:57:10:5F:07:5C:2D:AB:3E:26:A4:D1:3C:9C:97:15:78:9E:0D:56:0A:CE:DC"
            ]
        }
    }]
```
3. 在 Chrome 中打开你配好的链接
> **AppLink不能直接在地址栏里输入，需要用 `location.href=` 这种跳转的方式才能打开app**
> **AppLink不能直接在地址栏里输入，需要用 `location.href=` 这种跳转的方式才能打开app**
> **AppLink不能直接在地址栏里输入，需要用 `location.href=` 这种跳转的方式才能打开app**

### 接收数据
```

import 'dart:async';
import 'dart:io';

import 'package:uni_links/uni_links.dart';

// ...

  StreamSubscription _sub;

  Future<void> initUniLinks() async {
    // ... check initialUri

    // Attach a listener to the stream
    _sub = uriLinkStream.listen((Uri? uri) {
      // Use the uri and warn the user, if it is not correct
    }, onError: (err) {
      // Handle exception by warning the user their action did not succeed
    });

    // NOTE: Don't forget to call _sub.cancel() in dispose()
  }

// ...
```

> 可以使用 adb shell pm get-app-links  package_name 检查sha 是否正确，不正确的话在Android 12+ 上是不会通过验证的。手机上可能需要能连接到谷歌(你懂的)