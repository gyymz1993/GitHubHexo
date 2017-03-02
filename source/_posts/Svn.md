---
title: 开发之Svn安装使用
date: 2016-12-21 16:28:38
tags: 
- svn
- Subversion
- TortoiseSVN
- VisualSVN
---

欢迎我的小博，我正在努力学习，我会在不久将来给你们分享更多的干货，希望你们喜欢。
## Please read happily

<!-- more -->
<The rest of contents | 余下全文>

 **为什么要使用SVN？**
      程序员在编写程序的过程中，每个程序员都会生成很多不同的版本，这就需要程序员有效的管理代码，在需要的时候可以迅速，准确取出相应的版本。
**Subversion是什么？**
   它是一个自由/开源的版本控制系统，一组文件存放在中心版本库，记录每一次文件和目录的修改，Subversion允许把数据恢复到早期版本，或是检查数据修改的历史，Subversion可以通过网络访问它的版本库，从而使用户在不同的电脑上进行操作。
### SVN服务器搭建和使用。
   **1.     首先来下载和搭建SVN服务器,下载地址如下: [http://subversion.apache.org/packages.html](http://subversion.apache.org/packages.html)，进入网址后，滚动到浏览器最底部看到如下截图：**

![VisualSvn](http://upload-images.jianshu.io/upload_images/433829-b8d72dc66da8fa49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![VisualSvn](http://upload-images.jianshu.io/upload_images/433829-227710abe31fcc6c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###  点击【Finish】即可完成安装。安装完成后,启动VisualSVN Server Manager,如图:

![](http://upload-images.jianshu.io/upload_images/433829-3af0e1e14833a637.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以在窗口的右边看到版本库的一些信息,比如状态,日志,用户认证,版本库等.
###  要建立版本库,需要右键单击左边窗口的Repositores,如下图:

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/433829-ec0cba0f5b59731f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###     **需要建立用户和组，并且需要分配权限**。
  1. 在VisualSVN Server Manager窗口的左侧右键单击用户组,选择Create User或者新建->User,如图:

![](http://upload-images.jianshu.io/upload_images/433829-27f5c527daa2795d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/433829-51137c53333509d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## Windows客户端SVN安装。
###  **1.首先我们需要下载 ”svn小乌龟”后，进行安装。 [http://download.csdn.net/detail/gyymz1992/7664323](http://download.csdn.net/detail/gyymz1992/7664323)**

###  **2：checkout项目文件。**新建或者进入目录下(比如qianduan1)，右键 --> Svn Checkout -->


![从服务器下载](http://upload-images.jianshu.io/upload_images/433829-ca6ccfeb6383a91b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## AndroidStudio客户端Svn安装。
**1.首先我们需要下载 ”TortoiseSVN”后，进行安装。 [http://download.csdn.net/detail/gyymz1992/9717754](http://download.csdn.net/detail/gyymz1992/9717754)**
###  ** 1. 安装成功后设置环境变量 **
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/433829-664cd5d03befdee8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###  ** 2. 设置AndroidStudio路径 **

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/433829-71f9a5fe1d48c555.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##  引用文章地址
 [http://www.cnblogs.com/armyfai/p/3985660.html](http://www.cnblogs.com/armyfai/p/3985660.html)**