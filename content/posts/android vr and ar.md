---
title: "Android vr ar"
date: "2018-02-25"
categories: 
    - "ANDROID"
---
# Android VR-AR 

如果接下来要做AR眼镜相关的项目，目前需要做一些知识储备。所以本文做为一个项目开始前的准备工作。了解目前已知行业先行者已经实现的技术是已经到了一个什么样的程度后，才知道我们要前进的方向。着重了解Google和目前接触到的一个比较完善的vr-ar系统公司睿悦Niburu。

## VR和AR的概念

VR(Vritual Reality)虚拟现实，最直白的说就是纯虚拟的数字画面。理解起来就是，用户在VR中看到的所有东西都是虚拟的，但是这些虚拟的东西又需要让用户感觉到很真实。

AR(Argumented Reality)增强现实，虚拟数字画面+裸眼现实

此外现在还有一个概念提出来，MR(Mediatd Reality)介导现实，数字化现实+虚拟数字画面



- VR和AR的关系，可以理解为，VR为AR的一种极端情况。即假设我们把人眼的内容分为现实中真实的部分+数字投放的Argumentation（增强）部分。那么如果这种虚拟的部分越来越多以至于一种极端的情况，几乎没有的真实的部分，这种情况下叫：VR。所以这样理解起来，VR是AR的一个真子集。虚拟的东西占了全部，以至于越来越偏离了原来的现实原点。

