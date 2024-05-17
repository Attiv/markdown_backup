  

一个页面有多个TableView 或 CollectionView 时由于自适应高度导致的 contentSize 不正确问题

UITableViewCell 设置 Selected 样式不生效：

UICollectionViewCell 自适应布局不生效：

iOS16 之后 Safari 调试WebView:

Chrome 调试 iOS模拟器

WebView 加载的网页/字符串里有图片导致高度问题

链式响应推送通知

WKWebView loadHtmlString 计算高度不正确

WKWebView 加载内容显示不全的问题

ZFPlayer 开启画中画

Framework ‘xxx’ not found

# 一个页面有多个TableView 或 CollectionView 时由于自适应高度导致的 contentSize 不正确问题

  
1. 先给TableView 一个很高的高度:  
`make.height.equalTo(10000)`

2. 在主线程里更新：

```JavaScript
DispatchQueue.main.async { // 这个不是必须的，当前在主线程就不用这句了
      self.guideTableView.snp.updateConstraints { make in
          make.height.equalTo(self.guideTableView.contentSize.height)
      }
  }
```

# UITableViewCell 设置 Selected 样式不生效：

  

1. 添加一个 `var selectedIndex: Int = -1`
2. 在 `cellForRowAt` 里加上： `cell.isSelected = selectedIndex == indexPath.row`
3. 在 `didSelectRowAt` 里：
    
    ```JavaScript
            cell.isSelected = true
            selectedIndex = indexPath.row
            tableView.reloadData()
    ```
    

# UICollectionViewCell 自适应布局不生效：

可以把 imageView.contentMode 改为scaleToFill

  

# iOS16 之后 Safari 调试WebView:

```Swift
// 从 iOS16.4 之后，如果想要通过 Web Inspector 查看，需要设置如下代码
if \#available(iOS 16.4, *) {
    webView.isInspectable = true
} else {
    // Fallback on earlier versions
}
```

  

# Chrome 调试 iOS模拟器

- `brew install ios-webkit-debug-proxy`
- `brew install libplist libusbmuxd usbmuxd libimobiledevice`
- `ios_webkit_debug_proxy -f chrome-devtools://devtools/bundled/inspector.html`
- chrome 中打开终端显示的端口，比如9222: `localhost:9222`

  

# WebView 加载的网页/字符串里有图片导致高度问题

不要用js 获取高度，用KVC:

1. 监听 `ScrollView` 
    
    ```Swift
    fileprivate lazy var webView: WKWebView = {
            let config = WKWebViewConfiguration()
            let web    = WKWebView(frame: CGRect(x: 0, y: 0, width: contentView.bounds.width, height: 100), configuration: config)
            web.navigationDelegate = self
            web.scrollView.isScrollEnabled = false
            web.translatesAutoresizingMaskIntoConstraints = false
            // 添加观察者监听 scrollView.contentSize 属性
            web.addObserver(self, forKeyPath: "scrollView.contentSize", options: .new, context: nil)
            return web
    }()
    
    /// 监听 scrollView.contentSize 属性
    override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {
            if keyPath == "scrollView.contentSize", let newSize = change?[.newKey] as? CGSize 			{
                print("new size: \(newSize)")
                self.heightAction?(newSize.height)
            }
    }
    
    deinit {
            webView.stopLoading()
            webView.removeObserver(self, forKeyPath: "scrollView.contentSize")
        }
    ```
    
    1. 监听 `loading` 状态 (比 ScrollView 调用次数少):  
          
        
    
    ```Swift
    fileprivate lazy var webView: WKWebView = {
            let config = WKWebViewConfiguration()
            let web    = WKWebView(frame: CGRect(x: 0, y: 0, width: contentView.bounds.width, height: 100), configuration: config)
            web.navigationDelegate = self
            web.scrollView.isScrollEnabled = false
            web.translatesAutoresizingMaskIntoConstraints = false
            // 监听 webView 加载的动作
            web.addObserver(self, forKeyPath: "loading", options: .new, context: nil)
            return web
        }()
        
        /// 监听 scrollView.contentSize & loading
    override func observeValue(forKeyPath keyPath: String?, 
    						   of object: Any?, 
    						   change: [NSKeyValueChangeKey : Any]?, 
    						   context: UnsafeMutableRawPointer?) {
    						   
            if keyPath == "loading"{
                webView.evaluateJavaScript("document.body.scrollHeight") 
                { (heightValue, error) in
                    guard let height = heightValue as? CGFloat else { return }
                    print("Web loading Height: \(height)")
                    self.heightAction?(height)
                }
            }
        }
        
        deinit {
            webView.stopLoading()
            webView.removeObserver(self, forKeyPath: "loading")
        }
    ```
    

