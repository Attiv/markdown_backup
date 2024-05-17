> 我们日常开发中，自认为对Activity的生命周期了然于胸(onCreate , onStart , onResume , onPause , onStop , onDestroy , onRestart)，但是，是真的对Activity声明周期融会贯通了吗？  
> 对透明主题的 Activity 的生命周期变化呢？  

本文对 `Android` 中 `Activity` 间交互所引起的生命周期变化进行详细的分析~

_注：  
下文所有  
_`_Activity_` _均指普通风格，非透明的_ `_Activity_`_，透明风格的_ `_Acitivity_` _统一表示为_ `_TransActivity_` _。_

---

# Q1: `Activity1` 启动 `Activity2` 问题

** Question：描述 `MainActivity` 启动 `SecondActivity` ,生命周期变化过程？**

** Answer：**

> MainActivity 启动： onCreate() --- onStart() --- onResume()

- `startActivity(new Intent(MainActivity.this, SecondActivity.class))` 流程：`MainActivity - onPause()` --- `SecondActivity - onCreate()` --- `SecondActivity - onStart()` --- `SecondActivity - onResume()` --- `**MainActivity - onStop**`

**重点(敲黑板)：**

我们都知道 `Activity` 停止活动的时候流程是 `onPause` - `onStop`，但是在结合启动一个新的 `Activity` 的时候呢？

答案就是：

> 1、当前一个 Activity 执行完 onPause() 方法后，才会执行启动的 Activity 的 onCreate()  
> 方法；  
> 2、当启动的 Activity 执行完 onResume() 方法后才会去执行前一个 Activity 的 onStop() 方法。  

按照基本法，附上测试的Log信息：

```Plain
//启动 MainActivity
04-14 23:34:52.692 22963-22963/com.burjal.performancetest I/MainActivity: ====onCreate=====
04-14 23:34:52.692 22963-22963/com.burjal.performancetest I/MainActivity: ====onStart=====
04-14 23:34:52.692 22963-22963/com.burjal.performancetest I/MainActivity: ====onResume=====

//从 MainActivity 打开 SecondActivity
04-14 23:34:57.532 22963-22963/com.burjal.performancetest I/MainActivity: ====onPause=====
04-14 23:34:57.562 22963-22963/com.burjal.performancetest I/SecondActivity: ====onCreate=====
04-14 23:34:57.562 22963-22963/com.burjal.performancetest I/SecondActivity: ====onStart=====
04-14 23:34:57.562 22963-22963/com.burjal.performancetest I/SecondActivity: ====onResume=====
04-14 23:34:57.972 22963-22963/com.burjal.performancetest I/MainActivity: =====onStop====
```

**总结:**

> 1、优化 Activity 启动速度的时候，把相关数据持久化的耗时操作放在 onStop() 方法中，因为新的Activity 是在前一个 Activity 执行完 onPause() 方法才会开始创建;  
> 2、Activity 界面对用户可见是在 onResume() 方法执行完之后，所以一味地把相关启动操作从 onCreate() 移动到 onResume() 方法，成效并不大。  

经过上述问题，我们又会想到，那从 `SecondActivity` 返回到 `MainActivity` ，两个 `Activity` 的生命周期变化流程又是如何的呢？下面我们引入 `Q2` 问题。

---

# Q2: 从 `Activity2` 返回 `Activity1` 问题

** Question：描述 `SecondActivity` 返回到 `MainActivity` ,生命周期变化过程？**

** Answer：**

> onBackPressed() 流程：SecondActivity - onPause() --- MainActivity - onRestart() --- MainActivity - onStart() --- MainActivity - onResume() --- SecondActivity - onStop() --- SecondActivity - onDestroy()

众所周知，`onBackPressed()` 后直接调用到返回的 `Activity` 的 `onRestart()` 方法，但是我们很少结合到两个 `Activity` 交互并综合去看它们的声明周期问题。

通过 `Q1` 问题，其实很容易想到 `Q2` 的答案，就是在 `MainActivity` 的 `onResume()` 方法执行完后再去顺序执行 `SecondActivity` 的 `onStop()` , `onDestroy()` 方法。

同样，附上测试的Log信息：

```Plain
04-14 23:48:10.692 22963-22963/com.burjal.performancetest I/SecondActivity: ====onPause=====
04-14 23:48:10.692 22963-22963/com.burjal.performancetest I/MainActivity: ====onRestart=====
04-14 23:48:10.692 22963-22963/com.burjal.performancetest I/MainActivity: ====onStart=====
04-14 23:48:10.692 22963-22963/com.burjal.performancetest I/MainActivity: ====onResume=====
04-14 23:48:11.062 22963-22963/com.burjal.performancetest I/SecondActivity: =====onStop====
04-14 23:48:11.062 22963-22963/com.burjal.performancetest I/SecondActivity: ====onDestroy=====
```

**通过上述两个试验我们得出如下结论**(敲黑板，这是真重点啊，盆友们)：

