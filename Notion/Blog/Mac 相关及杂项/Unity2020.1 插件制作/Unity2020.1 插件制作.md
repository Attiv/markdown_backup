- [修改 unity设置](https://www.codenong.com/cs106683617/)
    1. 文件→生成配置→Android→导出项目
        
        ![[/Untitled 30.png|Untitled 30.png]]
        
    2. 基于 1 的页面，点击左下角「玩家设置」→其他设置→配置→脚本后端→IL2CPP，目标架构→ARMv7, ARM64
        
          
        
        ![[/Untitled 1 5.png|Untitled 1 5.png]]
        
    3. unity 偏好设置→外部工具，确保配置好 sdk 和 ndk
        
        ![[/Untitled 2 5.png|Untitled 2 5.png]]
        
- 插件开发([可参考部分](https://blog.csdn.net/K20132014/article/details/109159008))
    1. 新建Android studio 项目
        1. Empty Activity
        2. 包名随意
        3. minimum SDK 跟 unity 项目保持一致
    2. 拷贝unity 的 classes.jar (/Applications/Unity/PlaybackEngines/AndroidPlayer/Variations/mono/Release/Classes\classes.jar) 到 项目 app/libs 目录下，右键 classes.jar→Add As Library
    3. MainActivity 删除 setContentView 行代码, 删除 layout 下 activity_main.xml
        
        ![[/Untitled 3 4.png|Untitled 3 4.png]]
        
    4. 修改 `build.gradle` `apply plugin: 'com.android.application` 改成 `apply plugin: 'com.android.library`, 删除 defaultConfig 下的 applicaionId 行
        
        ![[/Untitled 4 3.png|Untitled 4 3.png]]
        
    5. 在 `/Applications/Unity/Hub/Editor/2020.1.13f1/PlaybackEngines/AndroidPlayer/Source/com/unity3d/player/UnityPlayerActivity.java` 找到 UnityPlayerActivity.java, 直接拷贝source 目录下的 com 包到 java文件夹
    6. 修改 AndroidManifest.xml
        
        ```XML
        <manifest xmlns:android="http://schemas.android.com/apk/res/android"
            package="随便">
        
            <application>
              <!--表明这个Activity是启动Activity 一定要写完全的包名 路径-->
                <activity android:name="包名.MainActivity">
                   
                    <intent-filter>
                        <action android:name="android.intent.action.MAIN" />
                        <category android:name="android.intent.category.LAUNCHER" />
                    </intent-filter>
                    <meta-data android:name="unityplayer.UnityActivity" android:value="true" />
                </activity>
            </application>
        </manifest>
        ```
        
    7. 在 build.gradle 里加入依赖库，比如:
        
        ![[/Untitled 5 2.png|Untitled 5 2.png]]
        
          
        
    8. 新建一个 class，在里面写原生代码:
        
        ```Java
        package 路径;
        
        public class MyClass {
            private Class<?> unityPlayerClass;
            private Field unityCurrentActivity;
            private Method unitySendMessage;
        
            public void init () {
        
                //Get the UnityPlayer class using Reflection
                unityPlayerClass = Class.forName("com.unity3d.player.UnityPlayer");
                //Get the currentActivity field
                unityCurrentActivity= unityPlayerClass.getField("currentActivity");
                //Get the UnitySendMessage method
                unitySendMessage = unityPlayerClass.getMethod("UnitySendMessage", new Class [] { String.class, String.class, String.class } );
            }
        
            //Use this method to get UnityPlayer.currentActivity
            public Activity currentActivity () {
        
                Activity activity = (Activity) unityCurrentActivity.get(unityPlayerClass);
                return activity;            
            }
        
        
            public void unitySendMessageInvoke (String gameObject, String methodName, String param) {
                //Invoke the UnitySendMessage Method
                unitySendMessage.invoke(null, new Object[] { gameObject, methodName, param} );
            }
        
            public void makeToast (final String toastText, final int duration) {
                currentActivity().runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        Toast.makeText(getActivity(), toastText, duration).show();
                    }
                });
            }
        		// 别忘了调用
        		private void listenSDKData() {
        	        currentActivity().runOnUiThread(new Runnable() {
        	            @Override
        	            public void run() {
        	                MotrixiSDK.INSTANCE.setOnLogListener(new OnLogListener() {
        	                    @Override
        	                    public void onLogListener(String s) {
        	                        unitySendMessageInvoke("UnityAndroidConnect", "AndroidCallUnityMsg", s);
        	                    }
        	                });
        	            }
        	        });
        	    }
        }
        ```
        
    9. Build->Make Project，一般只要 `build/intermediates/arr_main_jar/debug/classes.jar` 就行
        
        ![[/Untitled 6 2.png|Untitled 6 2.png]]
        
        用压缩包打开jar 包，删除 com 目录下的 unity3D和 项目名最底层文件夹里的 BuildConfig.class
        
        ![[/Untitled 7 2.png|Untitled 7 2.png]]
        
    10. 把上述项目的 AndroidManifest.xml 和 导出的 classes.jar(可以改名)放到unity 中，路径如下
        
        jar 放到 Assets/Plugins/Android/libs 下
        
    11. 在`/Applications/Unity/Hub/Editor/2020.1.13f1/PlaybackEngines/AndroidPlayer/Tools/GradleTemplates` 路径下有 gradle 模板，把需要用到的放到 unity 项目 Assets/Plugins/Android 下:
        - BaseProjectTemplate.gradle: project 路径下的gradle
        - gradleTemplate: gradle 配置
        - mainTemplate: module 下的 gradle
    12. Unity 创建一个GameObject，命名与自定义java class 文件中的 gameObject 名字一致, Assets 下创建一个cs文件，关联到GameObject.
        
        cs 文件如下：
        
        ```C#
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using UnityEngine;
        using UnityEngine.UI;
        
        public class UnityAndroidConnect : MonoBehaviour
        {
        
            private string appKey = "";
        		// 两个按钮
            private GameObject resetButton;
            private GameObject uploadButton;
        		// 文本框
            private GameObject informationLabel;
        		// 文本框的文字
            public Text informtaionText;
        
            // AndroidJavaClass jc;
            AndroidJavaObject androidInstance; 
        
        
            // Start is called before the first frame update
            void Start()
            {
                try
                {
        						//参数就是jar 包的项目package name
                    androidInstance = new AndroidJavaObject("com.motrixi.unity.plugin.Motrixi");
                    if (null != androidInstance) 
                    {
        								// 参数为自定义 java 文件里的方法
                        androidInstance.Call("initPlugin");
        								androidInstance.Call("init", appKey)
                    }
                }
                catch (Exception e)
                {
                    Debug.Log( "init error:" + e.ToString());
                }
        				// 获取 resetButton
                resetButton = GameObject.Find("ResetButton");
                resetButton.GetComponent<Button>().onClick.AddListener(Reset);
        
                uploadButton = GameObject.Find("UploadButton");
                uploadButton.GetComponent<Button>().onClick.AddListener(DebugUpload);
        
                informationLabel = GameObject.Find("SdkInformationArea");
        
                informtaionText = GameObject.Find("SdkInformationArea").GetComponent<Text>();
            }
        
             public void Reset()
             {
                try
                    {
                        Debug.Log("Reset Clicked. ClickHandler.");
                        androidInstance.Call("resetConsentForm");
                    }
                catch (Exception e)
                    {
                        Debug.Log( "reset button error:" + e.ToString());
                    }
             }
        
        
             public void DebugUpload()
             {
                    try
                    {
                        Debug.Log("DebugUpload Clicked. ClickHandler.");
                        androidInstance.Call("upload");
                    }
                catch (Exception e)
                    {
                        Debug.Log( "DebugUpload button error:" + e.ToString());
                    }
             }
        		
        		// java 传给 unity 的方法
             public void AndroidCallUnityMsg(string recvMsg)
             {
                Debug.Log("recvMsg:" + recvMsg);
                informtaionText.text = recvMsg;
             }
        
            // Update is called once per frame
            void Update()
            {
                
            }
        }
        ```
        
    13. 导出Android项目就可以了