  

> [!important]  
> Surgio，一款高度自定义各类App策略组的托管工具，例如比较热门的Surge、QuantumultX、Clash等，您甚至可以使Surge自动同步远程Rewrite、Hostname部分。  

- 项目地址https://github.com/geekdada/surgio，首先感谢作者geekdada。
- 本教程由sjh完成，观看教程需具备一定的汉语能力，您只需要一字不差照搬，无需VPS即可完成部署，如有疑问可留言至Telegram频道[https://t.me/cloudtest](https://t.me/cloudtest)

---

- ==演示地址：==
    
    ==[https://demo-beta.now.sh](https://demo-beta.now.sh/)==
    
    accessToken：==YOUR_PASSWORD==
    

![[2020-03-092.09.13.png]]

👆最终效果展示

废话不多说，下面进入正题，本教程使用macOS10.15.13系统演示。

---

- ==1、准备本地环境==
    
    - 1⃣️ 安装node.js，选择长期支持版LTS
        
        下载地址：[https://nodejs.org/zh-cn/download/](https://nodejs.org/zh-cn/download/)
        
        ![[2020-03-088.25.57.png]]
        
    - 2⃣️ 准备一个现代化的编辑器，例如VSCode
        
        创建一个文件夹备用，名字请便，此处为命名为demo
        
    
    ![[2020-03-088.41.19.png]]
    
    ![[2020-03-088.51.30.png]]
    

---

- ==2、安装surgio本体==
    
    - 1⃣️ 在上一步创建的文件夹demo中启动终端，使用命令安装surgio，二选一
        
        ```JavaScript
        # 安装
        npm init surgio-store my-rule-store
        
        # 使用国内镜像安装
        npm init surgio-store my-rule-store --use-cnpm
        ```
        
        此处提示是否配置将配置文件上传至阿里云 OSS，选择否
        
        ![[2020-03-088.59.54.png]]
        
    
    至此Surgio本地版已经完成
    

---

- ==3 、测试Surgio在本地生成Surge/QuantumultX/Clash完整配置（非必要，可略过）==
    
    - 1⃣️ 在上一步创建的**my-rule-store**目录输入以下命令，即可生成完整策略组配置。
        
        ```JavaScript
        # 生成规则(Surge/QuantumultX/Clash)
        
        npx surgio generate
        ```
        
        ![[2020-03-0912.02.46.png]]
        
    - 2⃣️ 已生成完整策略组配置，可在**my-rule-store/dist/**目录下查看
        
        ![[2020-03-0912.09.59.png]]
        
    
    测试完成，选取对应App配置后可见熟悉的配置文件。
    

---

- ==4、安装策略组托管API组件==
    
    - 1⃣️ 修改/my-rule-store/目录下的surgio.conf.js文件，复制下面这段到136行，添加accessToken，修改引号‘’里面的内，俗称改密码
        
        ```JavaScript
        // 接口鉴权
        gateway: {
            auth: true,
            accessToken: 'YOUR_PASSWORD',
          },
        ```
        
        ![[2020-03-0912.51.28.png]]
        
          
        
    - 2⃣️ 修改/my-rule-store/目录下的**package.json**文件，第10行添加以下内容，别忘了加上“,”英文逗号
        
        ```JSON
        ,
          "engines": {
            "node": "10.x"
          }
        ```
        
        ![[2020-03-091.42.22.png]]
        
    - 3⃣️ /my-rule-store/目录下新建**now.json**文件，输入以下内容
        
        ```JSON
        {
            "version": 2,
            "public": false,
            "builds": [
              { 
                "src": "/gateway.js",
                "use": "@now/node",
                "config": {
                  "includeFiles": [
                    "provider/**",
                    "template/**",
                    "*.js",
                    "*.json"
                  ]
                }
              }
            ],
            "routes": [
              {
                "src": "/(.*)",
                "dest": "/gateway.js"
              }
            ]
          }
        ```
        
        ![[2020-03-091.43.03.png]]
        
          
        
    - 4⃣️ /my-rule-store/目录下新建**gateway.js**文件，输入以下内容
        
        ```JavaScript
        'use strict';
        
        const gateway = require('@surgio/gateway');
        
        module.exports = gateway.createHttpServer();
        ```
        
        ![[2020-03-091.47.34.png]]
        
    - 5⃣️ /my-rule-store/目录下运行命令
        
        ```JavaScript
        npm i @surgio/gateway --save
        ```
        
        ![[2020-03-092.00.14.png]]
        
    
    至此API组件部署完成，接下来将本地仓库推送到GitHub并且关联now.sh网关即可
    
- ==5、将Surgio本体推送至GitHub仓库==
    
    - 1⃣️ 新建一个空仓库
        
        选择私有，注意不要勾选初始化仓库
        
        ![[2020-03-0912.44.50.png]]
        
        ⚠️ 当然你也可以选择公仓，机场主不封你号问题就不大。
        
        复制新建仓库的这条命令备用
        
        ![[2020-03-0910.42.34.png]]
        
    - 2⃣️ 本地项目Surgio推送GitHub仓库
        
        /my-rule-store/目录下新建名为.gitignore的文件，输入内容
        
        ```JavaScript
        .env
        node_modules
        dist
        .DS_Store
        ```
        
        ![[2020-03-0910.28.41.png]]
        
        以上步骤完成后保存文件，接下来连接远程仓库，依次在/my-rule-store/目录下输入命令，注意，你不要把汉字也输进去，过程会提示输入你的GitHub账户邮箱及密码
        
        ```JavaScript
        # 初始化仓库
        git init
        
        # 连接GitHub仓库，此命令每个仓库不相同，你需要在你的仓库里找到，参考上一步
        git remote add origin https://github.com/oss-net/demo.git
        ```
        
        ![[2020-03-0910.35.40.png]]
        
        远程仓库连接成功
        
        本地项目推送GitHub仓库
        
        点击带数字的蓝色圈，再点击右边的+，暂存更改
        
        ![[2020-03-0910.46.47.png]]
        
        暂存更改完成
        
        这里随便输几个字，点击右上角的✓，提交
        
        ![[2020-03-0910.53.41.png]]
        
        提交完成
        
        接下来推送到仓库，点击上图✓旁边的...，选择推送，过程会提示输入你的GitHub账户邮箱及密码，没有上游分支，确定发布
        
        ![[2020-03-0910.59.58.png]]
        
        推送完成
        
        ![[2020-03-0911.04.15.png]]
        
        查看仓库
        
    
    至此你的Surgio已推送到GitHub仓库，接下来需要关联now.sh网关
    

---

- ==6、now.sh关联GitHub仓库==
    - 1⃣️ 登陆Zeit
        
        登陆地址：[https://zeit.co/](https://zeit.co/)
        
        使用你的GitHub登陆即可
        
        ![[2020-03-091.15.45.png]]
        
        步骤过于简单，这里不演示
        
    - 2⃣️ 关联Surgio项目
        
        点击Import Project
        
        ![[2020-03-091.19.12.png]]
        
        选择From Git Repository，点击Continue
        
        ![[2020-03-091.24.24.png]]
        
        点击Import Project From GitHub，从你的GitHub仓库选择关联
        
        ![[2020-03-091.27.00.png]]
        
        名字、路径默认即可，无需修改
        
        ![[2020-03-091.29.13.png]]
        
        ![[2020-03-091.30.12.png]]
        
        项目关联成功
        
          
        
    - 3⃣️ 保存API地址
        
        这几条连接即为你的Surgio访问连接，保存备用
        
        ![[2020-03-091.32.33.png]]
        
        复制到浏览器打开，并且输入token，即可成功访问
        
        ![[2020-03-091.38.53.png]]
        
        ![[2020-03-091.40.04.png]]
        
        至此你的Surgio已经全部完成
        
          
        
    - 4⃣️ 同步托管地址
        
        修改/my-rule-store/surgio.conf.js，第123行
        
        ```JSON
        urlBase: 'https://example.com/',
        # 替换为你的API地址，必须以/结尾
        
        urlBase: 'https://demo-beta.now.sh/',
        ```
        
        ![[2020-03-091.50.15.png]]
        
        修改完成后提交推送，这里不再复述
        

---

- ==7、使用Surgio托管API==
    - 1⃣️ 输入Surgio面板地址
        
        https://demo-beta.now.sh/
        
        ![[2020-03-091.59.28.png]]