> 两个 Activity 涉及到互相切换的时候，执行完前一个 Activity 的 onPause() 方法后，立即进入目标 Activity 对应生命周期中去，当目标 Activity 执行完 onResume() 方法后，再顺序执行进入到前一个 Activity 的 onStop() 方法(返回的情况下还有 onDestroy() 方法)。

> 所以，在 Activity 启动速度优化上，也要考虑到 onPause() 减负问题。

---

# Q3: `Activity1` 启动 `TransActivity2` 问题

** Question：描述 `LifecycleListActivity` 启动 `LifecycleTransActivity` ,生命周期变化过程？**

首先，我们需要明确的是，在 `Android` 中设置透明主题方式可以通过`Theme.Translucent` 实现。

** Answer：**

> startActivity(new Intent(LifecycleListActivity.this, LifecycleTransActivity.class)) 流程：LifecycleListActivity - onPause() --- LifecycleTransActivity - onCreate() --- LifecycleTransActivity - onStart() --- LifecycleTransActivity - onResume()

** 重点(敲黑板)：**

> 对比与 Q1 打开普通 Activity 对比，少了前一个 Activity 的 onStop() 方法

- 我们都知道 `onPause()` 方法是当前 `Activity` 即将进入后台时调用，`onStop()` 方法是当前 `Activity` 不在对用户可见时调用
- 在 `LifecycleListActivity` 打开 `LifecycleTransActivity` 后，由于 `LifecycleListActivity` 进入后台，所以此时会调用 `LifecycleListActivity - onPause()` 方法。在 `LifecycleTransActivity - onResume()` 后，此时由于 `LifecycleTransActivity` 是透明主题，所以 `LifecycleListActivity` 对用户来说还是可见的(只是不能获取焦点能事件)，***所以不会执行 `LifecycleListActivity - onStop()` 方法 *** 。

按照惯例，附上测试的Log信息：

```Plain
04-29 16:40:39.033 16188-16188/com.burjal.androidcomponent I/LifecycleListActivity: ==[onPause]==
04-29 16:40:39.053 16188-16188/com.burjal.androidcomponent I/LifecycleTransActivity: ==[onCreate]==
04-29 16:40:39.083 16188-16188/com.burjal.androidcomponent I/LifecycleTransActivity: ==[onStart]==
04-29 16:40:39.083 16188-16188/com.burjal.androidcomponent I/LifecycleTransActivity: ==[onResume]==
```

---

# Q4: 从 `TransActivity2` 返回 `Activity1` 问题

** Question：描述 `LifecycleTransActivity` 返回到 `LifecycleListActivity` ,生命周期变化过程？**

** Answer：**

> onBackPressed() 流程：LifecycleTransActivity - onPause() --- LifecycleListActivity - onResume() --- LifecycleTransActivity - onStop() --- LifecycleTransActivity - onDestroy()

从透明风格的 `TransActivity` 返回到 `Activity`，生命周期变化基本同 **Q2(普通** `**Activity**` **返回问题)**。差别就是，此时返回不需要走 `onRestart() - onStart()` 流程，直接进入返回 `Activity` 的 `onResume()` 方法。

同样，附上测试的Log信息，有Log有真相:

```Plain
04-29 16:59:34.033 16188-16188/com.burjal.androidcomponent I/LifecycleTransActivity: ==[onPause]==
04-29 16:59:34.043 16188-16188/com.burjal.androidcomponent I/LifecycleListActivity: ==[onResume]==
04-29 16:59:34.063 16188-16188/com.burjal.androidcomponent I/LifecycleTransActivity: ==[onStop]==
04-29 16:59:34.063 16188-16188/com.burjal.androidcomponent I/LifecycleTransActivity: ==[onDestroy]==
```

---

# End

下面附上 `Activity` 各生命周期官方解释:

> onCreate(Bundle savedInstanceState) : Called when the activity is starting. This is where most initialization should go: calling setContentView(int) to inflate the activity's UI, using findViewById() to programmatically interact with widgets in the UI, calling managedQuery(android.net.Uri , String[], String, String[], String) to retrieve cursors for data being displayed, etc.

> onResume() : Called after onRestoreInstanceState(), onRestart(), or onPause(), for your activity to start interacting with the user.This is a good place to begin animations, open exclusive-access devices(such as the camera), etc.

> onStart() : Called after onCreate(); or after onRestart() when  
> the activity had been stopped, but is now again being displayed to the user. It will be followed by onResume().  

> onRestart() : Called after onStop() when the current activity is being re-displayed to the user (the user has navigated back to it). It will be followed by onStart() and then onResume().

> onPause() : Called as part of the activity lifecycle when an activity is going into the background, but has not (yet) been killed. The counterpart to onResume().

> onStop() : Called when you are no longer visible to the user. You will next receive either onRestart(), onDestroy(), or nothing,depending on later user activity.

> onDestroy() :Perform any final cleanup before an activity is destroyed. This can happen either because the activity is finishing (someone called finish() on it, or because the system is temporarily destroying this instance of the activity to save space. You can distinguish between these two scenarios with the isFinishing() method.

当然，在 `Android` 优化中，还有很多问题需要去继续探索，这篇文章主要是分享关于 **多** `**Activity**` **切换的生命周期问题** 。