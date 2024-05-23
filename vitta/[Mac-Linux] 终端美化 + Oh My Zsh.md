# [Mac/Linux] 终端美化 + Oh My Zsh
整容前：![整容前](https://raw.githubusercontent.com/Attiv/tubed/master/CleanShot%202021-11-26%20at%2020.21.10%402x.png)

整容后：![](https://raw.githubusercontent.com/Attiv/tubed/master/CleanShot%202021-11-26%20at%2023.38.15%402x.png)
> 本篇以 Linux 服务器为例

1. 安装 [Oh My Zsh](https://ohmyz.sh)
    1) 执行: `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
    2) 安装完之后是这样![安装后](https://raw.githubusercontent.com/Attiv/tubed/master/CleanShot%202021-11-26%20at%2020.22.19%402x.png)
    
> 安装插件的方式有很多，这里使用了Zplug
2. 安装[ZPlug](https://github.com/zplug/zplug)
    
    1) 执行 `curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh`
  
    2) 安装完之后编辑 `.zshrc` 文件. `vi ~/.zshrc`
     首先导入`zplug`: `source ~/.zplug/init.zsh`
     > 主题有很多，这里我们使用[P10K](https://github.com/romkatv/powerlevel10k#zplugin)
     > `p10k` 要求 `zsh` 最低版本 5.1, 具体办法自己搜,**需要注意卸载老版本的zsh之后安装新的之前可能会导致密码登录服务器报错**
     
     在`zshrc`文件里加入:
     ```
     zplug romkatv/powerlevel10k, as:theme, depth:1
     ```
     然后 `source .zshrc`，会提示安装插件，如果没有可以手动执行`zplug install`
     然后根据终端提示配置p10k.
     ![看这](https://raw.githubusercontent.com/Attiv/tubed/master/CleanShot%202021-11-26%20at%2023.32.58%402x.png)

    配置完就可以了
      
  3. Mac 端安装方法类似，更简单, Mac 推荐使用 [Iterm2](https://iterm2.com/)代替终端
   令分享一些插件：
   ```
   zplug 'zplug/zplug', hook-build:'zplug --self-manage'
# git git命令alias, 使用 cat ~/.oh-my-zsh/plugins/git/git.plugin.zsh 查看所有
zplug "plugins/git",   from:oh-my-zsh
zplug "plugins/osx",   from:oh-my-zsh
# vscode 使用vscode 打开文件
zplug "plugins/vscode",   from:oh-my-zsh
# Z 类似 autojump,快速跳转文件夹
zplug "plugins/z",   from:oh-my-zsh 
# d 跳转当前终端曾经cd 过的目录
zplug "plugins/d",   from:oh-my-zsh
# extract 解压
zplug "plugins/extract",   from:oh-my-zsh
# zplug "plugins/git-open",   from:oh-my-zsh
# git-open 在浏览器里打开当前git仓库
zplug "paulirish/git-open", as:plugin
# sudo 按两下ESC，就会在命令行头部加上sudo
zplug "plugins/sudo",   from:oh-my-zsh
# cp 复制显示进度条
zplug "plugins/cp",   from:oh-my-zsh
# web-search 添加命令以直接从 CLI 运行 bing、google、yahoo 和 duckduckgo 搜索.
zplug "plugins/web-search",   from:oh-my-zsh
# rand-quote 没啥用,随机显示名言
zplug "plugins/rand-quote", from:oh-my-zsh
# zplug "plugins/history-substring-search",  from:oh-my-zsh
# command-not-found 当你输入一条不存在的命令时，会自动查询这条命令可以如何获得。
zplug "plugins/command-not-found",   from:oh-my-zsh
# zsh-syntax-highlighting 命令高亮 红色代表没有此命令 绿色可能执行此命令
zplug "zsh-users/zsh-syntax-highlighting"
# autosuggestions 补全命令历史
zplug "zsh-users/zsh-autosuggestions"
# gitignore 提供一条 gi 命令，用来查询 gitignore 模板。比如你新建了一个 python 项目，就可以用：gi python > .gitignore 
zplug "voronkovich/gitignore.plugin.zsh"
# zsh-history-substring-search 查找匹配前缀的历史输入,使用方式搜一下吧
zplug "zsh-users/zsh-history-substring-search"

```
   

