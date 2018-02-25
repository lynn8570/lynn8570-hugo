---
title: "Understanding the Treasure Hunt sample game"
date: "2018-02-26"
categories: 
    - "ANDROID"
---
# Google VR SDK 寻宝游戏code overview

## Manifest 文件

- VR应用属性

  ```
  <manifest ...>
      <uses-sdk android:minSdkVersion="19" android:targetSdkVersion="24"/>
      ...
      <uses-feature android:glEsVersion="0x00020000" android:required="true" />
      <uses-feature android:name="android.software.vr.mode" android:required="false"/>
      <uses-feature android:name="android.hardware.vr.high_performance" android:required="false"/>
      ...
      <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
      ...
  </manifest>
  ```

  Google VR SDK 支持的最低版本为api 19, 另外Daydream 应用的target API 要24或者以上级别。需 OpenGL ES 2.0 支持，可正确渲染VR内容。`<uses-feature android:name="android.software.vr.mode" android:required="false"/>`和`<uses-feature android:name="android.hardware.vr.high_performance" android:required="false"/>` 由 Android N加入的新特性，前者表示需要使用Android VR模式，后者表示需要可支持Daydream的设备。

  对于没有Google VR服务的设备，需要安装Google VR 服务，才可以将可支持Daydream的设备与对应的VR viewer配对。因此还需要添加`READ_EXTERNAL_STORAGE`权限。


- VR Activity 属性

  Activity也需要添加一些属性声明，才可兼容Daydream

  ```
  <activity
      android:name=".MyActivity"
      android:screenOrientation="landscape"
      android:enableVrMode="@string/gvr_vr_mode_component"
      android:theme="@style/VrActivityTheme"
      android:resizeableActivity="false"
      android:configChanges="density|keyboardHidden|navigation|orientation|screenSize|uiMode"
      ...>

  ```

  `enableVrMode`属性用于启用Android VR 模式，Android 7.0 N 引入的功能特性，用于支持高性能的移动 VR 应用。该属性表示，当启动Activity的时候，系统需要自动启动VR模式。

  > 启动 VR activity的时候，屏幕会有些轻微的闪烁，这是因为当启动VR模式的时候，Android需要切换到低持久性模式显示。

  `android:theme="@style/VrActivityTheme"`确保Activity在VR转换期间正常运行，`android:resizeableActivity="false"`表明Activity不可调整显示大小，不与其他的Activity分屏。landscape表明屏幕需要横屏显示。

  `configChanges`可避免activity因为一些配置变化而造成activity的重新创建。

  Google VR应用基本和要求：

  https://developers.google.com/vr/distribute/daydream/app-quality

  - 设计要求：
    1. 物体对象需要放置在一定的距离，以便用户可以看清楚而不是看到两张图片。如果需要辅助文字，需要保证文字的可读性。建议物体对象需要放置在0.5米距离以上
    2. 需要维护头部动作位置追踪
    3. 地平线维持，不至于倾斜
    4. 相机操作需要用户启动，但可以不是一直直接的控制操作
    5. app不干涉系统级别的复位行为
    6. …….
  - 功能要求
    1. 使用支持的VR SDK版本
    2. 使用Daydream API进行activity切换`daydreamApi.launchVrHomescreen();`  `daydreamApi.launchInVr(componentName);`
  - ​

- ​





