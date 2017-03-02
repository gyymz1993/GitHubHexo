---
title: Android面试
date: 2016-12-07 15:29:30
tags: 
- 面试
- Android
---

欢迎我的博客，我会为你们奉献更多的干货，感谢大家的支持
## Please read happily

<!-- more -->
<The rest of contents | 余下全文>


## 经典中的经典四大组件
1 Activity 
2 Service
3 BroadCastRevceiver
4 ContentProviders

### Activity必须要了解的知识点
Activity的生命周期？
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/433829-b32d2883fc674dd0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
######  当我们启动一个Activity执行流程
onCreate->onStart->onResume
###### Activity退居后台:当我们点击返回后执行流程
onPause->onStop->onDestory
###### Activity退居后台:当我们点击Home后执行流程或者跳转新的Activity
onPaused->onStop
###### Activity返回前台:当我们点击Home后再次进入Activity
onRestart->onStart->onResume
###### 锁屏:onPause->Stop
###### 解锁 :onReStart->onStart->onResume
######  理解清楚整个生命周期中只有三个状态是稳定的，其他都是属于过渡状态很重要。
Resume:此时Activity处于运行状态位于栈顶，能和用户交互的状态；
Paused:此时Activity处理半遮挡状态，这个状态不能接受用户输入；
Stopped:完全被覆盖，也就是此Activity已经不可见了。

##### Activity中缓存方法以及数据恢复机制
在Activity中提供了两个很重要的方法
- onSaveInstanceState()
- onRestoreInstanceState()

######当Activity在未经你的许可，也就不是你人为销毁此Activity的情况下都会执行onSvaInstanceState方法来保存你的数据，举例说明几种情况会执行onSaveInstanceState
1 当用户按下Home键；
并且onSaveInstanceState中能保证在onStop之前执行，可能会在onPause之前也可能在后面。
2 长按Home键选择其他程序；
3 按下电源键关闭屏幕显示时；
4 从Activity中启动一个新的Activity
5 当屏幕方向切换时，如果没有指定ConfigChange属性
onSaveInstanceState方法的一般都是 记录Activity和UI的瞬间状态，不应该用这个方法不做持久化操作。

##### onRestoreInstanceState方法的恢复数据状态 
1 需要注意的是onSaveInstanceState
onRestoreInstanceState不一定是成双的；
2 onRestoreInstanceState执行条件是在此Activity的确被销毁了；
3 onSaveInstanceState中的Bundle也会传递到onCreate中,所以也可以选择在onCreate中恢复数据；
```@Override
 protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        outState.putString("anAnt","Android");
 }
```
##### Activity的四中启动模式
使用android:launchMode="standard|singleInstance|singleTask|singleTop"来控制Acivity任务栈。
- standard为默认启动模式，如果不指定其他模式则都会使用此模式启动，每次都会创建一个新的Activcity，并且将其置于任务栈的栈顶，而不管这个Activity是否创建，并且执行三回调（onCreate->onStart->onResume）
- singleTop为栈顶复用模式，系统判断你要启动的Activity是否位于栈顶，如果位于栈顶则直接使用，所以他的启动三回调不会执行，但是Activity的onNewIntent的方法会执行，如果Activity已存在不位于栈顶则和Standard模式一样。
- singleTask为栈内复用模式，singleTop判断顶栈元素是否是启动的Activity，而singleTask则判断栈内是否存在Activity，如果存在则至于栈顶，并且执行onNewIntent方法，以及会清理在当前Activity上面的所有Activity;
- singleInstance:为加强版的singleTask模式，这种模式类似使用浏览器，在多个程序中访问浏览器时，如果当前浏览器没有打开则先打开浏览器，否则直接在浏览器中访问，Activcity只能单独位于任务栈内，由于栈内复用的特性，所以后续的请求都不会创建新的Activity，除非这个独特的任务栈被系统销毁。

### Service必须了解的知识点
```
 public void startService(){
        //启动一个Service
        Intent intent=new Intent(this,Service.class);
        startService(intent);
  }
```
```
  public void startService(){
        Intent intent=new Intent(this, Service.class);
        bindService(intent, new ServiceConnection() {
            @Override
            public void onServiceConnected(ComponentName name, IBinder service) {}
            @Override
            public void onServiceDisconnected(ComponentName name) {}
        },BIND_AUTO_CREATE);
    }
```
上面是Service的两种启动方式
 ###### Activity相比，service的生命周期已经简单的不能再简单了
只有onCreate()->onStart()->onDestroy()三个方法。      
  Activity中和service有关的方法：        
- startService(Intent intent)：启动一个service        
- stopService(Intent intent) :停止一个service    

如果我们想使用service中的一些数据或者访问其中的一些方法，那么我们就要通过下面的方法：
- public boolean bindService(Intent intent, ServiceConnection conn, int flags) ；        
- public void unbindService(ServiceConnection conn); 

上面startService()和bindService()两种模式是完全独立的。你可以绑定一个已经通过startService()方法启动的服务
只要调用一次stopService()方法便可以停止服务，无论之前它被调用了多少次的启动服务方法

