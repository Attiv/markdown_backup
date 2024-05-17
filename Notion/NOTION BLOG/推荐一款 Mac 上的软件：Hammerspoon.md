---
type: Post
status: Published
date: 2021-07-02
tags:
  - 工具
category: 工具分享
---
Hammerspoon 是一款以自动化闻名的开源、免费的软件，将系统底层的一些接口封装成简单易用的 [Lua Api](https://www.hammerspoon.org/docs/index.html)，可以自己实现一些不太离谱的功能，github 上也有许多脚本。

比较常用的功能有这些:

- 显示粘贴板记录
- 窗口大小管理（快捷键）
- 音量调节（快捷键）
- 自动切换输入法
- 鼠标连点
- 快捷键唤醒app
- 等等

---

下面具体介绍一个比较常用的功能：**自动切换输入法**  
自动切换输入法，顾名思义，在切换到不同的 app 时自动切换不同的输入法，省去按下切换输入法或者大小写。  

使用场景：

- 在 QQ，微信 聊天时需要使用中文输入法
- 在 IDE，Slack，Terminal 等需要使用英文输入

安装教程：

1. 官网下载
2. 打开
3. 扔到 Application 里
4. 在 `~/.hammerspoon/init.lua` 里写代码或者点击菜单栏里的锤子，点 `open config`

Demo 如下：

> 可以单独创建一个lua 文件比如创建个文件夹叫 ime, 在ime文件夹下创建一个 ime.lua文件，在init.lua里引入: require "ime.ime"

```Plain
-- 中文输入法
local function Chinese()
    -- rime输入法
    hs.keycodes.currentSourceID("im.rime.inputmethod.Squirrel.Rime")
    -- 系统默认中文双拼输入法
    -- hs.keycodes.currentSourceID("com.apple.inputmethod.SCIM.Shuangpin")
end

-- 英文输入法
local function English()
    -- 系统默认英文输入法
    hs.keycodes.currentSourceID("com.apple.keylayout.ABC")
end

-- 哈利路亚英文输入法
local function Hlly()
    hs.keycodes.currentSourceID("github.dongyuwei.inputmethod.hallelujahInputMethod")
end

-- app to expected ime config
local app2Ime = {
    {'/Applications/Xcode.app', 'English'},
    -- {'/Applications/Google Chrome.app', 'Chinese'},
    -- {'/System/Library/CoreServices/Finder.app', 'English'},
    {'/Applications/DingTalk.app', 'Chinese'},
    -- {'/Applications/Kindle.app', 'English'},
    {'/Applications/NeteaseMusic.app', 'Chinese'},
    {'/Applications/WeChat.app', 'Chinese'},
    {'/Applications/System Preferences.app', 'English'},
    {'/Applications/Dash.app', 'English'},
    -- {'/Applications/MindNode.app', 'Chinese'},
    -- {'/Applications/Preview.app', 'Chinese'},
    {'/Applications/Fork.app', 'English'},
    {'/Applications/wechatwebdevtools.app', 'English'},
    {'/Applications/Sketch.app', 'English'},
    {'/Applications/Visual Studio Code.app', 'English'},
    {'/Applications/TablePlus.app', 'English'},
    {'/Applications/GitUp.app', 'English'},
    -- IDE 是使用 JetBrains Toolbox 安装的，app 路径不在 Application/ 下，有些自动切换输入法的工具会失效，所以使用全路径
    {'/Users/wanglikun/Library/Application Support/JetBrains/Toolbox/apps/AppCode/ch-0/212.5284.45/AppCode.app', 'English'},
    {'/Users/wanglikun/Library/Application Support/JetBrains/Toolbox/apps/PhpStorm/ch-0/212.5457.49/PhpStorm.app', 'English'},
    {'/Users/wanglikun/Library/Application Support/JetBrains/Toolbox/apps/WebStorm/ch-0/211.6693.108/WebStorm.app', 'English'},
    {'/Applications/Xcode12.app', 'English'},
    {'/Users/wanglikun/Library/Application Support/JetBrains/Toolbox/apps/AndroidStudio/ch-0/203.7678000/Android Studio.app', 'English'},
    {'/Applications/eDEX-UI.app', 'English'},
    {'/Applications/QQ.app', 'Chinese'},
    {'/Applications/Fork.app', 'English'},
    {'/Applications/iTerm.app', 'English'},
    {'/Applications/Unity/Hub/Editor/2019.4.14f1c1/Unity.app', 'English'},
    {'/Applications/Visual Studio.app', 'English'},
    {'/Applications/Sublime Text.app', 'English'},
}

-- 切换输入法
function updateFocusAppInputMethod()
    local focusAppPath = hs.window.frontmostWindow():application():path()
    for index, app in pairs(app2Ime) do
        local appPath = app[1]
        local expectedIme = app[2]

        if focusAppPath == appPath then
            hs.alert.closeAll()
            if expectedIme == 'English' then
                English()
                -- hs.alert.show('English', {}, 0.5)
            else
                Chinese()
                -- hs.alert.show('中文', {}, 0.5)
            end
            break
        end
    end
end

-- 杀掉哈利路亚输入法进程，因为使用哈利路亚输入法时切换桌面的时候会有一个黑色弹窗显示1秒才消失，官方回复是系统bug，杀掉进程就不会显示了
-- 此处有bug，杀掉进程有延时，偶尔杀掉还显示黑色弹窗
function killHLLL()
    local hlll = hs.application.get('hallelujah')
    if hlll ~= nil then
        hs.application.get('hallelujah'):kill9()
    end
end

-- helper hotkey to figure out the app path and name of current focused window
-- 绑定快捷键，获取当前app的路径和输入Source ID，并自动添加到粘贴板
hs.hotkey.bind({'ctrl', 'option'}, ".", function()
    hs.alert.show("App path:        "
    ..hs.window.focusedWindow():application():path()
    .."\\n"
    .."App name:      "
    ..hs.window.focusedWindow():application():name()
    .."\\n"
    .."IM source id:  "
    ..hs.keycodes.currentSourceID())
    hs.pasteboard.setContents('{\\'' .. hs.window.focusedWindow():application():path() .. '\\', \\'\\'},')
    -- hs.pasteboard.setContents(hs.keycodes.currentSourceID())
end)

-- 绑定快捷键，切换当前输入法为哈利路亚输入法(这里是想要手动切换输入法的时候用的)
hs.hotkey.bind({'cmd', 'shift'}, "0", function()
    Hlly()
end)

-- 绑定快捷键，切换当前输入法为英文输入法(这里是想要手动切换输入法的时候用的)
hs.hotkey.bind({'cmd', 'shift'}, "9", function()
    English()
end)

-- 绑定快捷键，切换当前输入法为中文输入法(这里是想要手动切换输入法的时候用的)
hs.hotkey.bind({'cmd', 'shift'}, "8", function()
    Chinese()
end)

-- 绑定快捷键，杀掉哈利路亚输入法进程
hs.hotkey.bind({'cmd', 'shift'}, "7", function()
    killHLLL()
end)

-- Handle cursor focus and application's screen manage.
function applicationWatcher(appName, eventType, appObject)
    if (eventType == hs.application.watcher.activated) then
        updateFocusAppInputMethod()
    end
end

appWatcher = hs.application.watcher.new(applicationWatcher)
appWatcher:start()


```

写完代码之后点击菜单栏里的锤子，点击 `reload config` 如果代码不报错就可以生效。

可以在锤子里点击 `console`, 在里面测试代码

Hammerspoon 提供了很多的 api，可以自己实现特别多的功能，希望大家多多分享.

> 彩蛋：一个英文输入法哈利路亚输入法

[![](https://raw.githubusercontent.com/dongyuwei/hallelujahIM/master/snapshots/suggestions2.png)](https://raw.githubusercontent.com/dongyuwei/hallelujahIM/master/snapshots/suggestions2.png)