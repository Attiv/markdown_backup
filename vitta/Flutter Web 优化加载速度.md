本文来自 https://juejin.cn/post/7149441892994777125

## 安装

`pubspec.yaml`里添加

```
dev_dependencies:
flutter_web_optimizer: ^1.1.8
```

## 添加 loading 脚本

```
import 'dart:io';

void main() {
  print('Fixing index.html');
  print('******************************');
  print('Please check --base-href path');
  print('******************************');
  var file = File('./build/web/index.html');
  var content = file.readAsStringSync();

  // var time = DateTime.now().millisecondsSinceEpoch;
  // content = content.replaceFirst('src="main.dart.js"', 'src="main.dart.js?_=$time"');

  content = content.replaceFirst(
      r'''<link rel="manifest" href="manifest.json" />''',
      r'''<link rel="manifest" href="manifest.json" /><style>
    @keyframes flash {
      from {
        opacity: 0;
      }
      to {
        opacity: 1;
      }
    }
  </style>''');
  content = content
      .replaceFirst(r'''<body>''', r'''<body><div style="position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -70%);
    animation: flash 0.8s ease-in-out infinite alternate;
    text-align: center;">
    <img src="logo.png" style="width: 178px" alt="">
  </div>''');

  file.writeAsString(content);
  print('done!');
}

```

## 使用

1. `flutter clean`
2. `flutter pub get`
3. `flutter build web --base-href '/' --release --web-renderer html --pwa-strategy none`
> `--pwa-strategy none` 是关闭 pwa 支持
4. `dart ./bin/build.dart`
5. `flutter pub run flutter_web_optimizer optimize --asset-base url_path/`
   > `url_path/` 是项目路径，必须以 `/` 结尾