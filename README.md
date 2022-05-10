![logo](https://github.com/gyf-dev/Screenshots/blob/master/ImmersionBar/readme_head.png)
# ImmersionBar -- android 4.4以上沉浸式实现 
[![version](https://img.shields.io/badge/version-3.2.2-brightgreen.svg)](https://bintray.com/geyifeng/maven/immersionbar) [![author](https://img.shields.io/badge/author-gyf--dev-orange.svg)](https://github.com/gyf-dev) [![简书](https://img.shields.io/badge/%E7%AE%80%E4%B9%A6-HeLe%E5%B0%8F%E5%AD%90%E6%8B%BD-blue.svg)](https://www.jianshu.com/p/2a884e211a62) [![QQ群](https://img.shields.io/badge/QQ%E7%BE%A4-314360549-red.svg)]()

## 直接看效果图，建议下载demo体验
<img width="300"  src="https://github.com/yanzhenjie/Sofia/blob/master/image/2.gif"/>

## 包引入说明
> 4.4以上版本(mavenCentral)
   ```groovy
   // 基础依赖包，必须要依赖
   implementation 'com.geyifeng.immersionbar:immersionbar:3.2.2'
   // kotlin扩展（可选）
   implementation 'com.geyifeng.immersionbar:immersionbar-ktx:3.2.2'
   ```

## 版本说明
#### [点我查看版本说明](https://github.com/gyf-dev/ImmersionBar/wiki)

## 下载demo 
#### [点我下载immersionBar-3.2.2.apk](https://github.com/gyf-dev/ImmersionBar/blob/master/apk/immersionbar-3.2.2.apk)

## 关于全面屏与刘海（特殊机型适配）//如果没有，这项可省略
#### 关于全面屏
   在manifest加入如下配置
    在manifest的Application节点下加入
   ```xml
      <meta-data 
        android:name="android.max_aspect"
        android:value="2.4" />
   ```

#### 关于刘海屏 
  在manifest的Application节点下加入，vivo和oppo没有找到相关配置信息
   ```xml
      <!--适配华为（huawei）刘海屏-->
      <meta-data 
        android:name="android.notch_support" 
        android:value="true"/>
      <!--适配小米（xiaomi）刘海屏-->
      <meta-data
        android:name="notch.config"
        android:value="portrait|landscape" />
   ```
  
## Api详解
- 基础用法

    ```java
    ImmersionBar.with(this).init();
    ```
- 高级用法(每个参数的意义)

    ```java
     ImmersionBar.with(this)
                 .transparentStatusBar()  //透明状态栏，不写默认透明色
                 .transparentNavigationBar()  //透明导航栏，不写默认黑色(设置此方法，fullScreen()方法自动为true)
                 .transparentBar()             //透明状态栏和导航栏，不写默认状态栏为透明色，导航栏为黑色（设置此方法，fullScreen()方法自动为true）
                 .statusBarColor(R.color.colorPrimary)     //状态栏颜色，不写默认透明色
                 .navigationBarColor(R.color.colorPrimary) //导航栏颜色，不写默认黑色
                 .keyboardMode(WindowManager.LayoutParams.SOFT_INPUT_ADJUST_RESIZE)  //单独指定软键盘模式
                 .setOnKeyboardListener(new OnKeyboardListener() {    //软键盘监听回调，keyboardEnable为true才会回调此方法
                       @Override
                       public void onKeyboardChange(boolean isPopup, int keyboardHeight) {
                           LogUtils.e(isPopup);  //isPopup为true，软键盘弹出，为false，软键盘关闭
                       }
                  })
                 .setOnNavigationBarListener(onNavigationBarListener) //导航栏显示隐藏监听，目前只支持华为和小米手机
                 .setOnBarListener(OnBarListener) //第一次调用和横竖屏切换都会触发，可以用来做刘海屏遮挡布局控件的问题
                 .addTag("tag")  //给以上设置的参数打标记
                 .getTag("tag")  //根据tag获得沉浸式参数
                 .reset()  //重置所以沉浸式参数
                 .init();  //必须调用方可应用以上所配置的参数
    ```
## 在Activity中实现沉浸式

- java用法

   ```java
    ImmersionBar.with(this).init();
   ```
- kotlin用法
 
   ```kotlin
    immersionBar {
        statusBarColor(R.color.colorPrimary) 
        navigationBarColor(R.color.colorPrimary)
    }
   ```
  

## 在Fragment中实现沉浸式
......

## 在Dialog中实现沉浸式，具体实现参考demo
- ①结合dialogFragment使用，可以参考demo中的[BaseDialogFragment](https://github.com/gyf-dev/ImmersionBar/tree/master/immersionbar-sample/src/main/java/com/gyf/immersionbar/sample/fragment/dialog/BaseDialogFragment.java)这个类
   ```java
       ImmersionBar.with(this).init();
   ```
- ②其他dialog，关闭dialog的时候必须调用销毁方法
    ```java
        ImmersionBar.with(this, dialog).init();
    ```
    销毁方法：
    
    java中
    ```java
        ImmersionBar.destroy(this, dialog);
    ```
    kotlin中
    ```kotlin
        destroyImmersionBar(dialog)
    ```
   
<img width="300"  src="https://github.com/gyf-dev/Screenshots/blob/master/ImmersionBar/Screenshot_dialog.gif"/>

## 在PopupWindow中实现沉浸式，具体实现参考demo
   重点是调用以下方法，但是此方法会导致有导航栏的手机底部布局会被导航栏覆盖，还有底部输入框无法根据软键盘弹出而弹出，具体适配请参考demo。
   ```java
       popupWindow.setClippingEnabled(false);
   ```

## 各种疑难问题的描述，及其解决方案


     ```
       
## 解决EditText和软键盘的问题

    .....

## 当白色背景状态栏遇到不能改变状态栏字体为深色的设备时，解决方案
   .....
   
## 混淆规则(proguard-rules.pro)

   ```
    -keep class com.gyf.immersionbar.* {*;} 
    -dontwarn com.gyf.immersionbar.**
   ```
    

## 额外说明 ##
.....

## 联系我 ##
- QQ群 xxxxxxx（问题交流）
