## 准备工作

您首先需要一个 Android 工程，这个工程可以是您现有的工程，也可以是您新建的一个空的工程。

## 第一步：创建项目和应用（已完成请跳过）

在使用我们的服务前，您必须先在 MobileLine 控制台上 [创建项目和应用](https://cloud.tencent.com/document/product/666/15345)。

## 第二步：添加配置文件（已完成请跳过）

在您创建好的应用上单击【下载配置】按钮来下载该应用的配置文件的压缩包：

![](http://tacimg-1253960454.cosgz.myqcloud.com/guides/project/downloadConfig.png)

解压该压缩包，您会得到 `tac_service_configurations.json` 和 `tac_service_configurations_unpackage.json` 两个文件，请您如图所示添加到您自己的工程中去。

<img src="http://tac-android-libs-1253960454.cosgz.myqcloud.com/tac_android_configuration.jpg" width="50%" height="50%">

>**注意：**
>请您按照图示来添加配置文件，`tac_service_configurations_unpackage.json` 文件中包含了敏感信息，请不要打包到 apk 文件中，MobileLine SDK 也会对此进行检查，防止由于您误打包造成的敏感信息泄露。


## 第三步：集成 SDK

#### 1. 在您应用级 build.gradle 文件（通常是 app/build.gradle）中添加 Authorization 服务依赖：

```
dependencies {
    // 增加这两行
    compile 'com.tencent.tac:tac-core:1.1.+'
    compile 'com.tencent.tac:tac-authorization:1.1.+'
}
```

#### 2. 添加 QQ SDK

手动下载 [QQ SDK](http://tac-android-libs-1253960454.cosgz.myqcloud.com/jars/open_sdk_r5923_lite.jar) ，并拷贝到应用模块的 `app/libs` 文件夹下，并在您应用级 build.gradle（通常是 app/build.gradle）文件中包含对 libs 目录的依赖：

```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
}
```

## 第四步：配置第三方渠道

登录 SDK 需要配置 QQ、微信等第三方渠道才能正常工作，关于如何配置第三方渠道，请参见 [配置第三方渠道](https://cloud.tencent.com/document/product/666/17846)。

到此您已经成功接入了 MobileLine 登录与授权服务。

## Proguard 配置

如果您的代码开启了混淆，为了 SDK 可以正常工作，请在 `proguard-rules.pro`文件中添加如下配置：

```
# MobileLine Core

-keep class com.tencent.qcloud.core.** { *;}
-keep class bolts.** { *;}
-keep class com.tencent.tac.** { *;}
-keep class com.tencent.stat.*{*;}
-keep class com.tencent.mid.*{*;}
-dontwarn okhttp3.**
-dontwarn okio.**
-dontwarn javax.annotation.**
-dontwarn org.conscrypt.**

# Wechat

-keep class com.tencent.mm.opensdk.** {*;}
-keep class com.tencent.wxop.** {*;}
-keep class com.tencent.mm.sdk.** {*;}

# QQ
-keep class com.tencent.connect.** {*;}
-keep class com.tencent.open.** {*;}
-keep class com.tencent.tauth.** {*;}
-keep class com.tencent.mobileqq.openpay.** {*;}
```
