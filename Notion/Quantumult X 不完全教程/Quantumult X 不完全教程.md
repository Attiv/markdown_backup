**更新说明**

> [!important]  
> 更多关于 QuantumultX 使用问题，可加入下 telegram 群/频道 交流讨论 https://t.me/QuanXApp (Quantumult X 交流群) https://t.me/QuanXNews （Quantumult X 频道）本教程以及本人 QuantumultX-API的相关信息，可以订阅此频道: https://t.me/QuanX_API (API&教程&解析器通知频道)  

  

- 2020-04-12
    
    新增 [**`配置关联`**](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21) 部分用法说明(5.2)
    
- 2020-04-26
    
    新增[资源解析器部分教程](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)
    
- 2020-05-02
    
    补充运行模式 [running-mode-trigger](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21) 说明
    

- 2020-05-10
    
    调整部分教程结构
    
- 2020-05-28
    
    策略组新正则参数`**regex**`说明
    

- 2020-11-22
    - 更新远程脚本使用说明；
    - 增加 ==[[Quantumult X 不完全教程]]== 使用部分

  

---

---

# **教程目录（****`请先从目录中查找你需要的内容`**）

教程目录（请先从目录中查找你需要的内容）

说明：教程包括以下 6️⃣ 部分(懒人可直接从 0️⃣ 跳到 5️⃣ [==5.1部分==](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)==)==：

🕹 切换模式～隐藏VPN～等常用技巧...

A. 分流模式/远程资源更新/ssid悬停/运行模式(图1&图2)

B. 延迟测试 (图3)

C. 其它 (图4)

D. SSID/运行模式相关

0⃣️ 完整示范配置说明

0.1 Quantumult X 特性说明

0.2 完整示范配置

0.3 通用设置 [general]

1⃣️ 节点导入[server_remote/local]

1.1 节点订阅引用（ss/ssr/vmess/https/trojan）

1.2 UI/文本 添加示范(ss/ssr/vmess/https/trojan)

1.3 👍️👍️资源解析器👍️👍️

A. 添加方法

B. 功能介绍

B. 使用示范

C. 效果示范

1.4 ⚠️⚠️进阶教程：节点订阅第三方 API 的使用⚠️⚠️

A. UDP & TFO 参数

B. ㊙️ 节点list 过滤 ㊙️（利用参数过滤节点)

C. list订阅&策略组的绑定

1.5 节点/订阅 后续操作

2⃣️ 分流规则导入[filter_remote/local]

2.1 本地手动添加

2.2 导入 （订阅规则到本地）此方式已取消

2.3 引用 （远程订阅）— 👍👍 推荐

A. 整体规则引用(❎️不推荐❎️)

B. 👍👍 rule-list 引用 👍👍

I. 使用方法：

2.4 后续操作(⚠️⚠️策略组使⚠️⚠️)

A. 引用规则编辑

B.⚠️⚠️策略组操作👈️👈️

3⃣️ QuantumultX 策略组[policy]

3.1 策略组说明

3.2 策略组的添加 & SSID 策略组实例

A. 策略组的自定义添加

B. SSID 策略组添加实例

3.3 ⚠️⚠️策略组的生效⚠️⚠️

A. 直接引用生效

B. 间接引用生效

3.4 🚥策略组图标自定义

A. 操作方法（分本地/远程两种方式）

B. 效果示范：

C. 资源下载 ⏬

3.5 策略组的删除

3.6 👍️👍️策略组进阶玩法(regex正则筛选)

A. 参数说明&使用

B. 参数优点

4⃣️ Rewrite/MITM 解密

4.1 . Rewrite 部分

4.2 . MitM 部分

4.3 . HTTPS 调试

5⃣️ URL-Scheme/配置导入与同步

5.1 整个配置导入(👍👍懒人/小白推荐👍👍)

a. 示范配置链接：

b. 使用方式：

5.2 配置关联绑定(类似托管👍️👍️)

a. 说明

b. 使用方法

C. 注意事项

5.3 URI 导入

6⃣️ JavaScript 脚本以及[task]使用

6.1 使用简要说明

A. JS 文件（远程-本机-iCloud）

B. 重写语句

6.2 JavaScript 去广告(rewrite)

A . JS脚本资源 (可供学习，但请勿滥用)

6.3 任务脚本使用（task scripts）

A. 添加方法

B. 效果展示

C. 资源分享

D. 调试方法

6.3 JS 自定义查询节点信息

---

## 说明：教程包括以下 6️⃣ 部分(==懒人可直接从 0️⃣ 跳到== ==5️⃣== [==5.1部分==](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)==)==：

⚠️⚠️==**因为功能的增加，教程会越发臃肿混乱，请先阅读目录，按需寻找相应内容。⚠️⚠️**==

- 0️⃣ 常见问题&小技巧
- 0️⃣0️⃣Quantumult X 简要说明
- 1⃣️ [节点导入 (SS/SSR/V2Ray)](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)
- 2⃣️ [分流规则导入（Filter）](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)
- 3⃣️ [QuantumultX 策略组说明](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)
- 4⃣️ [Rewrite/MITM 解密](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)
- 5⃣️ [URL-Scheme/远程导入配置(⚠️⚠️)](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)
- 6⃣️ [JavaScript 脚本使用](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)

老司机直接看官方配置说明即可：