######注意：Service的onCreate的方法只会被调用一次，就是你无论多少次的startService又 bindService，Service只被创建一次。如果先是bind了，那么start的时候就直接运行Service的onStart方法，如果先是start，那么bind的时候就直接运行onBind方法。如果你先bind上了，就stop不掉了，只能先UnbindService, 再StopService,所以是先start还是先bind行为是有区别的。

#### IntentService的使用
因为Service默认都是在主线程中使用，所以如果在服务里处理一些耗时操作很容易出现ARN的情况
这个时候就可以用到IntentService，而且当IntentService执行完毕后会自动停止。

###Service怎么避免被杀毒软件杀掉和系统回收
1 Service设置为START_STICKY,Kill后会被重启，重传Intent，保证和重启前一样。
2 提升Service的优先级，在AndroidManifaster.xml中android:priority="1000"。
3 当Service销毁时发送个广播来重启Service
4 双进程守护
5 开启一个一像素的Activity在前台。
6 android的系统进程分为五个等级, Foreground Process(前台进程), Visible Process(可见进程), Service Process(服务进程), Background Process(后台进程), Empty Process(空进程), Service的进程处于第三个位置. 系统的回收会从低到高依次回收, 所以我们必须提高Service的等级；
仔细看Service的API会发现这么个方法 [参考链接](https://zhidao.baidu.com/question/986920772385515139)
- public final void startForeground (int id, Notification notification)
```
public class MyService extends Service {
    private void startForegroundCompat() {
        try {
            if (Build.VERSION.SDK_INT < 18) {
                Log.e(TAG, "startForgroundCompat");
                startForeground(1120, new Notification());
            }
        } catch (Exception e) {
        }
    }
```
如果这样做之后, 你会发现一键清理对你的Service是完全不起作用的。

### BroadcastReceive广播接收器
标准广播：是一个完全异步的广播，在广播发出后，所有的广播接收器机会都会在同一时刻收到这条广播消息，因此他们之间没有任何先后顺序而言。
有序广播：是一个同步执行广播，在 广播发出后，同一时刻只会有一个接收器接收到此广播，并且当广播接收器接收执行完毕后，广播才会继续传播，所以 他们是有先后顺序的，优先级越高则先收到广播，并且这样的广播接受者可以截断正在传播的 广播，这样后面的广播接受者就无法接收到广播了。
发送标准广播和有序广播只要改动一行代码 sendBroadcast()改成sendOrderBroadCast()
######广播的使用
- 动态注册广播
    registerReceiver(mBroadcastReceive,null);
    unregisterReceiver(mBroadcastReceive);
- 静态注册广播

1 Service的两种启动方法，有什么区别 1.在Context中通过public boolean bindService(Intent service,ServiceConnection conn,int flags) 方法来进行Service与Context的关联并启动，并且Service的生命周期依附于Context(不求同时同分同秒生！但求同时同分同秒屎！！)。
2  通过public ComponentName startService(Intent service)方法去启动一个Service，此时Service的生命周期与启动它的Context无关。
在AndroidManifaster中注册广播

###### 本地广播
前面得广播数据系统全局广播，如果你发的 广播只想本程序收到那么久可以使用本地广播
开启本地广播只需要得到本地广播管理器来发送和注册广播就可以LocalBoradCastManager
- mLocalBroadcastManager.registerReceiver(mBroadcastReceive,null);
- mLocalBroadcastManager.unregisterReceiver(mBroadcastReceive);

###  contentProvider内容提供者，跨程序数据共享 。
一个程序通过ContentProvider抽象接口将自己的数据提供了外部访问的接口，而且是以类似数据库中表的方式暴露出去。ContentProviders存储与检索数据，任何其他应用程序都可以对这部分数据进行访问。
1 创建自己的ContentProvider继承ContentProvider
2  在AndroidManifaster中注册自己 的ContenetProviders
3  通过设置 URL让CotentPorvider内部做类似数据库的响应操作
最后我们就可以更具此URL来实现数据的访问操作

### 解析XML的几种方式的原理和特点：DOM,SAX,PULL
DOM:消耗内存，先把xml文件读取到内存中，然后再用DOM API来访问树形结构，这个写起来很简单，但是消耗内存较大。
要是数据过大，手机不够牛逼，可以导致手机直接死机。

SAX:解析效率高，占内存少，基于事件驱动，更简单的说就是对文档进行顺序扫描，当扫面到的文档（doucument）开始和结束，元素
（element）开始和结束，文档（document）结束等地方通知事件处理函数，由事件处理函数做相应动作，然后继续同样的扫描，直到文档结束。

PULL：与SAX类似，也是基于事件驱动，我们可以调用他的next()方法，来获取下一个解析事件（就是开始文档，结束文档，开始标签，结束标签）
当处于某个元素时可以调用XmlPullParser的getAttributte()方法来获取属性的値，也可以调用他的nextText()获取本节点的値。