# 链式响应推送通知

```Swift
//
//  NotificationObserver.swift
//  Ysp
//
//  Created by 王立坤 on 2023/11/30.
//

import Foundation
class NotificationObserver {
    private var observers: [NSObjectProtocol] = []

    deinit {
        removeAllObservers()
    }

    func addObserver(forName name: Notification.Name, using block: @escaping (Notification) -> Void) -> NotificationObserver {
        let observer = NotificationCenter.default.addObserver(forName: name, object: nil, queue: nil) { [weak self] notification in
            block(notification)
        }
        observers.append(observer)
        return self
    }

    func removeAllObservers() {
        for observer in observers {
            NotificationCenter.default.removeObserver(observer)
        }
        observers.removeAll()
    }
}


// 调用:
lazy var observer: NotificationObserver = .init()
observer.addObserver(forName: Name) { notification in
	// your handle
}
```

切记生命周期和重复调用问题， 有的没有触发 deinit 会导致多次响应

  

# WKWebView loadHtmlString 计算高度不正确

```Swift
let metaTag = "<meta name='viewport' content='width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0;'>"
        let htmlStringWithMeta = "\(metaTag)\(yourHtmlString)"

        contentText.loadHTMLString(htmlStringWithMeta, baseURL: nil)
```

  

# WKWebView 加载内容显示不全的问题

如果 `webView` 是放在 `cell` 里的话会出现加载显示不完全的问题，此时可以在 `tableView` 或者上级的滚动方法里加上:

```Swift
func scrollViewDidScroll(_ scrollView: UIScrollView) {
	webView.setNeedsLayout()
}
```

  

# ZFPlayer 开启画中画

- 添加后台设置

![[/Untitled 32.png|Untitled 32.png]]

- 添加代码

```Swift

// 在需要的页面里
import AVKit
var pipVC: AVPictureInPictureController?
lazy var playerManager: ZFAVPlayerManager = {
        let playerManager = ZFAVPlayerManager()
        playerManager.shouldAutoPlay = true
        return playerManager
}()
lazy var player: ZFPlayerController = {
        let player = ZFPlayerController(playerManager: playerManager, containerView: headerVideo.imageView)
        player.stopWhileNotVisible = true
        return player
}()
// 调用前 player 不能是空
func pipButtonClicked() {
        if AVPictureInPictureController.isPictureInPictureSupported() {
            do {
                try AVAudioSession.sharedInstance().setActive(true)
                let manager = player.currentPlayerManager  as! ZFAVPlayerManager
                pipVC = AVPictureInPictureController(playerLayer: manager.avPlayerLayer)
                if \#available(iOS 14.2, *) {
                    pipVC?.canStartPictureInPictureAutomaticallyFromInline = true
                } else {
                    // Fallback on earlier versions
                }
                VTUtil.delayExecution(seconds: 0.3) {
                    self.pipVC?.startPictureInPicture()
                }
            } catch {
                DDLog("AVAudioSession发生错误")
            }
         
        } else {
            DDLog("不支持画中画")
        }
        
    }


// appdelegate
import AVFoundation

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
		do {
                  // 设置AVAudioSession.Category.playback后，在静音模式下，或者APP进入后台，或者锁定屏幕后还可以继续播放。
                  try AVAudioSession.sharedInstance().setCategory(AVAudioSession.Category.playback, mode: AVAudioSession.Mode.moviePlayback)
            } catch {
                  print(error)
            }
	return true
}
```

  

# Framework ‘xxx’ not found

`Project-build setting-Other Linker Flags` 里删掉，保留 `$(inherited)` 就行，如果需要可以加上 `-ObjC`