[https://github.com/crossutility/Quantumult-X/blob/master/sample.conf](https://github.com/crossutility/Quantumult-X/blob/master/sample.conf)

或者先行查看此有简单注释部分的配置示范：

[https://github.com/KOP-XIAO/QuantumultX/blob/master/QuantumultX_Profiles.conf](https://github.com/KOP-XIAO/QuantumultX/blob/master/QuantumultX_Profiles.conf)

PS. 作者更新太勤，所以以下内容仅保证 ==tf版本 1.0.8 build-272== 有效

> [!important]  
> 如果觉得教程对你有帮助，可以大胆打赏请咖啡👍  

![[IMG_5957.jpg]]

  

---

---

# 🕹 切换模式～隐藏VPN～等常用技巧...

---

> [!important]  
> QuantumultX是一款很有开发者个人风格的app，所以，有些操作/彩蛋，请自行折腾/体会,下面是几个常见的小技巧：  

### A. 分流模式/远程资源更新/ssid悬停/运行模式(图1&图2)

- 点开查看详细内容
    
    1 - 请直接 `**==长按==**`右下角圆图标，切换成 `**==分流==**` 模式(三色)； 参见 图1& 图2
    
    > [!important]  
    > 从build92版本开始，此方式默认关闭，请先自行开启：点右下角图标 → 点最下方[其他设置] → 打开“长按主页功能键切换”  
    
    2 - **`一键更新`** 所有订阅（**`分流/节点/rewrite`**）：见图①
    
    如果你只想`**单独更新**` 节点/分流/rewrite部分， 你可以长按 对应模块 进入相应的二级菜单，然后更新（**`默认24小时自动更新所有资源`**）
    
    3 - **`隐藏 VPN`**：点右下角图标→点右上角...（新TF中为最下方 “**`其它设置`**”）→ 打开 排除路由0.0.0.0/31“” 参见图1
    
    4 - **`geoip数据库更新`**：按照 4 中进入**`其它设置`**后，即可找到GeoLite2
    
    5 - `**ssid suspend:**` 配置文件/编辑/[general]: ssid_suspended_list = 你的 WiFi 名字  
    这样设置后，Quantumult X 将在你指定的 WiFi 下自动暂停工作  
    

### B. 延迟测试 (图3)

- 点开查看详细内容
    
    - **`延迟测试`****(热点分享模式下，禁止了延迟测试)：参见图3**
    
    - 请在 **`节点/策略组`** 页面，展开订阅（如有） **`下拉`** 即可；
    - 同样可以长按节点名，选择“`**网页响应测试**`”，来测对应 节点/订阅 的延迟 ；
    - 或者点按 策略组 图标，同样可以测试节点延迟
    

### C. 其它 (图4)

- 点开查看详细内容
    
    1 - **`精简模式`**：策略组那一栏图标**`向右`**滑动到最`**左边**`**，  
    继续用力一拉，即可进入  
    **`**单行的精简模式**`**  
    再拉一次，进入  
    **`**双行精简模式**`**;  
    再拉一次，退回  
    **`**普通显示模式**`
    
    2 - 如**图4** 所示，有`**虚线圆环**`的地方，表示有**`二级菜单`**，可通过长按进入
    
    3 - 在QuantumultX中，以下符号是 `**注释符号**`**，**用于解释代码，加了就不会生效：  
      
    `**分号 ; ，双斜杠 // ，井号 # （所以你在添加节点/规则时，请不要在前面添加此类符号）**`
    

### D. SSID/运行模式相关

- 运行模式(点击查看详细内容)
    
    **根据网络模式切换运行模式**
    
    Quantumult X 最新 tf 支持 running_mode_trigger 设置，即根据网络自动切换 分流/直连/全局代理 等模式。
    
    1⃣️ 示范 ( [general]模块下 )：
    
    running_mode_trigger=filter, filter, asus-5g:all_direct, asus: all_proxy
    
    ; 上述写法，4G 网络跟一般 Wi-Fi 下，走 filter(分流)模式，asus-5g 则切换为全局直连，asus 切换为全局代理
    
    2⃣️ 与ssid-suspend以及ssid策略组的区别
    
    - ssid-suspend 下，Quantumult X 网络相关功能会停止工作，只有[task] 模块生效；
    
    - ssid 策略组，属于 filter 即分流模式的一个小部分，灵活，但设置相对麻烦；
    
    - mode-trigger 模式下，跟手动切换直连/全局代理 等效，rewrite/task 模块始终会生效，设置简单
    

![[Untitled.png]]

> [!important]  
> PS. 后续请务必请注意 点按 与 长按 两操作的区别，quantumultx 中有很多隐藏操作。 右下角图标可能随版本有重大变化，不用纠结  

![[STIIITCH_2020_01_10_04_24_31.jpg]]

**图1**

![[STIIITCH_2020_01_10_04_35_14.jpg]]

**图3**

![[STIIITCH_2020_01_10_04_28_08.jpg]]

**图2**

![[IMG_047243FC77F2-1.jpeg]]

图4

---

---

---

# 0⃣️ 完整示范配置说明

## 0.1 Quantumult X 特性说明

QuantumultX 最大的特色，就是在保持丰富而灵活的策略分流功能的同时，实现了 **`节点与规则`** 的独立，而后通过内置的策略组PROXY（或自定义的策略组）实现了完整耦合。

这里值得一提的是Quantumult X `**内置的 PROXY**`，是一个包含你所有节点的策略组，也就是“`**节点**`”模块，

- 如果你有一条分流规则是 `**host, google.com, PROXY**`, 那么google.com的请求，就将走你在`**节点**` 模块所指定的服务器；
- PROXY 的存在，是为了方便小白以及需求简单的用户，能够导入节点后直接使用，无需再添加过多的策略组。

简单来说，Quantumult X是通过所谓的`**分流规则**`，来实现对网络请求的处理，从而实现：

- Google 相关请求走 节点A
- Netflix 相关请求走节点B
- 微信/优酷 相关请求走直连，或回国路线C
- 广告相关/不想访问的网站 请求被拒绝，走 reject (当然，去广告实际更为复杂，可能需要用到rewrite以及mitm解密相关的部分)

> [!important]  
> 所以对于普通用户而言，需要用到的无非两个东西：1. 节点； 2.分流规则也就是 导入节点，再导入规则，你就可以愉快的使用了  

## 0.2 完整示范配置

了解 QuantumultX 完整的配置结构后，你基本就已经知道了它的使用逻辑。

[[示范配置说明]]

而教程将大概按照示范配置的分块进行讲解，分别为：

`**[general]**` 常用设置；

`**[server_remote/local]**` 远程/本地 节点添加;

`**[filter_remote/local]**` 远程本地 分流规则；

`**[rewrite_remote/local]**` 远程本地 重写规则 ;

`**[mitm]**` 解密模块

`**JavaScript**` 脚本以及`**[task]**` 的使用

## 0.3 通用设置 [general]

general 模块内为一些通用的设置参数项

其中比较重要的 `**running_mode_trigger**` 已经在前面的小技巧里提及，而最为强大的资源解析器 `**resource_parser_url**` 则在教程的 1.4部分 会被详细介绍

```JavaScript
[general]
;Quantumult X 会对 server_check_url 指定的网址进行相应测试，以确认节点的可用性
;你同样可以在 server_local/remote 中，为节点、订阅单独指定server_check_url参数
server_check_url= http://www.qualcomm.cn/generate_204

;资源解析器，可用于自定义各类远程资源的转换，如节点，规则 filter，复写 rewrite 等，url 地址可远程，可 本地/iCloud(Quantumult X/Scripts目录);
;下面是我写的一个解析器，具体内容直接参照链接里的使用说明
resource_parser_url= https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/resource-parser.js

;geo_location_checker用于节点页面的信息展示，可完整自定义
; extreme-ip-lookup为Quantumult X 作者提供的示范 api
;geo_location_checker=http://extreme-ip-lookup.com/json/, https://raw.githubusercontent.com/crossutility/Quantumult-X/master/sample-location-with-script.js
;下面是我所使用的 api 及获取、展示节点信息的 js
geo_location_checker=http://ip-api.com/json/?lang=zh-CN, https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IP_API.js

;dns exclusion list中的域名将不使用fake-ip方式. 其它域名则全部采用 fake-ip 及远程解析的模式
;dns_exclusion_list=*.qq.com, qq.com

;运行模式模块，running_mode_trigger 设置，即根据网络自动切换 分流/直连/全局代理 等模式。
;running-mode-trigger 模式下，跟手动切换直连/全局代理 等效，rewrite/task 模块始终会生效，设置简单

;running_mode_trigger=filter, filter, asus-5g:all_direct, asus: all_proxy
; 上述写法，前两个 filter 表示 在 4G 网络跟一般 Wi-Fi 下，走 filter(分流)模式，asus-5g 则切换为全局直连，asus 切换为全局代理

;ssid_suspended_list 写入你想要 Quantumult X 暂停的 Wi-Fi网络名称，多个wifi用“,”连接
;ssid_suspended_list=Asus, Shawn-Wifi

;UDP名单，留空则默认所有为端口。不在udp白名单列表中的端口，将被丢弃处理。
;udp_whitelist=53, 123, 1900, 80-443

;下列表中的内容将不经过 QuantumultX的处理
;excluded_routes= 192.168.0.0/16, 172.16.0.0/12, 100.64.0.0/10, 10.0.0.0/8
;icmp_auto_reply=true
```

---

---

# 1⃣️ 节点导入[server_remote/local]

---

> [!important]  
> 无论你使用的是何种节点，请先添加 [[Quantumult X 不完全教程]]后，再进行操作  

  

目前来说，Quantumult X 共支持 5⃣️种 类型的服务器：`**SS， SSR， VMess， HTTP(s)，Trojan**`

![[IMG_5961.jpg]]

> [!important]  
> UI中的 添加只支持输入简单 ss 信息  
  
> [!important]  
> 引用 支持 ss，ssr 订阅，以及 Quanx 格式的 vmess / https / trojan 订阅使用解析器后则支持其它任何格式订阅  
  
> [!important]  
> 扫码跟 URI 支持 ss、ssr以及 Quanx 格式的 vmess / https / trojan uri/二维码1.0.13 + 解析器 后则支持其它格式单节点  
  
> [!important]  
> 配置文件 [server_local]支持手写 ss/ssr/vmess/https/trojan, 格式参照 配置文件/示例，或下面的 1.2 部分  

  

细分来说吧，共有以下`**三种**` 导入节点的方式

1. 订阅导入： `ss/ssr，可直接通过订阅方式导入`，而 Vmess / https / trojan, 暂时只支持`Quantumult X 格式`(`见1.2部分文本示范`)的订阅格式链接导入，(其它格式请参照[==**下方1.3 的资源解析器**==](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21))；
    - 所以如果你有`**订阅链接**`，请选择此方式；
    - 如果你使用了`**资源解析器**`，同样可以通过`**本地资源片段**`来进行订阅管理[[Quantumult X 不完全教程]][[Quantumult X 不完全教程]][[Quantumult X 不完全教程]]
    - 订阅后，会出现在配置文件的 `**[server_remote]**` 部分
2. UI扫码/URI 加入，支持ss/ssr，或者Quantumult X 格式编码的vmess/http 二维码，
    - 其它格式请参照 [**1.3 解析器部分**](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21) [](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)的本地资源片段引用
    - 如果是 `版本 1.0.13+`，则可`**添加解析器后**`直接通过扫码、uri 导入任何格式节点
    - 添加后，节点会出现在配置文件的 `**[server_local]**` 部分
3. 通过 配置`文本编辑 手动添加`，支持所有节点类型，ss/ssr/vmess/https/trojan，格式参照app内的示范配置，或本教程的 **[1.2部分](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)**；
    - 如果你只有节点信息，请选用此方式手动添加

具体操作方式如下：

## **1.1 节点订阅引用（ss/ssr/vmess/https/trojan）**

引用（订阅）的节点，对应配置文件的 `**[server_remote]**` 部分，标准写法如下：

```YAML
[server_remote]
#可直接订阅 SSR，SS 链接，以及 Quantumult X 格式的 vmess/trojan/https 订阅
#虽然模块被叫做remote，但实际上可以使用远程订阅链接，也可以使用本地/iCloud文件路径进行引用
#远程订阅
https://raw.githubusercontent.com/crossutility/Quantumult-X/master/server.txt, tag = 示范订阅 1 (可删除), enabled=true
#本地文件，文件内为quanx可识别格式的服务器信息
server.txt, tag = 示范订阅 2 (可删除), enabled=true
```

当然，最方便的，也最推荐的，是在APP内UI中进行操作，具体如下

- 展开查看详细内容
    
    - 如果你机场提供 ss/ssr 订阅 以及 **`标明支持 quantumultX 格式的 V2/http/trojan 订阅`**，那你可以直接通过引用导入；
    - 如果只是**`普通的 v2ray 订阅链接`**，请参照 `[1.3 部分](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)` 利用api 进行转换导入
    - 如果是普通的 `**http订阅链接/trojan链接？**`，那算了，我也不知道什么机场会这样
    
    - 另外，最新TF版本增加了对订阅链接图标(`**图b**`)的支持
        - 进入配置文件, [server_remote], 在你的订阅后加上 ", img-url = xxxx.png "
        - 图片格式要求与策略组图标一致( `**3.4 部分**`)
    
    a. 操作步骤
    
    ![[Untitled 1.png]]
    
      
    
    b. 显示界面
    
    ![[IMG_5942.png]]
    
      
    

---

## **1.2 UI/文本 添加示范(ss/ssr/vmess/https/trojan)**

- 展开查看详细内容
    
    在上图中间部分，通过 添加/SS-URI/扫码 等方式将单条/多条ss/ssr 线路添加到本地，或
    
    文本编辑添加到配置文件的 **`[server_local]`** 部分，格式与其它app均有所不同，具体如下：
    
    ```YAML
    # 以下示范都是 ip(域名):端口，
    # 比如 vmess-a.203.167.55.4:777 ，实际是 203.167.55.4:777
    # 前面的 ss-a，ws-tls, vmess-a 这些，只是为了让你快速找到自己节点的类型
    # 实际使用时，请不要真的 傻乎乎的 写 vmess-a.203.167.55.4:777 这种。
    shadowsocks=ss-a.example.com:80, method=chacha20, password=pwd, obfs=http, obfs-host=bing.com, obfs-uri=/resource/file, fast-open=false, udp-relay=false, server_check_url=http://www.apple.com/generate_204, tag=Sample-A
    shadowsocks=ss-b.example.com:80, method=chacha20, password=pwd, obfs=http, obfs-host=bing.com, obfs-uri=/resource/file, fast-open=false, udp-relay=false, tag=Sample-B
    shadowsocks=ss-c.example.com:443, method=chacha20, password=pwd, obfs=tls, obfs-host=bing.com, fast-open=false, udp-relay=false, tag=Sample-C
    shadowsocks=ssr-a.example.com:443, method=chacha20, password=pwd, ssr-protocol=auth_chain_b, ssr-protocol-param=def, obfs=tls1.2_ticket_fastauth, obfs-host=bing.com, tag=Sample-D
    shadowsocks=ws-a.example.com:80, method=aes-128-gcm, password=pwd, obfs=ws, obfs-uri=/ws, fast-open=false, udp-relay=false, tag=Sample-E
    shadowsocks=ws-b.example.com:80, method=aes-128-gcm, password=pwd, obfs=ws, fast-open=false, udp-relay=false, tag=Sample-F
    shadowsocks=ws-tls-a.example.com:443, method=aes-128-gcm, password=pwd, obfs=wss, obfs-uri=/ws, fast-open=false, udp-relay=false, tag=Sample-G
    vmess=ws-c.example.com:80, method=chacha20-ietf-poly1305, password= 23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, obfs-host=ws-c.example.com, obfs=ws, obfs-uri=/ws, fast-open=false, udp-relay=false, tag=Sample-H
    vmess=ws-tls-b.example.com:443, method=chacha20-ietf-poly1305, password= 23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, obfs-host=ws-tls-b.example.com, obfs=wss, obfs-uri=/ws, tls-verification=true,fast-open=false, udp-relay=false, tag=Sample-I
    vmess=vmess-a.example.com:80, method=aes-128-gcm, password=23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, fast-open=false, udp-relay=false, tag=Sample-J
    vmess=vmess-b.example.com:80, method=none, password=23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, fast-open=false, udp-relay=false, tag=Sample-K
    vmess=vmess-over-tls.example.com:443, method=none, password=23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, obfs-host=vmess-over-tls.example.com, obfs=over-tls, tls-verification=true, fast-open=false, udp-relay=false, tag=Sample-L
    http=http.example.com:80, username=name, password=pwd, fast-open=false, udp-relay=false, tag=http
    http=https.example.com:443, username=name, password=pwd, over-tls=true, tls-verification=true, tls-host=example.com, fast-open=false, udp-relay=false, tag=http-tls
    trojan=example.com:443, password=pwd, over-tls=true, tls-verification=true, fast-open=false, udp-relay=false, tag=trojan-tls-01
    trojan=192.168.1.1:443, password=pwd, over-tls=true, tls-host=example.com, tls-verification=true, fast-open=false, udp-relay=false, tag=trojan-tls-02
    ```
    

## 1.3 👍️👍️资源解析器👍️👍️

版本 `**Quantumult X (v1.0.8-build253)**` 后，作者引入了资源解析器，可以用于所有 remote 资源的解析转换 ( 格式请看 [作者示范链接](https://github.com/crossutility/Quantumult-X/blob/master/resource-parser.js))。

所谓的资源解析器，其用途是将任何格式的 `**服务器订阅、规则、复写**`等资源，通过解析器转换成 Quanxtumult X 所支持的格式(当然，前提是解析器内有对应的处理模块)。

鉴于规则跟复写相关的 QuantumultX 规则已经比较齐全，但服务器订阅方面，仍旧有不少机场没有提供 QuantumultX 特有格式的片段引用。

所以，我写了一个粗略的节点资源解析器，用于将各种格式的订阅转换成QuantumultX 格式，并提供节点筛选、udp/tfo 开启，节点重命名以及旗帜 emoji 等简单功能：

> [!important]  
> 链接：https://github.com/KOP-XIAO/QuantumultX/blob/master/Scripts/resource-parser.js  

相比于常见的在线 API，资源解析器的最大优势：

- 完全本地解析，无暴露服务器风险;
- 无需 `**URLencode**` 步骤，直接填入原始订阅链接即可，更可直接使用中文参数(空格除外)

### A**. 添加方法**

0⃣️ 在Quantumult X 配置文件中`**[general]**` 部分，加入

```YAML
[general]
resource_parser_url=https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/resource-parser.js
```

> [!important]  
> ⚠️⚠️如提示"没有自定义解析器"，请长按右下角图标后点击左侧刷新按钮，更新资源，后台退出 app，直到出现解析器说明  

### B. 功能介绍

> [!important]  
> 主要功能: 将节点订阅解析成Quantumult X引用片段, 并提供下列可选参数(已支持 V2RayN/SSR/SS/Trojan/Quanx/Surge(conf&list)订阅)；附加功能：rewrite (复写) /filter (分流) 过滤，可用于解决无法单独禁用远程引用资源中某 (几) 条 rewrite/hostname/filter，以及直接导入 Surge 类型规则 list 的问题  

参数说明

0️⃣ 请在订阅链接后加入 "#" 符号后再加参数, 不同参数间请使用 "&" 来连接, 如:

```YAML
https://mysub.com\#in=香港+台湾&emoji=1&tfo=1
#如果是本地资源引用，请将参数 "\#in=xxx" 填入资源文件第一行 （参考图 C）
```

1️⃣ ”节点“订阅--参数说明

- in, out, 分别为 保留/排除, 多参数用 "+" 连接(逻辑"或"), 逻辑"与"请用"."连接，可直接用中文, 空格用"%20"代替 (如 "`in=香港.IPLC.04+台湾&out=香港%20BGP`" )
- regex , 利用正则表达式以筛选节点
- emoji=1,2 或 -1, 为添加或删除节点名中的 emoji 旗帜 (国行设备请用 emoji=2 )
- udp=1/-1, tfo=1/-1 参数开启 udp-relay 及 fast-open
- rename 重命名, rename=旧名@新名, 以及 "前缀@", "@后缀", 用 "+" 连接, 如 "`**rename=香港@HK+[SS]@+@[1X]**`"
- delreg 参数，利用正则表达式以删除节点名中的字段
- replace 参数，正则替换 server 中的内容，可用于重命名、更改加密方式等需求
- cert=0，跳过证书验证(vmess/trojan)，即强制"`**tls-verification=false**`"
- tls13=1, 开启 "tls13=true"(vmess/trojan), 请自行确认服务端是否支持;
- sort=1 / -1 / x , 排序参数，分别根据节点名 正序 / 逆序 / 随机 排列;
- info=1, 开启通知提示流量信息(前提：原订阅链接有返回该信息)，默认关闭;

2⃣️ ”rewrite(复写)/filter(分流)“ 引用--参数说明

- 分流、复写规则 筛选参数 "`**in=xxx**`" 以及 "`**out=xxx**`", 多个参数用 "+" 连接；
- 主机名筛选参数 "inhn=xxx" 以及 "outhn=xxx", 多个参数用 "+" 连接；
- regex，利用正则表达式以筛选分流规则、重写、主机名等
- 分流规则额外支持 "policy=xx" 参数, 可用于直接指定策略组，或者为 Surge 格式的 rule-set 生成策略组(默认"Shawn"策略组)

3⃣️ 通用参数：ntf=1, 用于打开资源解析器的提示通知 (默认关闭),

- rewrite/filter 类型则会强制在有 out 参数时开启通知提示被删除（禁用）的内容，以防止规则误删除

### B. 使用示范

**I. 节点订阅 (图A)**

1⃣️ 假设你的订阅连接为: **`https://raw.githubusercontent.com/crossutility/Quantumult-X/master/server-complete.txt`**

2⃣️ 假设你想要保留的参数为 `**in=tls+ss**`, 想要过滤的参数为 `**out=http+2**`, 请注意下面订阅链接后一定要加 ”#“ 符号

3⃣️ 则填入 Quanx 节点引用的的总链接为 `**https://raw.githubusercontent.com/crossutility/Quantumult-X/master/server-complete.txt\#in=tls+ss&out=http+2**`

4⃣️ 填入上述链接并打开的资源解析器开关

**II. 分流规则、重写规则 的解析（图B）**

同上，具体参数可见解析器说明

```Shell
[filter_remote]
https://Advertising.list\#policy=Shawn&out=aweme, tag=🚦去广告，update-interval=86400, opt-parser=true, enabled=true
```

**III. 本地片段引用（图C）**

适用场景：

- 添加单条 vmess/trojan 的 uri链接：vmess://xxxx...;
- 临时添加节点，但不想放到 local 里无法分组
- 本地规则、复写的操作

### C. 效果示范

A. 节点订阅转换/过滤

![[IMG_6456.jpg]]

B. rewrite 复写引用过滤

![[Untitled 2.png]]

C. 解析本地资源引用示范

![[Untitled 3.png]]

  

## 1.4 ⚠️⚠️进阶教程：节点订阅第三方 API 的使用⚠️⚠️

> [!important]  
> 解析器目前已经实现了API的绝大部分功能，所以更加建议使用资源解析器。  

但如果对API情有独钟的，仍旧可以参照以下使用教程

之所有需要第三方 API，主要有三个作用：

> [!important]  
> 1 - ss/ssr/v2ray 订阅不包含 UDP 跟 TFO 参数，第三方 api 可以解决；2 - 有时不想要订阅内所有的节点，第三方 api 可以过滤筛选；3 - QuantumultX 暂时不支持V2RayN 订阅链接, 以及surge的托管及list资源，第三方 api 可以提供转换  

**下面是常用的三个第三方 API，按需选择使用 (**==**对于Quantumult X 来说，第一个就够用了**==**)**

我自己写的 API：

> [!info] &nbsp&nbspQuantumultX-Surge-Clash-订阅转化  
>  
> [https://dove.589669.xyz/web](https://dove.589669.xyz/web)  

  

Fndroid 大佬的 API

> [!info] Fndroid的日常  
> 新API开放： Surge托管生成QuantumultX格式订阅地址 接口： 1.  
> [https://t.me/fndroid_news/416](https://t.me/fndroid_news/416)  

Tindy X的超全能 API 在线版本

> [!info] Subscription Converter  
> Utility to convert between various subscription format  
> [https://subcon.dlj.tf/](https://subcon.dlj.tf/)  

以下说明仅针对第一个 API ([`**KOP-XIAO- QuantumultX-Surge-API**`](https://dove.589669.xyz/web))，API可实现的功能较多，下面会挑几个常用的具体示范。其它请自行参考相应参数跟使用说明

### A. UDP & TFO 参数

由于普通的 ss/ssr/v2ray 订阅中不含 UDP/TFO 参数，所以远程引用导入后，quantumultX 也默认将其设置为：`udp-relay=false，这样可以确保节点不支持 udp 转发时，不会影响使用。`

由于F大懒，所以我自己写了一个可以将各种订阅转换成 quanx 格式的的API，分别将**`ssr订阅`**/ **`ss订阅`** 转换成`quantumultx`的格式，并可自己打开udp跟tfo参数：

```HTML
udp/tfo=1 表示打开udp跟tfo参数的开关（true）；
udp/tfo=0 表示关闭udp跟tfo参数的开关（false）
目前quantumult X 中，不支持 v2ray 的 udp 转发，所以上述参数对 V2 无效
```

当然， 如果你确认你的节点支持 udp 转发，可手动导入本地，并添加：`udp-relay=true`

### B. ㊙️ 节点list 过滤 ㊙️（利用参数过滤节点)

订阅里可能节点很多，而你只想要其中一部分，那么你可能就需要API来帮你过滤节点了

你可以使用正则参数：filter

如果不会正则，则可以使用简化的参数 in 跟 out来实现同样目的

> [!important]  
> 如果你不想手动 urlencode 之类，请直接去 API网站 操作  

1. 你的订阅链接为 ： https://example.com，urlencode 之后为：https%3A%2F%[2Fexample.com](http://2fexample.com/)
2. 则sub参数为：`**sub=https%3A%2F%2Fexample.com**`
3. 你想保留节点中名字包含“香港”的节点，则 `**in=%E9%A6%99%E6%B8%AF**`
4. 你想去掉节点中 4倍率 节点(名字为 4X)， 则 `**out=4X**`

最后链接为

```Python
https://dove.589669.xyz/all2quanx?&sub=https%3A%2F%2Fexample.com&in=%E9%A6%99%E6%B8%AF&out=4X
```

然后填入Quantumult X的 `**节点/引用**` 即可

这里只说几个注意事项：

1. 订阅链接请先[urlencode](https://www.urlencoder.org/)之后再接入 sub 参数后；
2. API中的filter的正则参数同样需要先行UrlEncode；
3. 正则过滤请先用 .*开始，比如你想要名字中含 `**游戏**` 的节点，拿 `**.*游戏**` **放到 urlencode 网站进行 encode，结果** .%2A%E6%B8%B8%E6%88%8F，那么过滤的正则表达式为：  
      
    `filter=.%2A%E6%B8%B8%E6%88%8F`

```Python
#示范，只选择某ssr订阅中(https://example.com)，名字中含有 “游戏” 的节点，并添加国家地区emoji
https://dove.589669.xyz/all2quanx?&tfo=1&udp=1&emoji=2&filter=.%2A%E6%B8%B8%E6%88%8F&sub=https%3A%2F%2Fexample.com
```

### C. list订阅&策略组的绑定

> [!important]  
> 在将节点按地区或功能分类后，有一种需求，是将策略组与节点订阅绑定，从而在节点增减时，策略组也能随之同步（类似 surge 的 policy-path，clash 的 proxy-provider）  

然而 Quantumult X开发者觉得这种设计不够灵活，因此只是隐性的支持了这种操作，下面就将给出操作示范: 将Dler的IPLC节点单独订阅，并捆绑策略组

**最新版本1.0.10后，提供** `**两种**` **将 节点订阅 与 策略组绑定 的方法 (原先的 ui 绑定操作已无效)**

1. **通过 as-policy 参数绑定**

新版本中，可通过在 `**[server-remote]**` 中指定 `**as-policy**` 参数，从而生成相应策略组并绑定：

```JavaScript
[server-remote]
https://xxxx.server.com, tag=Hong Kong, as-policy=static, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/HK.png, enabled=true
;这样就会生成一个叫Hong Kong的策略组, 类型是static, 由 as-policy决定
```

  
这样就会生成一个叫Hong Kong (tag参数决定)的策略组, 类型是static (由 as-policy参数决定)  

同样可以 **`as-policy = available`**

或者 **`as-policy=round-robin`**

绑定后，策略组中节点也将随订阅的变动而自动更新变动

**2. 👍👍regex 参数👍👍**

相比于 as-policy，新 regex 参数更加灵活与强大，具体使用请见[3.6 部分](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)

> [!important]  
> ⚠️ ⚠️ Quantumult X 的 regex 筛选只适用于 server_remote 的节点 ⚠️ ⚠️  

## **1.5 节点/订阅 后续操作**

- 长按`节点`模块，可进入`订阅列表`
- 订阅列表里可 `左/右 ↔️ 滑动`，进行图中对应操作，以及`长按` 对订阅进行排序；
- 列表的每个链接的 `右上角`，会显示最近一次的 `更新时间`

![[Untitled 4.png]]

---

# 2⃣️ 分流规则导入[filter_remote/local]

---

QuantumultX目前提供规则 `**==手动本地添加/ 远程引用==**` 两种方式：

## **2.1 本地手动添加**

可以直接在UI添加，也可以在`**配置文件**`中编辑添加，

也可以在`**网络请求记录**`中 找到对应记录，点击右上角漏斗符号直接添加

这些方式都适合 `临时 调整/测试` 规则

A. 分流规则/添加

![[STIIITCH_2019_07_13_05_23_49.jpg]]

B. 网络活动 添加/修改

![[IMG_2775.jpg]]

C. 分流规则页 查看/修改

![[Untitled 5.png]]

## ~~**2.2 导入 （订阅规则到本地**~~**）此方式已取消**

- 提供两个常用规则订阅：
    
    1. [基于lhie1](https://github.com/lhie1/Rules/tree/master/Quantumult): （9K条 跟 2K条）
        - [https://raw.githubusercontent.com/lhie1/Rules/master/Quantumult/QuantumultX.conf](https://raw.githubusercontent.com/lhie1/Rules/master/Quantumult/QuantumultX.conf)
        - [https://raw.githubusercontent.com/shigalin/Config/master/QuantumultX.conf](https://raw.githubusercontent.com/shigalin/Config/master/QuantumultX.conf)
    2. [神机规则](https://github.com/ConnersHua/Profiles/tree/master)：（1K+条）
        - [https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Pro.conf](https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Pro.conf)
    
    由于quantumult 提供独有的规则个性化选项，所以导入规则时，又分两种情况：
    
    ### Case 1 : 无自定义策略组
    
    - 此时规则会直接添加到本地：
    
    ![[Untitled 6.png]]
    
    ### Case 2: 已有自定义策略组(图中 😄TEST😢)
    
    - 会跳出替换面板供分流选择
    
    ![[Untitled 7.png]]
    
      
    

## **2.3 引用 （远程订阅）— 👍👍 推荐**

### A. 整体规则引用(❎️不推荐❎️)

你依旧可使用上述2.2中提供的规则链接进行引用，但缺点明显，所以不建议：

- 因为他们都是整体规则，单独调整不灵活；
- 规则内依旧按照quantumult的个性化方式填写(比如：“Apple策略组，不懂选Direct“这种策略组名)，而quantumultX已经不提供替换面板，因此会生成奇奇怪怪的策略组名

### B. 👍👍 rule-list 引用 👍👍

**规则引用&个性化** 功能，使得Quantumult X的分流规则变得更加强大跟灵活（类似与Surge的Rule-Set 方式），可以将规则更为细分，比如Netflix YouTube之类单独订阅规则，因此推荐此方式

> [!important]  
> 相同规则，在上面的优先生效，所以自己按需进行排序：比如神机规则中 global.list 已经包含了 telegram 分流 , ForeignMedia.list包含了 YouTube 等分流，如果你要对 YouTube/telegram 进行单独设定，请将 YouTube.list 放于 ForeignMedia.list 前面；telegram.list 放在 Global.list前面  

目前，神机规则已经提供完整的 QuantumultX 的rule-list，**==点击下方链接查看教程==**  
(⚠️  
`请勿尝试直接引用导入此链接`⚠️)

- [https://github.com/ConnersHua/Profiles/tree/master/Quantumult/X/Filter](https://github.com/ConnersHua/Profiles/tree/master/Quantumult/X/Filter)
- 以及多媒体细分规则 list:
    
    - [https://github.com/ConnersHua/Profiles/tree/master/Quantumult/X/Filter/Media](https://github.com/ConnersHua/Profiles/tree/master/Quantumult/X/Filter/Media)
    
      
    

**⚠️⚠️ list 的raw链接获取步骤：**

![[Untitled 8.png]]

分流订阅在配置文件中对应模块为 `**[filter_remote]**` **,具体格式如下**

```YAML
[filter_remote]
#远程分流模块，可使用 force-policy 来强制使用策略偏好
#跟节点引用一样，可以使用远程链接，也可以使用本机/iCloud文件路径
#远程链接
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Advertising.list, tag=🚦去广告，enabled=true
#本地文件
advertising.txt, tag=🚦去广告，forcr-policy=reject, enabled=true
```

### I. **使用方法：**

> [!info] QuantumultX 的rule-set导入方式  
> Rule-Set的分list方式，相比起来更加灵活方便，推荐使用 A.  
> [https://telegra.ph/QuantumultX-的rule-set导入方式-06-28](https://telegra.ph/QuantumultX-的rule-set导入方式-06-28)  

- A. UI 添加：（点击展开查看）
    
    1. 点进对应的list，找到raw链接（Apple.list 为例）：[https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Apple.list](https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Apple.list)
    2. 填入QuantumultX的分流规则引用，自行决定是否"`**策略偏好**`"替换策略组名
        - 不勾选“`**策略偏好**`”，将会自动创建名叫 **Apple** 的策略
    3. 同理，加入其它你需要的其它list规则类别
    
    ```HTML
    1️⃣: 去广告  https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Advertising.list
    
    2️⃣: 苹果相关 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Apple.list
    
    3️⃣: 国内 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/China.list
    
    4️⃣: 国内视频 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/DomesticMedia.list
    
    5⃣️ Netflix相关 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Media/Netflix.list
    
    6⃣️ YouTube相关 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Media/YouTube.list
    
    7⃣️ 国外视频 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/ForeignMedia.list
    
    8⃣️ 国外路线 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Global.list
    
    9⃣️ 运营商劫持 https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Hijacking.list
    ```
    
    按图片操作
    
    ![[IMG_5967.jpg]]
    
- B. 文本统一添加：(点击展开查看)
    
    放入配置文件`**/编辑/[filter_remote]**`下
    
    ```HTML
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Advertising.list, tag=去广告, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Apple.list, tag=苹果相关, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/China.list, tag=国内, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/DomesticMedia.list, tag=国内视频, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Media/Netflix.list, tag=📺Netflix, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Media/YouTube.list, tag=🎬Youtube, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/ForeignMedia.list, tag=国外视频, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Global.list, tag=国外, enabled=true
    
    https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Hijacking.list, tag=运营商劫持, enabled=true
    ```
    
    提供tag,force-policy,enabled等三个参数说明:
    
    - tag - 标签 ：
        
        ```HTML
        tag = 去广告
        ```
        
    - force-policy，强制用自定义策略组替换规则中的策略组名：
        
        ```JavaScript
        force-policy = 📺 Netflix专用
        ```
        
    - enabled，是否生效/禁用：
        
        ```HTML
        ;生效
        enabled=true
        ;禁用
        enabled= false
        ```
        
        **示范：**https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Advertising.list, tag=去广告, force-policy= 🈲️广告, enabled=true
        
          
        

- C. 规则转换API的使用
    
    ~~目前好像还没人直接提供 quantumultx 方式~~~~`细分的流媒体规则`~~~~，所以可以用 F 大的 api 跟 surge 的细分 rule-set(lhie1 跟神机都有)进行转换：~~
    
    神机规则现已经提供细分的流媒体规则，可见[上方](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21) ， 但依旧可以用Fndroid的API进行其它处理：
    
    1. 直接自定义policy名字；
    2. 用在其它仍未支持quanx格式的list上
    
    1️⃣格式： http://cloudcompute.lbyczf.com/x-rule-set?url={ 细分的流媒体 surge 的rule -set链接}&policy={强制策略组名，名字含中文或者emoji的话，先去`urlencode`}
    
    如 🎬Youtube：%F0%9F%8E%ACYouTube
    
    如 📺Netflix：%F0%9F%93%BANetflix
    
    > [!important]  
    > 如果你是直接通过QuantumultX的文本编辑写入配置的话，可以不用urlencode  
    
    2️⃣示范：
    
    ```HTML
    http://cloudcompute.lbyczf.com/x-rule-set?url=https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/YouTube.list&policy=%F0%9F%8E%ACYouTube
    http://cloudcompute.lbyczf.com/x-rule-set?url=https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/Netflix.list&policy=%F0%9F%93%BANetflix
    ```
    

## 2.4 **后续操作(⚠️⚠️策略组使⚠️⚠️)**

### **A. 引用规则编辑**

- 同样通过`长按` `分流规则` 进入 `规则订阅列表`；
    - 左右↔️ 滑动，长按 等操作

### **B.⚠️⚠️策略组操作👈️👈️**

- a. QuantumultX导入上述分流规则后，会自动建立 force-policy 或规则中自带的策略组，比如：Youtube， Netflix , Foreign Media 等等;
- b. 长按这些策略组名，你会发现里面默认加入了 Direct/Reject 两个内置策略，如果你想要你的 YouTube/Netflix/Foreign Media 等走你希望的节点，请在此页面手动添加/移除服务器
    - 长按 `策略组` ，进入编辑页面，`**添加/删除/排序**` 等操作

![[Untitled 9.png]]

![[Untitled 10.png]]

---

---

# 3⃣️ QuantumultX 策略组[policy]

---

策略组的存在，使得 Quantumult/QuantumultX 以及 Surge/Clash 分流灵活性大大强于其它同类APP  
关于策略组的理解跟使用，可以参考  
`**Fndroid**`**大佬** 的这篇文章：

[https://github.com/Fndroid/jsbox_script/wiki/关于策略组的理解](https://github.com/Fndroid/jsbox_script/wiki/%E5%85%B3%E4%BA%8E%E7%AD%96%E7%95%A5%E7%BB%84%E7%9A%84%E7%90%86%E8%A7%A3)

或者🌶️🐤壮壮的二次解读文章：  
  
[https://zhuangzhuang.cf/2019-03-20/proxygroup/](https://zhuangzhuang.cf/2019-03-20/proxygroup/)

而 QuantumultX 在 quantumult 的基础上，调整并优化了其策略组的玩法，具体如下

## 3.1 策略组说明

```YAML
[policy]
; static policy points to the server in candidates you manually selected.
// Static静态策略组，即你手动选择 节点/子策略
; available policy points to the first available server in candidates based on server_check_url(concurrent url latency test will be launched when the policy has been triggered).
// Available 可用性策略组：选择列表里 第一个可用的节点 （url-test不超时）
; round-robin policy points to the next server in candidates for next connection.
// round-robin 轮询策略组：按请求依次使用列表中的节点
; ssid policy points to the server depending on the network environment.
// ssid策略组，根据Wi-Fi网络的的ssid名, 移动网络，切换节点/策略
以下是具体写法，千万记得要去掉 ；号才会生效

;static=policy-name-1, Sample-A, Sample-B, Sample-C,img-url=https://example.com/icon.png
//静态策略组，static=策略组名,节点 1, 节点 2,策略组-C
;available=policy-name-2, Sample-A, Sample-B, Sample-C,img-url=https://example.com/icon.png
//可用性策略组，available=策略组名,节点 1,节点 2,节点 3
;round-robin=policy-name-3, Sample-A, Sample-B, Sample-C,img-url=https://example.com/icon.png
/轮询策略组，round-robin = 策略组名, 节点 1, 节点 2,节点 
;ssid=policy-name-4, Sample-A, Sample-B, LINK_22E171:Sample-B, LINK_22E172:Sample-C,img-url=https://example.com/icon.png
//ssid策略组，ssid=你的组名,4g下默认策略,Wi-Fi下默认策略, wifi-A:策略 A, wifi-B:策略 B
;------------
;以下为进阶玩法（版本 1.0.10 291+）详细介绍看 3.6 小节
;通过正则表达式将某些订阅或某些节点添加到策略组中（同时添加两参数时取交集)
;static=policy-name, resource-tag-regex=^sample, server-tag-regex=^example, img-url=https://example.com/icon.png
```

总结，QuantumultX 总共提供 4 种类型策略组，

- static静态策略组，==可以==嵌套其它所有类型的策略组，**`需自己手动选择路线/子策略组`**；
- Available 健康检查策略组，只可直接套用节点，不可嵌套其它策略组，自动选择**`第一个可用的节点`****(需要至少****`两个`****节点)**；
- Round-Robin轮询策略，只能直接套用节点，不可以嵌套其它策略组，按网络请求**`轮流使用所有节点`**；
- SSID策略组，自然也是可以套用其它类型的策略组，**`根据 网络/Wi-Fi 切换 节点/策略`**

## 3.2 策略组的添加 & SSID 策略组实例

### A. 策略组的自定义添加

目前，QuantumultX中添加策略组有三种方式：

a. `文本编辑`添加, 支持所有类型的策略组（点 `右下角图标/配置文件/编辑/[policy] 部分`）

- 此方式支持所有类型策略组的添加

b. 在`节点订阅列表`中，选中， `右滑动/更多`，即可将 **`该订阅链接内所有节点`** 直接绑定生成 一新策略组（**==此方式生成的策略组，将与订阅链接绑定，节点也跟随链接改变==**）

- 支持生成类型：`**static静态策略，available健康检查策略，round-robin负载均衡策略**`

c. 添加订阅时，直接通过`**as-policy**`参数生成并绑定策略组（[1.3 节 C部分](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)）

- 支持生成类型：`**static静态策略，available健康检查策略，round-robin负载均衡策略**`

### B. SSID 策略组添加实例

下面，以难度最大的SSID 策略组作为具体示范，具体写法：

`**ssid= 组名,4g下默认策略/节点, Wi-Fi下默认策略/节点, wifi-A:策略/节点 A, wifi-B:策略/节点 B, wifi-C: 策略/节点 C**`

```HTML
ssid = 🏠 SSID Group,🇭🇰 HK Group,🇭🇰 HK Group,ASUS_5G:🇲🇴 MO Group ,AMG-5G: direct
;具体解释如下
;组名：🏠 SSID Group
;蜂窝网下默认策略：🇭🇰 HK Group， Wi-Fi下默认策略：🇭🇰 HK Group
;ASUS_5G 这个 Wi-Fi下走：🇲🇴 MO Group ， AMG-5G 这个 Wi-Fi下走直连：direct
; AUSS_5G 跟 AMG-5G 是我的 Wi-Fi 名字，而 🇭🇰 HK Group, 🇲🇴 MO Group是我的策略组 ；
; 请按需改成你自己的节点或策略组，别傻乎乎直接全部照搬。。。
```

![[Untitled 11.png]]

**==如果你实在不会😢, 按下图1⃣️2⃣️3⃣️操作==**

![[48AEC7A2-6EFE-4CBF-A09E-27304150BE3C.png]]

> [!important]  
> 添加完后，请千万记得看下一部分  

## 3.3 ⚠️⚠️策略组的生效⚠️⚠️

> [!important]  
> 很多人存在一个误解，以为自己添加了一个策略组，那么，软件就能按照设定的策略组开始随心所欲的进行分流😢（... 🧠呢？）- 比如你规则里写明了：host-keyword, google, direct- 那么凡是匹配了关键词google的所有连接，都将走direct（直连），就算你建了100个能上天的策略组，那又如何？  

总之，策略组的存在也是为规则服务的，策略组建立后，需要`配合添加到规则当中`，才可能生效，下面是关于 3.2中SSID策略组生效的示范：

### A. 直接引用生效

1⃣️ 建立名为 “`🏠 SSID Group`“ 的策略组；

2⃣️ 加入想要的规则生效：长按 `**分流规则**`**，进入**`**分流资源列表**`：

- 比如我想让 `**list A 分流规则**` 走该 `**SSID策略组**`，那么⬅️`**左滑编辑**`该分流list；
- 如果想让某新的list走该ssid策略组，则进入`**分流(资源列表)**`后，点 `**右上角+**`

![[Untitled 12.png]]

### B. 间接引用生效

上述利用规则直接指向策略组，这只是一种生效方法。

你可以利用策略组嵌套，来间接使其生效：

比如 上述规则指向 `🌍Global` 策略组，而 `🌍Global` 中嵌套并选中了 `🏠 SSID Group`

![[IMG_5014.png]]

  

## 3.4 🚥策略组图标自定义

此为开发者提供额外福利，可骚气 自定义策略组的图标，通过策略组看片指日可待。

![[IMG_3143.jpg]]

### A. 操作方法（分本地/远程两种方式）

I. 本地文件法

文件可放在 本机，也可放在 iCloud 对应文件夹下(需在Quantumult X 中打开 iCloud 开关)

- `图片格式`：PNG后缀(==大/小写均可==)，大小`108*108`像素(强制)，建议图片无背景(保留alpha通道)  
      
    `文件夹路径`：a. 将图片放在 ==on My iPhone(我的iPhone)/Quantumultx/Images== 下  
    b. 放在  
    ==iCloud/Qantumult X/Images== 下，记得去quantumultX 设置中开启 iCloud  
      
    `名字要求`：这里又分两种方式：  
    1. 跟你想要的⚠️⚠️  
    **`策略组 同名`** ⚠️⚠️，比如 `🍏 Apple.PNG` ，`📺 Netflix.PNG` ；  
    2. 不管名字(比如名字叫  
    **==1.png==**)，但需要在对应的策略组后协商图片名字，格式如：  
      
    ==static=Netflix, 节点1, 节点2 , 策略组1 , 策略组2 , img-url= 1.png==  
      
    `生效方式`：以上确认无误后，后台关闭quantumultX并重开生效

II. 远程链接法（👍推荐👍）

```HTML
远程示范图片链接为：
https://raw.githubusercontent.com/crossutility/Quantumult-X/master/icon-samples/youtube.PNG
```

```HTML
文本编辑配置文件 [policy] 部分, 在你想要修改icon的策略组那，加上 “ img-url=图片链接“， 如
static=YouTube,  节点1, 节点2 , 策略组1 , 策略组2 , img-url= https://raw.githubusercontent.com/crossutility/Quantumult-X/master/icon-samples/youtube.PNG
```

---

---

如果文字看不懂，直接看下面图片示范步骤（图片来自Zealson）：

![[Untitled 13.png]]

![[Untitled 14.png]]

**辅助工具**：

1⃣️ 图片网站：[icons8](https://icons8.cn/icons/set/youtube) ， [阿里iconfont](https://www.iconfont.cn/home/index?spm=a313x.7781069.1998910419.2) ， [icon for everything](https://thenounproject.com/) ，[PNG Mart](http://www.pngmart.com/) ，[开发者提供](https://github.com/crossutility/Quantumult-X/tree/master/icon-samples)

2⃣️ Fndroid的jsbox脚本(`将相册中图片转成108*108大小，命名后 手动导出到上述路径`)

![[QuanX.box]]

3⃣️ 设计师Zealson的icon项目(👍推荐👍)：

> [!info] Koolson/Qure  
> Qure是一套专为 Quantumult X内策略组而精心设计的图标组。在这里你可以订阅、下载并更新它们。 跨设备同步策略组图标，及时获取图标更新 该操作以Quantumult X v1.  
> [https://github.com/Koolson/Qure](https://github.com/Koolson/Qure)  

### B. 效果示范：

- 龙珠系列：
    
    ![[STIIITCH_2019_08_10_12_41_34.png]]
    
- 东京热系列：
    
    ![[IMG_3145.jpg]]
    

- 混搭系列：
    
    ![[STIIITCH_2019_08_09_07_11_13.png]]
    

  

- 返璞归真系列：（图片来自**`群友Zealson`**）
    
    ![[2019-08-11_21.07.25.jpg]]
    

- 天道合一系列: (来自**`tg之神 - 李哥`**)
    
    ![[5EA3EF9E-69F1-4C45-BE20-E4811AECB170.jpeg]]
    

### C. 资源下载 ⏬

附上下面3⃣️个资源，供大家享用。（有需求的还是自行去网络搜集资源）

![[108.zip]]

![[Quantumult X 不完全教程 0a71ba8e36664e7c89d72911f86d69f2.zip]]

`来自Yeebee`

![[Quantumult_X_Policy_Icons_v1.0.0_by_zealson.zip]]

`来自 Zealson`

  

## 3.5 策略组的删除

这原本是毫无必要的一个章节，无奈太多人完全不动脑子，只知道张口就问：

> "`**我添加了策略组，怎么删不掉啊？**`**"**

删除策略组前，请先搞清楚你的 **策略组** 的来源

1. 策略组由规则 list 自动生成
    - 你要么删除那条list，要么用“强制策略”的方式，使改规则list走其它的策略；
    - 然后，你回到 `**配置文件 [policy]**` 部分，删除对应策略组
2. 策略组本就是你手动添加
    - 那么，先确认你没有额外的规则指向该策略；
    - 然后，同上，文本编辑删除即可

否则，你可能会一直面对 `**“我明明删除了，怎么它又自动回来了”**` 的疑问❓️

如果你连配置文件在哪编辑都不知道，请返回第 0⃣️部分

## 3.6 👍️👍️策略组进阶玩法(regex正则筛选)

(以下内容转自 [https://t.me/QuanXNews/119](https://t.me/QuanXNews/119) )

> [!important]  
> ⚠️ ⚠️ Quantumult X 的 regex 筛选只适用于 server_remote 的节点 ⚠️ ⚠️  

### A. 参数说明&使用

![[Untitled 15.png]]

**新增参数：**

- `**resource-tag-regex**`: 根据订阅名(tag)来筛选节点
- `**server-tag-regex:**` 根据节点名来筛选节点

**策略组根据 订阅 tag 或 节点 tag 筛选节点 版本要求：**1.0.10 build 291 或以上

**功能说明：**

- 通过正则表达式将某些订阅或某些节点添加到策略组中（同时添加两参数时取交集）

- 支持 static, available, round-robin 类型策略组

- 当筛选结果为空时，走直连

- Available 策略组可仅包含一个节点

- 只能与direct，proxy 等内置策略组混搭

**格式示范：**

```Shell
[policy]
;策略类型=策略名, resource-tag-regex=筛选订阅 tag 的正则, server-tag-regex=筛选节点 tag 的正则, img-url=策略组图标地址
static=policy-name, resource-tag-regex=^sample, server-tag-regex=^example, img-url=https://example.com/icon.png
```

### B. 参数优点

**新regex参数与 as-policy 比较**（[1.3 节 C部分](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917?pvs=21)）**：**

- as-policy 生成的策略组均在 [policy] 中的策略组的右侧，无法进行排序；新参数可实现将策略组与订阅进行绑定，取代 as-policy，从而进行排序；

- 相比于通过使用 as-policy 与 API/解析器 结合分组，新参数可仅使用一条机场订阅链接，无需重复添加；

- 使用 as-policy 参数，多个订阅链接（例如多机场使用者）需要生成多个策略组，而通過新参数可将不同订阅的节点添加到同一策略组进行关联，例如：

- resource-tag-regex=Dler Silver|Dler Gold
- server-tag-regex=🇹🇼|TW|Taiwan|台湾|台北|台中|新北|彰化|CHT|台|HINET

> [!important]  
> 整体来说，新 regex参数，比 as-policy 好用强大灵活太多，推荐使用  

  

---

---

# 4⃣️ Rewrite/MITM 解密

---

复写跟 mitm 用于去广告，以及某些重定向，比如将 `**google.cn**` 重定向 `**google.hk**`

而接下来的js部分，也是集成在QuantumultX的rewrite模块中。此部分功能强大，但也相对复杂

一般用户而言，订阅某几位大佬的复写规则即可

配置文件中，对应为 `**[rewrite_remote]**` 以及 `**[rewrite_local]**` 模块, 分别为引用，以及本地

其中remote引用模块，可以引用远程链接，以及本机/iCloud路径下的文件

```YAML
[rewrite_remote]
#远程复写模块，内包含主机名 hostname 以及复写 rewrite 规则
# 远程链接
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Rewrite.conf, tag = 神机复写规则，enabled=true
#本地/iCloud 引用
rewrite.txt, tag=本地复写, enabled=true
```

而local模块，则如下所示，相当于将远程的内容复制到本地模块下

```YAML
[rewrite_local]
^http://example\.com/resource1/1/ url reject
^http://example\.com/resource1/2/ url reject-img
```

![[Untitled 16.png]]

## 4.1 . Rewrite 部分

提供一个rewrite订阅链接：（本地文件 或 远程链接 引用 两种方式都可以）

- 神机：
    - [https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Rewrite.conf](https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Rewrite.conf)

## 4.2 . MitM 部分

UI里自行生成 (`**生成→安装→信任**`)，  
如提示规则里已带有证书信息，直接"  
`**安装→信任**`"

```Shell
QuamtumultX的mitm解密:
配置文件/编辑,最下方
[mitm]
passphrase = xxx(quan/surge里找)
p12 = xxx(quan/surge里找)
```

---

## 4.3 . **HTTPS 调试**

**日志模块/长按，下方** `**开启 https 调试**`

> [!important]  
> 平时建议关闭  

  

---

---

---

# 5⃣️ URL-Scheme/配置导入与同步

---

## 5.1 整个配置导入(👍👍懒人/小白推荐👍👍)

build 80 之后提供完整配置url导入方式：

### a. **示范配置链接**：

包含：

1.`神机分流规则，包含 YouTube 跟 Netflix 的分流`，精简到7个策略组；

> 其中，`🕹 黑/白名单` 控制 Final 走的策略（即上面规则没匹配到的剩余请求）

2. 常用 dns部分；

3.`神机`的rewrite部分；

4. 自制的geo-checker 的js脚本，使用的是ip-api数据库;

5. 内置 img-url 参数，默认为Qure 系列对应的 icon

![[Untitled 17.png]]

**导入链接：**

```Shell
https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/QuantumultX_Profiles.conf
```

### b. **使用方式**：

复制上述链接，按下图中' ⚠️ 0⃣️ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ ' 操作即可：

导入链接 → 导入服务器 → 策略组按需选择分流配置 → 开启 rewrie/mitm 开关

> [!important]  
> ⚠️当然，记得 长按右下角图标，选择 三色的规则分流模式  

![[STIIITCH_2019_08_08_10_16_52.jpg]]

---

## 5.2 配置关联绑定(类似托管👍️👍️)

> [!important]  
> 正式版 1.0.8 之后，Quantumult X 终于支持了所谓的 “远程托管” 与“iCloud配置同步”  

### a. 说明

与 `**5.1 部分**`的导入不同，托管绑定的配置，会自动更新完整配置文件，支持 `**远程/本地/iCloud**`，展开来说：

1. 绑定`**远程配置**`时，APP内可以修改操作，但下次更新时，会被远端配置覆盖（所以适合机场托管使用）；
2. `**引用 iCloud**` 下的配置文件时，APP内作修改操作，会立即生效到配置文件本身。如果你另外的设备也是使用同一份配置，那么就能多设备同步配置生效（适合多设备用户）

### b. 使用方法

**文字版：**

- 设置中，打开右上角的 “关联” 按钮 ；
- 填入配置 链接/路径 (例如我的配置放在iCloud的 `**Quantumult X/Profiles**`文件夹下，名为 `**QX01.txt**` )，即可关联成功

> [!important]  
> ⚠️⚠️注意，QX01.txt 只是我的文件名(QX01)以及格式(.txt)，⚠️⚠️请别傻乎乎照搬  

- 可能你注意到了关联成功后，右上角的 `**悟空图标符号**` **。**没错，那是通过在配置文件的 [general]下添加 `**profile_img_url**` 参数实现的
    
    ```Python
    ;图片地址可远程，可本地
    ;图片为108*108的png格式，PNG与png大小写敏感
    profile_img_url= https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/img/dragonball/1.PNG
    ```
    

**图片版**

![[IMG_6266.jpg]]

### C. 注意事项

1. 绑定后可以`解除关联`，也可`手动更新`；
    - iCloud上的配置引用会实时更新
2. 暂时未支持同时显示多份配置关联 (但估计快了)
3. 如果你多设备上使用同一配置，但 `**task**` 类签到任务只需要在某一设备上执行，你可以去其它设备上关闭 `**task**` 开关
    
    ![[IMG_6267.jpg]]
    

  

## ~~5.3 URI 导入~~

- 由于此方式比较折腾且低效率，有兴趣者可以点击左边的 ▶️ 打开围观，但不建议使用
    
    通过QuantumultX的url-scheme，也可以实现一键导入配置(`**但是既麻烦又低效，不大建议**`)：
    
    ### a. **官方说明：**
    
    - [https://github.com/crossutility/Quantumult-X/blob/master/url-scheme.md](https://github.com/crossutility/Quantumult-X/blob/master/url-scheme.md)
    
    ### b. **示范教学：**
    
    1. **按照下方json格式填写，其中：**
        - server_remote 填写节点订阅链接；
        - filter_remote 填写分流规则:
        - rewrite_remote 填入复写规则链接
    
    ```JSON
    {
        "server_remote": [
            "https://raw.githubusercontent.com/crossutility/Quantumult-X/master/server.txt, tag=Sample-01",
            "https://raw.githubusercontent.com/crossutility/Quantumult-X/master/server-complete.txt, tag=Sample-02"
        ],
        "filter_remote": [
            "https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Advertising.list, tag=去广告, enabled=true",
            "https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Apple.list, tag=Apple服务, enabled=true",
            "https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/China.list, tag=国内网站, enabled=true",
            "https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/DomesticMedia.list, tag=国内视频, enabled=true",
            "http://cloudcompute.lbyczf.com/x-rule-set?url=https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/Netflix.list, tag=📺Netflix, force-policy=📺 Netflix, enabled=true",
            "http://cloudcompute.lbyczf.com/x-rule-set?url=https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/YouTube.list, tag=🎬Youtube, force-policy=🎬 Youtube, enabled=true",
            "https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/ForeignMedia.list, tag=国外视频, enabled=true",
            "https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Global.list, tag=国外网站, enabled=true",
            "https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Hijacking.list, tag=运营商劫持, enabled=true"
        ],
        "rewrite_remote": [
            " http://cloudcompute.lbyczf.com/quanx-rewrite, tag=Lhie1复写"
        ]
    }
    ```
    
    2. **复制以上全部代码，进行url-encode**： [https://www.urlencoder.org/](https://www.urlencoder.org/)
    
    进入此网站，粘贴上述代码，点击 Encode，复制结果
    
    ![[Untitled 18.png]]
    
    **3. 将上述结果加在：**
    
    ```JSON
     quantumult-x:///update-configuration?remote-resource=上一步的结果
    ```
    
    复制总链接，丢入Safari即可：
    
    ```Shell
    quantumult-x:///update-configuration?remote-resource=%7B%0A%20%20%20%20%22server_remote%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fcrossutility%2FQuantumult-X%2Fmaster%2Fserver.txt%2C%20tag%3DSample-01%22%2C%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fcrossutility%2FQuantumult-X%2Fmaster%2Fserver-complete.txt%2C%20tag%3DSample-02%22%0A%20%20%20%20%5D%2C%0A%20%20%20%20%22filter_remote%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FQuantumult%2FX%2FFilter%2FAdvertising.list%2C%20tag%3D%E5%8E%BB%E5%B9%BF%E5%91%8A%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FQuantumult%2FX%2FFilter%2FApple.list%2C%20tag%3DApple%E6%9C%8D%E5%8A%A1%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FQuantumult%2FX%2FFilter%2FChina.list%2C%20tag%3D%E5%9B%BD%E5%86%85%E7%BD%91%E7%AB%99%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FQuantumult%2FX%2FFilter%2FDomesticMedia.list%2C%20tag%3D%E5%9B%BD%E5%86%85%E8%A7%86%E9%A2%91%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22http%3A%2F%2Fcloudcompute.lbyczf.com%2Fx-rule-set%3Furl%3Dhttps%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FSurge%2FRuleset%2FMedia%2FNetflix.list%2C%20tag%3D%F0%9F%93%BANetflix%2C%20force-policy%3D%F0%9F%93%BA%20Netflix%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22http%3A%2F%2Fcloudcompute.lbyczf.com%2Fx-rule-set%3Furl%3Dhttps%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FSurge%2FRuleset%2FMedia%2FYouTube.list%2C%20tag%3D%F0%9F%8E%ACYoutube%2C%20force-policy%3D%F0%9F%8E%AC%20Youtube%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FQuantumult%2FX%2FFilter%2FForeignMedia.list%2C%20tag%3D%E5%9B%BD%E5%A4%96%E8%A7%86%E9%A2%91%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FQuantumult%2FX%2FFilter%2FGlobal.list%2C%20tag%3D%E5%9B%BD%E5%A4%96%E7%BD%91%E7%AB%99%2C%20enabled%3Dtrue%22%2C%0A%20%20%20%20%20%20%20%20%22https%3A%2F%2Fraw.githubusercontent.com%2FConnersHua%2FProfiles%2Fmaster%2FQuantumult%2FX%2FFilter%2FHijacking.list%2C%20tag%3D%E8%BF%90%E8%90%A5%E5%95%86%E5%8A%AB%E6%8C%81%2C%20enabled%3Dtrue%22%0A%20%20%20%20%5D%2C%0A%20%20%20%20%22rewrite_remote%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%22%20http%3A%2F%2Fcloudcompute.lbyczf.com%2Fquanx-rewrite%2C%20tag%3DLhie1%E5%A4%8D%E5%86%99%22%0A%20%20%20%20%5D%0A%7D
    ```
    

---

---

# 6⃣️ JavaScript 脚本以及[task]使用

## 6.1 使用简要说明

> [!important]  
> JS 的引入，起初只是为了能更好的修改响应体从而去除某些顽固广告，但随着版本的不断更新迭代，现在Quantumult X 的js脚本功能已经五花八门，完美适合各类爱折腾的同学。在版本 1.0.12+ 后，作者重新开放了 远程脚本的一键更新 ，⚠️但需满足一个条件：购买时间>30天⚠️⚠️否则，你依旧可以使用远程 js 脚本，但只能一个个手动更新  

**JS 使用的 2⃣️ 个 要素：**

1. **JS 脚本文件本身**
    - 如果你是极端小白，那你只用知道，脚本文件本身，就是你在网上 `**找到/下载**` 到的那个，叫xxx.js 的文件(它可以是本地文件，也可以是别人放在GitHub的远程链接🔗️)
2. **Quantumult X 配置中的重写rewrite语句**
    
    - 有了JS文件之后，你当然还需要告诉 Quantumult X，你要如何使用这个xxx.js
        - 写法的通用表达 ： `**匹配网址 url 复写类型 脚本文件**`
    - 这个语句是一句 rewrite，可以放在本地配置(rewrite_local)，也可以放远程引用(rewrite_remote)
    
    ```JavaScript
    ; 匹配网址请求  url  复写类型  脚本文件
    http://example\.com/resource5/ url script-response-body  123.js
    ```
    
    - 解读上面的语句：当访问网址匹配 “[http://example](http://example/)\.com/resource5/” 时，将会执行 123.js 的脚本文件， 而 `**url script-response-body**`，则是 `**复写类型**`
    - 各类型的具体说明，参见作者: [https://github.com/crossutility/Quantumult-X](https://github.com/crossutility/Quantumult-X)

### A. JS 文件（远程-本机-iCloud）

首先，关于 js脚本文件 的位置说明:

> [!important]  
> 0⃣️. 请大佬们 千万别 直接把js脚本链接直接丢进rewrite引用，然后还跑来问“怎么报错？” 1️⃣. 同时，放对位置后，需要去 rewrite_local里添加引用  

1. 可以放 `github 后， 远程使用对应链接（raw 链接）`

2. 也可以放入本机文件夹中 /`On My iPhone/Quantumult X/Scripts` 目录下

3. 当然也可以放入`**iCloud Drive**`下的 `**Quantumult X/Scripts**` 目录 (但记得去quantumultx中开启开关，如`**右下图**`所示)

![[STIIITCH_2019_07_23_11_14_39.png]]

![[STIIITCH_2019_12_09_12_37_09.png]]

### B. 重写语句

示范 1：本地写法（`**文本编辑，[rewrite_local] 部分**`）:

```JavaScript
;远程 github js脚本
http://example\.com/resource5/ url script-response-body https://raw.githubusercontent.com/crossutility/Quantumult-X/master/sample-rewrite-with-script.js

;本地js文件
http://example\.com/resource5/ url script-response-body script_name.js
```

当然，你也可以将`**上述复写语句**`放在GitHub中，作为远程 rewrite ， 直接引用导入（但记得脚本路径跟文件本身，都要放置在本地）

示范2: 远程写法 （UI内重写部分直接引用，或文本编辑填入 `**[rewrite_remote]**` 部分）

譬如神机规则重写的订阅链接内，就包含部分js复写，可以直接引用导入使用：

> [!info]  
>  
> [https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/Block/Advertising.conf](https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/Block/Advertising.conf)  

## 6.2 JavaScript 去广告(rewrite)

Quantumult X 支持通过JS脚本修改 响应体 / 响应头/ 请求头 等等, 以满足更复杂的需求。

官方示范说明链接：

> [!info] crossutility/Quantumult-X  
> Samples of HTTP rewrite feature.  
> [https://github.com/crossutility/Quantumult-X/blob/master/rewrite.md](https://github.com/crossutility/Quantumult-X/blob/master/rewrite.md)  

`P.S.: 与 surge 的部分去广告脚本基本通用，只需按各自格式进行更改即可（不支持定时任务&脚本内发送请求）`

### A . JS脚本资源 (可供学习，但请勿滥用)

某些js脚本频道订阅

可关注几位大佬的脚本频道，频道中有可以通过rewrite 直接订阅 的js集合：

1⃣️ [https://t.me/meetashare](https://t.me/meetashare)

2⃣️ [https://t.me/NobyDa](https://t.me/NobyDa)

3⃣️ [https://github.com/yichahucha/surge/tree/master](https://github.com/yichahucha/surge/tree/master) 👍👍👍 （京东 / 淘宝 商品历史价格显示，Netflix 电影评分显示）

4⃣️[https://github.com/chavyleung/scripts](https://github.com/chavyleung/scripts) （`**签到狂魔**`大佬的地址, bilibili, 喜马拉雅，腾讯视频 爱奇艺 什么值得买 等）

**效果展示：**

![[Untitled 19.png]]

## 6.3 任务脚本使用（task scripts）

Quantumult X**`最新TF版本中 (170+)`**, 增加了期待已久的 `**任务脚本功能(task scripts)**`。可设置定时发送请求，比如“`**天气提醒、话费查询、甚至是签到**`”，进一步提高了Quantumult X的可玩性。

目前该功能模块被独立出来，且仅限本地使用 **`[task_local]`**

### A. 添加**方法**

1. **单条使用：**

```JavaScript
;配置文件中，自己添加下面的[task_local]模块，并填写任务，
;任务脚本 name.js 文件放于 本机 或者 iCloud 的 "Quantumult X/Scripts" 目录下
; * * * * * 为分开始的 cron语法，用法可随意 Google或见教程：Cron语法格式学习
;tag 参数指定 task 标签名
;img-url参数为 task 指定图标 icon
[task_local]
//脚本在本地时
* * * * * name.js, tag=京东签到, img-url=https://icon.expamle.png
//脚本在远程时
* * * * * https://example.name.js, tag=京东签到, img-url=https://icon.expamle.png

;如果是签到类task任务，一般还需要先获取对应的cookie；
;提供签到类的脚本处一般会有使用说明，请自行寻找
;一般在提供签到js的资源处，会有对应的说明，请参照具体情况使
```

![[IMG_7059.jpg]]

![[IMG_4598.jpg]]

  

  

**2. task gallery 订阅**

TF 版本 1.0.17 (`**build 433**`)后，Quantumult X 加入了 task-gallery，可以实现签到脚本订阅&管理。

- [官方示范格式](https://github.com/crossutility/Quantumult-X/blob/master/gallery.json) [JSON](https://github.com/crossutility/Quantumult-X/blob/master/gallery.json)；
- [可用 API 转换，示范](https://t.me/QuanX_API/63)；
- 已有大佬们的仓库(可直接引用)：
    
    > [!info]  
    >  
    > [https://raw.githubusercontent.com/HotKids/Rules/master/Quantumult/X/TaskGallery.json](https://raw.githubusercontent.com/HotKids/Rules/master/Quantumult/X/TaskGallery.json)  
    
    > [!info]  
    >  
    > [https://gist.githubusercontent.com/Peng-YM/cc2cd6205b305d36544a44ec77129832/raw/gallery.json](https://gist.githubusercontent.com/Peng-YM/cc2cd6205b305d36544a44ec77129832/raw/gallery.json)  
    

![[Untitled 20.png]]

  

### B. 效果展示

![[STIIITCH_2019_12_19_13_17_03.png]]

![[IMG_5016.png]]

### C. 资源分享

1. 自己按照作者示范写

> [!info] crossutility/Quantumult-X  
> You can't perform that action at this time.  
> [https://github.com/crossutility/Quantumult-X/blob/master/sample-task.js](https://github.com/crossutility/Quantumult-X/blob/master/sample-task.js)  

2. 网友大佬们的分享

> [!info] yichahucha/surge  
> Remove Weibo ads, promotion and recommend [Script] http-response .  
> [https://github.com/yichahucha/surge/tree/master](https://github.com/yichahucha/surge/tree/master)  

[https://github.com/NavePnow/Profiles#weatherjs](https://github.com/NavePnow/Profiles#weatherjs)

> [!info] ‌Darren's Channel  
> Utilities \#Reference \#Lifestyle \#Weather 更新: 捷径适配quanx(tf169支持定时脚本功能) 修护: 浮点数相乘导致数据位数错误的问题 每日天气提醒脚本  
> [https://t.me/Leped_Channel/542](https://t.me/Leped_Channel/542)  

> [!info] chavyleung/scripts  
> You can't perform that action at this time.  
> [https://github.com/chavyleung/scripts](https://github.com/chavyleung/scripts)  

> [!info] sazs34/TaskConfig  
> QuantumultX专用的任务执行，作者没有Surge因此无法进行适配，请谅解.  
> [https://github.com/sazs34/TaskConfig](https://github.com/sazs34/TaskConfig)  

### D. 调试方法

1.0.16版本后，task手动运行(`**右滑**`)有两种模式

- 后台运行，不会即时跳出日志页面；
- 日志模式，可以即时看到运行状态（运行结束前不能关闭退出）

![[Untitled 21.png]]

  

## 6.3 JS 自定义查询节点信息

这部分与上面的JS其实没太多关系。仅用于`**获取节点信息**`并 展示在Quantumult X节点页面

官方说明如下：

```Shell
- 增加自定义主页显示节点落地信息的数据获取方式（geo_location_checker）。
- 增加长按节点获取节点落地信息的功能（需有配置 geo_location_checker）。
- 范例中脚本各返回值为必须，否则显示查询失败。如不在意某个值，脚本返回任意固定值即可。
- 为提高查询效率节点信息查询接口的请求仅支持 http，范例如下：
[general]
geo_location_checker=http://extreme-ip-lookup.com/json/, https://raw.githubusercontent.com/crossutility/Quantumult-X/master/sample-location-with-script.js
```

下图中，前两图 分别使用了 `[api.ipstack.com](http://api.ipstack.com)` 跟 `[ifconfig.co/json](http://ifconfig.co/json)` 的查询接口返回数据，然后脚本自定义返回的参数进行显示（如 ip，city，country 等）：

第三图为 长按节点，显示详细信息

![[STIIITCH_2019_07_22_05_43_12.png]]

具体代码如下，根据喜好自行修改查询的 api 以及所需参数(第 3️⃣ 4️⃣个为返回 `中文` 的api)

如`上图 4` 所示，代码放到 `文本配置`，`[general]` 下，可通过`;注释`来选择生效的 api 代码：

```Shell
;加';'来注释掉对应行, 如下，仅第 5⃣️ 行生效
;geo_location_checker=http://ifconfig.co/json,https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IPConfig.js
;geo_location_checker= http://extreme-ip-lookup.com/json/ ,https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IPCheck.js
;geo_location_checker=http://ip-api.com/json/?lang=zh-CN, https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IP_API.js
;geo_location_checker= http://api.ipstack.com/check?access_key=1c24147fb534e1a71cb35ff84de2d153&language=zh&output=json , https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IPInfo.js
geo_location_checker= http://api.live.bilibili.com/ip_service/v1/ip_service/get_ip_addr?, https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IP_bili_cn.js
```

[[在本地运行 Code Autopilot – IoT 技术专栏]]