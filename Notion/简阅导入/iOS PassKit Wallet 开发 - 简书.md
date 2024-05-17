### 前言

根据目前系统钱包中的能够添加的卡，大致可分为三类

- 银行卡 / 交通卡

[![](http://upload-images.jianshu.io/upload_images/2121032-c254edc4db9fdd6a.png)](http://upload-images.jianshu.io/upload_images/2121032-c254edc4db9fdd6a.png)

image.png

- 电子卡 (例如：美团闪付 / 京东闪付)

[![](http://upload-images.jianshu.io/upload_images/2121032-901cb5601038f27d.png)](http://upload-images.jianshu.io/upload_images/2121032-901cb5601038f27d.png)

image.png

- 消费凭证 (电影票 / 机票 / 优惠券)

[![](http://upload-images.jianshu.io/upload_images/2121032-ab8ba68f138ec78f.png)](http://upload-images.jianshu.io/upload_images/2121032-ab8ba68f138ec78f.png)

image.png

### 消费凭证

消费凭证，大致分为五类，具体请看下图，对于每种凭证的包含信息，[点我](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Fdocumentation%2FUserExperience%2FConceptual%2FPassKit_PG%2FCreating.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40012195-CH4-SW1)

[![](http://upload-images.jianshu.io/upload_images/2121032-f7df3c458904ce98.png)](http://upload-images.jianshu.io/upload_images/2121032-f7df3c458904ce98.png)

image.png

### 制作凭证并添加到 Wallet

### 创建 pass 包

1. 先学习一波，—-> [请看大屏幕](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Fdocumentation%2FUserExperience%2FConceptual%2FPassKit_PG%2FYourFirst.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40012195-CH2-SW1)
2. 创建一个 Pass 包

首先要明白 Pasees 是以 Pass 包 形式创建的，Pass 包里面包含一个 pass.json 文件，一些图片资源（像 icon, logo 等）  
创建一个 Pass 包：  
  
（1）在 Finder 的 Desktop 初 创建一个 名为 Lollipop.pass 的文件夹  
  
（2）下载苹果提供的资源文件（包括一些 Pass 包例子, 一个签名工具， 一个测试服务器）  
  
下载资源：在官方文档中点击 developer downloads area ，即可下载  

[![](http://upload-images.jianshu.io/upload_images/2121032-fd96ed101af84f5e.png)](http://upload-images.jianshu.io/upload_images/2121032-fd96ed101af84f5e.png)

image.png

（3）在苹果资源处将 Event.pass 文件夹中的所有内容拷贝到 Lollipop.pass 文件夹中。

[![](http://upload-images.jianshu.io/upload_images/2121032-50eb66ac2b1b9835.png)](http://upload-images.jianshu.io/upload_images/2121032-50eb66ac2b1b9835.png)

image.png

1. 设置 Pass Type Identifier 和 Team ID  
    每一个 pass 都有和开发者账号相关连的 Pass Type Identifier  
    

官方文档如下：

```Plain
To register a pass type identifier, do the following:

In Certificates, Identifiers & Profiles, select Identifiers.

Under Identifiers, select Pass Type IDs.

Click the plus (+) button.

Enter the description and pass type identifier, and click Submit.

To find your Team ID, do the following:

Open Keychain Access, and select your certificate.
Select File > Get Info, and find the Organizational Unit section under Details. This is your Team ID.
The pass type identifier appears in the certificate under the User ID section.
```

按照苹果的意思在自己的开发账号内生成一个 Pass Type ID, 然后在 pass.json 文件内替换生成的 Pass Type ID， Team ID 同理，开发者账号内找到并且在 pass.json 文件内替换。

步骤如下：

- 在 Certificates, Identifiers & Profiles, 选择 Identifiers
- 在 Identifiers 下，选择 Pass Type IDs.
- 选择你已经创建好的 pass type identifier， 点击编辑。
- 如果已经存在证书文件，直接点击下载即可。如果没有，点击创建，按照提示创建一个（与创建 APNs 推送证书基本一样）。

[![](http://upload-images.jianshu.io/upload_images/2121032-2eeeb742f0d4d8cb.png)](http://upload-images.jianshu.io/upload_images/2121032-2eeeb742f0d4d8cb.png)

image.png

[![](http://upload-images.jianshu.io/upload_images/2121032-24fbb53bb99fc276.png)](http://upload-images.jianshu.io/upload_images/2121032-24fbb53bb99fc276.png)

image.png

如果有选择已经有的，如果没有则从电脑导出来

生成好之后如下：

[![](http://upload-images.jianshu.io/upload_images/2121032-6bdeed3c1f3ff31e.png)](http://upload-images.jianshu.io/upload_images/2121032-6bdeed3c1f3ff31e.png)

image.png

下载之后，双击安装到电脑。

1. 修改 pass.json 文件的 ID

- 查看 Team ID:
- 到开发者账号下，选择 MemberShip 。

[![](http://upload-images.jianshu.io/upload_images/2121032-bfb28b3d7e7cf7b7.png)](http://upload-images.jianshu.io/upload_images/2121032-bfb28b3d7e7cf7b7.png)

image.png

- 添加 PassTypeID 和 Team ID 到 pass.json

PassTypeID: pass.com.cuilinhao.TestPassKit

Team ID: P6E2X8E5T9

打开 Lollipop.pass 文件夹下的 pass.json , 将 PassTypeID 和 Team ID 替换为自己开发者账号下的。

```Plain
{
...
"passTypeIdentifier" : "your pass type identifier",
"teamIdentifier" : "your Team ID",
...
}
```

1. 生成 .pkpass 后缀的压缩文件

- 找到之前下载的文件，WalletDemo-master/WalletTest.xcodeproj  
    使用 xcode 运行  
    
- 选中 Xcode 中 Products 文件夹下的 signpass 文件，右击鼠标，Show in Finder。

[![](http://upload-images.jianshu.io/upload_images/2121032-fa5b5000ca8fa964.png)](http://upload-images.jianshu.io/upload_images/2121032-fa5b5000ca8fa964.png)

image.png

- 拷贝 signpass 文件到 filmTicket.pass 文件夹的同级目录（Desktop）下。
- 执行以下语句：

```Plain
cd ~/Desktop
./signpass -p Lollipop.pass
```

### 创建 Xcode 项目 添加凭证到 Wallet

直接放代码，其他文件配置可下载查看，[点我](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fcuilinhao%2FPassKit-Wallet-.git)

```Plain
- (void)viewDidLoad {
    [super viewDidLoad];

    PKAddPassButton *pkAddBtn = [[PKAddPassButton alloc] initWithAddPassButtonStyle:PKAddPassButtonStyleBlack];
    pkAddBtn.titleLabel.font = [UIFont systemFontOfSize:12];
    pkAddBtn.frame = CGRectMake(100, 100, 220, 40);
    [self.view addSubview:pkAddBtn];

    [pkAddBtn addTarget:self action:@selector(pkClick:) forControlEvents:UIControlEventTouchUpInside];
}


- (void)pkClick:(PKAddPassButton *)sender
{
    NSString *passPath = [[NSBundle mainBundle] pathForResource:@"Lollipop" ofType:@"pkpass"];
    NSData *passData = [[NSData alloc] initWithContentsOfFile:passPath];
    NSError *error = nil;
    PKPass *pass = [[PKPass alloc] initWithData:passData error:&error];
    if (error) {
        NSLog(@"创建pass 过程中发生错误,错误信息:%@", error.localizedDescription);
    }

    PKAddPassesViewController *vc = [[PKAddPassesViewController alloc] initWithPass:pass];
    vc.delegate = self;

    [self presentViewController:vc animated:YES completion:nil];

}


\#pragma mark -  delegate

- (void)addPassesViewControllerDidFinish:(PKAddPassesViewController *)controller
{
    NSLog(@"add pass finished");

    [self dismissViewControllerAnimated:YES completion:nil];

}
```

### 修改凭证信息，重新生成

1. 原有 pass.json 文件,

```Plain
{
  "formatVersion" : 1,
  "passTypeIdentifier" : "pass.com.cuilinhao.TestPassKit",
  "serialNumber" : "nmyuxofgna",
  "teamIdentifier" : "P6E2X8E5T9",
  "webServiceURL" : "https://example.com/passes/",
  "authenticationToken" : "vxwxd7J8AlNNFPS8k0a0FfUFtq0ewzFdc",
  "relevantDate" : "2011-12-08T13:00-08:00",
  "associatedStoreIdentifiers" : [728326385],
  "appLaunchURL" : "http://www.xingshulin.com",
  "locations" : [
    {
      "longitude" : -122.3748889,
      "latitude" : 37.6189722
    },
    {
      "longitude" : -122.03118,
      "latitude" : 37.33182
    }
  ],
  "barcode" : {
    "altText" : "订单号：123456",
    "message" : "123456789",
    "format" : "PKBarcodeFormatQR",
    "messageEncoding" : "iso-8859-1"
  },
  "organizationName" : "Apple Inc.",
  "description" : "Apple Event Ticket",
  "foregroundColor" : "rgb(255, 255, 255)",
  "backgroundColor" : "rgb(60, 65, 76)",
  "headerFields" : [
    {
      "key" : "filmName",
      "label" : "影片",
      "value" : "加勒比海盗5：死无对证",
      "textAlignment" : "PKTextAlignmentNatural"
    }
  ],
  "eventTicket" : {
    "primaryFields" : [
      {
        "key" : "filmName",
        "label" : "影片",
        "value" : "test1111111",
        "textAlignment" : "PKTextAlignmentNatural"
      }
    ],
  "secondaryFields" : [
      {
        "key" : "orderNumber",
        "label" : "订单号",
        "value" : "test2",
        "textAlignment" : "PKTextAlignmentLeft"
      },
      {
        "key" : "verificationNumber",
        "label" : "验证码",
        "value" : "test222",
        "textAlignment" : "PKTextAlignmentRight"
      }
    ],
  "auxiliaryFields" : [
      {
        "key" : "site",
        "label" : "影院",
        "value" : "test333",
        "textAlignment" : "PKTextAlignmentLeft"
      },
      {
        "key" : "order",
        "label" : "场次",
        "value" : "test3",
        "textAlignment" : "PKTextAlignmentCenter"
      },
      {
        "key" : "seat",
        "label" : "座位",
        "value" : "test333333",
        "textAlignment" : "PKTextAlignmentRight"
      }
    ],
    "backFields" : [
      {
        "numberStyle" : "PKNumberStyleSpellOut",
        "label" : "spelled out",
        "key" : "numberStyle",
        "value" : 200
      },
      {
        "label" : "in Reals",
        "key" : "currency",
        "value" : 200,
        "currencyCode" : "BRL"
      },
      {
        "dateStyle" : "PKDateStyleFull",
        "label" : "full date",
        "key" : "dateFull",
        "value" : "1980-05-07T10:00-05:00"
      },
      {
        "label" : "full time",
        "key" : "timeFull",
        "value" : "1980-05-07T10:00-05:00",
        "timeStyle" : "PKDateStyleFull"
      },
      {
        "dateStyle" : "PKDateStyleShort",
        "label" : "short date and time",
        "key" : "dateTime",
        "value" : "1980-05-07T10:00-05:00"
      },
      {
        "dateStyle" : "PKDateStyleShort",
        "label" : "relative date",
        "key" : "relStyle",
        "value" : "2013-04-24T10:00-05:00",
        "isRelative" : true
      }
    ]
  }
}
```

[![](http://upload-images.jianshu.io/upload_images/2121032-65d333854fbd7de5.png)](http://upload-images.jianshu.io/upload_images/2121032-65d333854fbd7de5.png)

image.png

上述代码和制作出的卡包是对应的，test11111 对应代码如下：

```Plain
"eventTicket" : {
    "primaryFields" : [
      {
        "key" : "filmName",
        "label" : "影片",
        "value" : "test1111111",
        "textAlignment" : "PKTextAlignmentNatural"
      }
    ],
```

其他部分，依次类推，其中下方的二维码部分，对应代码如下：

```Plain
// 修改前
"barcode" : {
    "message" : "123456789",
    "format" : "PKBarcodeFormatPDF417",
    "messageEncoding" : "iso-8859-1"
}
// 修改后
"barcode" : {
    "altText" : "订单号：123456",
    "message" : "123456789",
    "format" : "PKBarcodeFormatQR",
    "messageEncoding" : "iso-8859-1"
}
```

1. 更新好 pass.json 之后再次执行

```Plain
cd Desktop/
./signpass -p Lollipop.pass
```

然后将下面三个文件替换，Xcode 运行项目安装

[![](http://upload-images.jianshu.io/upload_images/2121032-862529fb9def6edb.png)](http://upload-images.jianshu.io/upload_images/2121032-862529fb9def6edb.png)

image.png

1. pass.json 官方说明

- [样式和内容规范](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Fdocumentation%2FUserExperience%2FConceptual%2FPassKit_PG%2FCreating.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40012195-CH4-SW1)
- [key-value 介绍文档](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Fdocumentation%2FUserExperience%2FReference%2FPassKit_Bundle%2FChapters%2FLowerLevel.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40012026-CH3-SW3)

### 更新凭证信息

流程图如下：

[![](http://upload-images.jianshu.io/upload_images/2121032-8b76677d6db38c4e.png)](http://upload-images.jianshu.io/upload_images/2121032-8b76677d6db38c4e.png)

image.png

- pass 被设置为支持更新和安装，并且用户设备注册到你的服务器获取更新。
- 如果有变更，则触发更新，你的服务器发送推送通知。
- 用户收到推送后，从你的服务器查询更新的列表。
- 用户从你的服务器获取每个 pass 的最新版本到自己的设备。

### 附上 Demo [OC 版 && Swift 版本](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fcuilinhao%2FPassKit-Wallet-.git)

### 京东闪付卡 / 美团闪付卡 / 银行卡

[![](http://upload-images.jianshu.io/upload_images/2121032-4a20d50c5ae70a2c.png)](http://upload-images.jianshu.io/upload_images/2121032-4a20d50c5ae70a2c.png)

image.png

这一类的卡，是通过公司接入银联支付产生的，具体可参考[银联官网](https://links.jianshu.com/go?to=https%3A%2F%2Fopen.unionpay.com%2Fijweb%2Fproduct%2Fdetail%3Fid%3D167), 并可直接电话联系咨询，京东和美团的闪付卡都是接入银联中的一个手机闪付业务做成闪付卡，然后添加到系统钱包。

在 [iOS Developer Wallet](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Fdocumentation%2Fpasskit%2Fwallet) 中，也介绍到，使用 [PKAddPaymentPassViewController](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Fdocumentation%2Fpasskit%2Fpkaddpaymentpassviewcontroller) 可以添加这类卡，苹果官方描述如下：

```Plain
Adding payment passes requires a special entitlement issued by Apple. Your app must include this entitlement before this class can be instantiated. For more information on requesting this entitlement, see the Card Issuers section at [developer.apple.com/apple-pay/](https://developer.apple.com/apple-pay/).

>>>
添加付款通行证需要Apple颁发特殊权利。 您的应用程序必须在此类可实例化之前包含此权利。有关请求此权利的更多信息，请参阅“发卡机构”部分
```

### 如何做一个凭证，从钱包跳回 App

```Plain
In your pass.json file you can include a key to define an associated app:

"associatedStoreIdentifiers" : [Adam ID],

where Adam ID can be obtained from the link to the app in the app store:

[https://itunes.apple.com/app/id](https://itunes.apple.com/app/id)<Adam ID> ..

e.g. to get the Facebook App, go to:

[https://itunes.apple.com/us/app/facebook/id284882215](https://itunes.apple.com/us/app/facebook/id284882215)

To include it in a Pass, add this to pass.json:

"associatedStoreIdentifiers" : [284882215],
```

[![](http://upload-images.jianshu.io/upload_images/2121032-03549bc0a8b8e2e5.png)](http://upload-images.jianshu.io/upload_images/2121032-03549bc0a8b8e2e5.png)

image.png

步骤如下：

- 拿到你的 App 上架的时候的 App ID
- 在制作凭证的. json 文件中 设置该 ID 为 associatedStoreIdentifiers 的 value 值，即：  
    “associatedStoreIdentifiers” : [1395841695]  
    
- 官方文档说明如下：

[![](http://upload-images.jianshu.io/upload_images/2121032-adcc266c66365777.png)](http://upload-images.jianshu.io/upload_images/2121032-adcc266c66365777.png)

image.png

### passKit 库用到的 API

PKAddPassButton ： 添加钱包按钮，主要有两种类型，PKAddPassButtonStyleBlack 、 PKAddPassButtonStyleBlackOutline

创建方式有两种：

- (instancetype)addPassButtonWithStyle:(PKAddPassButtonStyle)addPassButtonStyle;
- (instancetype)initWithAddPassButtonStyle:(PKAddPassButtonStyle)style NS_DESIGNATED_INITIALIZER;

PKPass 该类集成自 PKObject  
PKPassType: 枚举类型，  
  
PKPassTypeBarcode：条码  
  
PKPassTypePayment: 支付  
  
PKPassTypeAny：其它类型  

构造方法：

- (instancetype)initWithData:(NSData _)data error:(NSError_ )error;

PKPassLibrary 提供用户传递库

检测 PKPassLibrary 是否可用

- (BOOL)isPassLibraryAvailable API_AVAILABLE(ios(6.0), watchos(3.0));

根据 passtypeID 和 serialNumber 返回 pass

- (nullable PKPass _)passWithPassTypeIdentifier:(NSString_ )identifier serialNumber:(NSString *)serialNumber;

根据 passType 返回 pass

- (NSArray<PKPass _>_ )passesOfType:(PKPassType)passType API_AVAILABLE(ios(8.0), watchos(3.0));

移除 pass

- (void)removePass:(PKPass *)pass;  
    判断是否包含 pass  
    
- (BOOL)containsPass:(PKPass *)pass;  
    替换一个 pass  
    
- (BOOL)replacePassWithPass:(PKPass *)pass;  
    添加 pass  
    
- (void)addPasses:(NSArray<PKPass _>_ )passes withCompletionHandler:(nullable void(^)(PKPassLibraryAddPassesStatus status))completion API_AVAILABLE(ios(7.0), watchos(3.0));

PKPaymentPass 继承自 PKPass

PKPaymentPassActivationState 枚举类型，  
PKPaymentPassActivationStateActivated,（已激活）  
  
PKPaymentPassActivationStateRequiresActivation,（需要被激活）  
  
PKPaymentPassActivationStateActivating,（正在激活）  
  
PKPaymentPassActivationStateSuspended, （挂起）  
  
PKPaymentPassActivationStateDeactivated （停用）  

PKAddPaymentPassRequestConfiguration

该类包含初始化一个新的 PKAddPaymentPassViewController 实例的配置数据。加密机制，持卡人姓名，卡号后四位需要被提供。配置信息仅用来设置和显示。它不包含任何的敏感信息

重要说明：  
添加 Payment Pass 支付卡需要一个特殊的由苹果发行的授权。在使用这个类之前 app 中必须包括这个授权  

- (nullable instancetype)initWithEncryptionScheme:(PKEncryptionScheme)encryptionScheme

初始化一个新的配置对象

emcryptionScheme 用于该请求的加密机制。所有可能的值可以查看 Encryption Schemes.  
返回值：一个新的实例化的配置对象。  
  
当实例化一个配置对象之后，在使用它创建一个 PKAddPaymentPassViewController 实例之前，也必须设置 cardholderName 和 primaryAccountSuffix 属性  

cardholderName  
显示在卡上面的姓名  

encryptionScheme  
用于该请求的加密机制  

localizedDescription  
对卡片简短的描述。  

paymentNetwork  
支付系统，默认为 nil。该属性判断哪些卡片可以展示在 PKAddPaymentPassViewController 类的实例中并显示到屏幕上。PKAddPaymentPassViewController 展示卡片区域的所有支持的系统。为了指定一个单一的系统，可指派给该属性一个常量。可查看 PKPyamentRequest 类的 Payment Networks 的介绍。  

primaryAccountSuffix  
后四位或五位卡号  

Filtering Pass Libraries 筛选卡库  
primaryAccountIdentifier  
  
卡号账户的标识，筛选卡库 (来自不同的设备 iPhone,iPhone Watch)  

Constants 常量  
Encryption Schemes  
  
加密体制  
  
NSString * const PKEncryptionSchemeECC_V2  

PKAddPaymentPassViewController

使用提供的配置和代理，返回一个初始化的添加支付的视图控制器实例  
/* This controller should be presented with -[UIViewController presentViewController:animated:completion:].  
  
*/  

- (nullable instancetype)initWithRequestConfiguration:(PKAddPaymentPassRequestConfiguration *)configuration  
    delegate:(nullable id  
    
    )delegate
    

configuration 配置实例：定义视图控制器的外观  
delegate 添加支付视图控制器的代理  
  
返回值：一个新的添加支付的视图控制器  

添加 Payment Pass 支付卡需要一个特殊的由苹果发行的授权。如果 app 中不包括这个授权，该方法返回值为 nil

PKAddPaymentPassViewControllerDelegate 代理  
PKAddPaymentPassViewController 类的代理必须遵守该协议。该协议定义了两个必需实现的方法。这些方法使系统提示添加支付请求和当请求失败或成功的时候法通知 app。  

- (void)addPaymentPassViewController:(PKAddPaymentPassViewController _)controller__  
    generateRequestWithCertificateChain:(NSArray<NSData  
    _> _)certificates__  
    nonce:(NSData  
    _)nonce  
    nonceSignature:(NSData  
    _)nonceSignature__  
    completionHandler:(void(^)(PKAddPaymentPassRequest  
    _request))handler;

controller 添加支付请求的视图控制器  
certificates NSData 对象的数组。每个对象包括一个 DER 编码的证书。必须下载根目录 CA 验证整个链。  
  
nonce 苹果服务器生成的一次性随机值，该随机值必须被包含在添加支付请求的加密数据中。  
  
nonceSignature 有特定设备的签名的随机值。该签名必须被包含在添加支付请求的加密数据中。  
  
handler 完工的处理者。当创建支付请求之后回调该 Block。Block 中的参数：request 一个新创建的添加支付请求，必须 20 秒之内传送该请求实例给处理者否则该请求将失败，系统将为用户显示一个错误信息。  

该方法提供需要创建一个添加支付请求的书。通过证书束缚在发行者服务器上。该服务器返回一个包含卡数据的加密的 JSON 文件。当收到加密数据之后，创建一个添加支付请求并回调处理者。  
更多关于加密卡数据的信息，可以查看 PKPaymentRequest 类里的 encryptedPassData 属性。  

- (void)addPaymentPassViewController:(PKAddPaymentPassViewController _)controller didFinishAddingPaymentPass:(nullable PKPaymentPass_ )pass error:(nullable NSError *)error;  
    controller 添加支付请求的视图控制器  
      
    pass 完成的卡，如果有错误，返回 nil  
      
    error 如果请求失败，该参数包含错误对象 (PKPassKitErrorDomamin 域错误) 。更多可能的错误代码，可查看枚举 PKAddPaymentPassError。  
    

当请求成功地添加卡片到 Apple Pay 或者失败时，调用该方法。

//—- 苹果支付 —–  
PKPaymentRequest 订单请求对象  
  
PKPaymentSummaryItem 商品订单信息对象  

配置商品价格，送货方式等

- (instancetype)summaryItemWithLabel:(NSString _)label amount:(NSDecimalNumber_ )amount;
- (instancetype)summaryItemWithLabel:(NSString _)label amount:(NSDecimalNumber_ )amount type:(PKPaymentSummaryItemType)type API_AVAILABLE(ios(9.0), watchos(3.0));

PKPaymentAuthorizationViewController 苹果支付请求控制器  
初始化方法  

- (nullable instancetype)initWithPaymentRequest:(PKPaymentRequest *)request NS_DESIGNATED_INITIALIZER;

PKPaymentAuthorizationViewControllerDelegate 代理方法

// 支付银行卡回调，如果需要根据不同的银行调整付费金额，可以实现该代理

- (void)paymentAuthorizationViewController:(PKPaymentAuthorizationViewController _)controller didSelectPaymentMethod:(PKPaymentMethod_ )paymentMethod completion:(void (^)(NSArray<PKPaymentSummaryItem _>_ _Nonnull))completion

// 支付凭据，发给服务端进行验证支付是否真实有效

- (void)paymentAuthorizationViewController:(PKPaymentAuthorizationViewController _)controller didAuthorizePayment:(PKPayment_ )payment completion:(void (^)(PKPaymentAuthorizationStatus status))completion

// 支付完成

- (void) paymentAuthorizationViewControllerDidFinish:(PKPaymentAuthorizationViewController *)controller > 本文由简悦 SimpRead 转码