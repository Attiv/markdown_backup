错误: The iOS deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to  
8.0, but the range of supported deployment target versions is 9.0  

PodFile 里加上

```C#
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|
            config.build_settings.delete 'IPHONEOS_DEPLOYMENT_TARGET'
        end
    end
end
```