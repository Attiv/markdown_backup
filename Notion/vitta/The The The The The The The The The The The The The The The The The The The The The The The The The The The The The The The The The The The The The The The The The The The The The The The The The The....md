在 `podfile`里加入

```Plain
# Enable DEBUG flag in Swift for SwiftTweaks
post_install do |installer|
    installer.pods_project.targets.each do |target|
        if target.name == 'SwiftTweaks'
            target.build_configurations.each do |config|
                if config.name == 'Debug'
                    config.build_settings['OTHER_SWIFT_FLAGS'] = '-DDEBUG'
                end
            end
        end
    end
end
```

比如：

```Plain
platform :ios, '10.0'
use_frameworks!
target 'OnTime Talent' do
    pod 'GPUImage'
    pod 'Colours'
    pod 'CenterTextLayer'
    pod 'FirebaseMessaging', '~> 2.0.0'
end

# Enable DEBUG flag in Swift for SwiftTweaks
post_install do |installer|
    installer.pods_project.targets.each do |target|
        if target.name == 'SwiftTweaks'
            target.build_configurations.each do |config|
                if config.name == 'Debug'
                    config.build_settings['OTHER_SWIFT_FLAGS'] = '-DDEBUG'
                end
            end
        end
    end
end
```

%E5%9C%A8%20%60podfile%60%E9%87%8C%E5%8A%A0%E5%85%A5%0A%60%60%60%0A%23%20Enable%20DEBUG%20flag%20in%20Swift%20for%20SwiftTweaks%0Apost_install%20do%20%7Cinstaller%7C%0A%20%20%20%20installer.pods_project.targets.each%20do%20%7Ctarget%7C%0A%20%20%20%20%20%20%20%20if%20target.name%20%3D%3D%20'SwiftTweaks'%0A%20%20%20%20%20%20%20%20%20%20%20%20target.build_configurations.each%20do%20%7Cconfig%7C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20if%20config.name%20%3D%3D%20'Debug'%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20config.build_settings%5B'OTHER_SWIFT_FLAGS'%5D%20%3D%20'-DDEBUG'%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20end%0A%20%20%20%20%20%20%20%20%20%20%20%20end%0A%20%20%20%20%20%20%20%20end%0A%20%20%20%20end%0Aend%0A%60%60%60%0A%0A%E6%AF%94%E5%A6%82%EF%BC%9A%0A%60%60%60%0Aplatform%20%3Aios%2C%20'10.0'%0Ause_frameworks!%0Atarget%20'OnTime%20Talent'%20do%0A%09pod%20'GPUImage'%0A%09pod%20'Colours'%0A%09pod%20'CenterTextLayer'%0A%09pod%20'FirebaseMessaging'%2C%20'~%3E%202.0.0'%0Aend%0A%0A%23%20Enable%20DEBUG%20flag%20in%20Swift%20for%20SwiftTweaks%0Apost_install%20do%20%7Cinstaller%7C%0A%20%20%20%20installer.pods_project.targets.each%20do%20%7Ctarget%7C%0A%20%20%20%20%20%20%20%20if%20target.name%20%3D%3D%20'SwiftTweaks'%0A%20%20%20%20%20%20%20%20%20%20%20%20target.build_configurations.each%20do%20%7Cconfig%7C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20if%20config.name%20%3D%3D%20'Debug'%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20config.build_settings%5B'OTHER_SWIFT_FLAGS'%5D%20%3D%20'-DDEBUG'%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20end%0A%20%20%20%20%20%20%20%20%20%20%20%20end%0A%20%20%20%20%20%20%20%20end%0A%20%20%20%20end%0Aend%0A%0A%60%60%60