- MR 数字化的视觉感知。对本身现实的感知能力的大小。例如让你有能力看到更小的东西，例如让佩戴者像有了X射线般的超级视力，看到皮肤下的血管？？？超能力！！或者是在现实的景物傻姑娘加以渲染，置身奇幻世界等等。所以MR是视觉能力维度上的提升。

  ![知乎图示](https://pic3.zhimg.com/80/817549fc583ef153904ef2f324e3fa0f_hd.jpg)

  他们三者的关系像是：在AR之外，增加了数字化的感知能力。

  ![知乎图示](https://pic4.zhimg.com/80/f208e8d885ed7749c9b1c53988f85593_hd.jpg)

> 以上整理自36kr，作者艾韬，易瞳科技CTO，师从Steve Mann。

为什么不是同心圆，而是有偏离呢？全图其实还有：

![](http://a.36krcnd.com/nil_class/6d8fab32-010b-4d77-bf31-20af3eb0358e/7B22.tmp.jpg!heading)

还有个Mixed，混合现实。如果我们把同心圆的原点认为是真实世界的原点。这几个概念给我们的感受是怎样的？

## 市面上的AR-VR眼镜

- 轻量级AR - Google Glass，单眼棱镜光学透视的设计方案，提示型系统
- 中量级AR - Hololens，双目棱镜光学透视方案，还有例如亮风台
- 重量级AR - HTC the Void 动态VR 眼镜，头戴VR显示，背上电脑，将真实的环境渲染成游戏场景。
- 纯VR - VR头盔



## Google VR 做了什么

- DayDream

  > Daydream是由谷歌2016年11月10日发布的一个vr平台，由一个头盔，一个控制杆盒很多兼容的智能手机组成。

  ![](http://7xl98n.com1.z0.glb.clouddn.com/QQ20180225-151253@2x.png)

  我们可以使用google提供的VR SDK来开发Daydream app

  - 硬件

    Daydream 或者 cardboard

    ![](http://7xl98n.com1.z0.glb.clouddn.com/QQ20180225-153056@2x.png)

  - 软件

    android studio，Nougat（API 25）or higher, Google VR SDK

  - VR SDK sample

    sdk-treasurehunt：示例应用，可以展示搜索和搜集物品。

    sdk-controllerclient 	主要演示接收和处理daydream的控制输入

    sdk-simplepanowidget 	可以载入全景视图的组件
    sdk-simplevideowidget 	可以渲染360度视频的视图组件 VRView
    sdk-video360 	可以渲染360度视频的视图组件
    sdk-videoplayer 	通过 Asynchronous Reprojection Video Surface API来播放视频，

  - Treasure Hunt 示例应用演练

    这个应用体现的Google VR SDK的核心功能：**Stereo rendering** 立体渲染，将app的view进行立体渲染，从而创造出3D的体验；**Spatial audio** 空间音效，制造出声音从不同地方出来的效果，增强现实体验；**Head movement tracking**根据头部动作，更新视图；**User input**用户输入响应，接收Daydream controller或者Cardboard 按钮的输入。

    *Todo: [Treasure Hunt walkthrough](https://developers.google.com/vr/android/samples/treasure-hunt) 详细走一遍sample的代码* 

  - 开发GoogleVR项目步骤

    1. 配置项目等级

       ```
       // The Google VR SDK requires version 2.3.3 or higher.
           classpath 'com.android.tools.build:gradle:2.3.3'

           // The Google VR NDK requires experimental version 0.9.3 or higher.
           // classpath 'com.android.tools.build:gradle-experimental:0.9.3'

       ```

    2. 添加依赖库

       ```
       dependencies {
            // Adds Google VR spatial audio support
            compile 'com.google.vr:sdk-audio:1.80.0'

            // Required for all Google VR apps
            compile 'com.google.vr:sdk-base:1.80.0'
         }

       ```

    3. 配置ProGuard

       如果需要使用proguard来减小apk文件大小的话，需要添加

       ```
       buildTypes {
               release {
                   minifyEnabled true
                   proguardFiles.add(file('../../proguard-gvr.txt'))
               }
           }

       ```

    4. 接下来需要哪些知识储备：

       - 浏览一遍谷歌VR示例代码 Treasure Hunt，寻宝游戏

       - GoogleVRSDK视频和全景图片示例应用

       - GoogleVR设计和开发准则

       - android空间音频效果开发向导

       - Google VR API

       - Daydream，学习Daydream用户交互控制器相关操作，可查看Review the controller library in **gvr-android-sdk** > **libraries** >
           **sdk-controller** ，查阅 库api 控制器 API

         > 原文链接如下：

       - [Treasure Hunt sample code walkthrough](https://developers.google.com/vr/android/samples/treasure-hunt)

       - [Google VR SDK video and panoramic image sample app walkthrough](https://developers.google.com/vr/android/samples/vrview)

       - Learn about Google VR design and development principles in [Daydream elements](https://developers.google.com/vr/elements/overview).

       - [Spatial audio for Android tutorial](https://developers.google.com/vr/android/spatial-audio)

       - [Google VR API Reference](https://developers.google.com/vr/android/reference_overview)

       - Daydream:

          Learn about implementing Daydream controller user interactions   in your app:

         - Review the controller library in **gvr-android-sdk** > **libraries** >  **sdk-controller**.
         - See also the [controller library API reference](https://developers.google.com/vr/android/reference/com/google/vr/sdk/controller/package-summary).


- Tilt Brush

  3d空间绘画

  Oculus Rift and HTC VIVE可支持该功能。

  都是vr头戴式设备

  ​

- Earth VR

  vr 视角来查看一些风景名胜

- Cardboard

- Expeditions

  教育类相关，旅行远征，例如体验在火星表面，老师可以带着孩子进行更有沉浸式的体验

- Jump

  Jump is Google's professional VR video solution. Jump makes 3D-360 video
   production at scale possible with best-in-class automated stitching. 
  Jump cameras are designed to work with the Jump Assembler to enable 
  seamless VR video production.

  一系列的摄像头产品，用于拍摄全景视频，自动缝合技术，实现

- Developers

## Google AR 提供了什么

https://developers.google.com/ar/discover/

ARCore 是一个用于在 Android 上构建增强现实应用的平台。ARCore 使用三个主要技术将虚拟内容与通过手机摄像头看到的现实世界整合：

- [**运动跟踪**](https://developers.google.com/ar/discover/concepts#motion_tracking)让手机可以理解和跟踪它相对于现实世界的位置。
- [**环境理解**](https://developers.google.com/ar/discover/concepts#environmental_understanding)让手机可以检测平坦水平表面（例如地面或咖啡桌）的大小和位置。
- [**光估测**](https://developers.google.com/ar/discover/concepts#light_estimation)让手机可以估测环境当前的光照条件。



### Arcore SDK概览

需要android 7.0以上，需要安装arcore

Cv java

Hello AR java  

但是安装了之后，在7.1上又提示 “this device does not support AR”



## Google VR AR 在现有平台上的运行情况

1. 寻宝游戏，demo 代码根据vr提供的sdk实现了左右分屏的这种效果，也就是说只要运行在普通的安卓手机上，在屏幕上，就可以看到一个左右分屏显示的功能，然后如果配合Google 的cardboard viewer 或者是 Daydream viewer 是可以直接在眼睛上实现3D显示的。那这个demo在我们的820+眼镜上的运行效果就是。在切换到2D模式的时候，我们看到的就是两个左右的图片，切换到3d的时候，确实可以实现看到一个叠加的图片，但是这个叠加后的有些变形。
2. ​









## Niburu 系统







## Niburu VR 可以做什么

Google Daydream 是否支持？

其他平台的VR兼容性？



## Niburu AR 可以 做什么



## Unity



## Unreal