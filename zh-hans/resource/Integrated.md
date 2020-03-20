# 集成 SDK
## 创建工程

在 Android Studio 中新建工程。

## 配置 build.gradle 

build.gradle 文件里添加集成准备中下载的 dependencies 依赖库。

```groovy
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
 }
    dependencies {
        implementation 'com.alibaba:fastjson:1.1.67.android'
        implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.12.3'
        implementation 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.2.0'
        implementation 'com.tuya.smart:tuyasmart:3.13.0'
    }
    
```

在根目录的 build.gradle 文件中增加 jcenter() 仓库

```groovy
repositories {
    jcenter()
}
```

>** [info] 【注意事项】**
>
> * 涂鸦智能 3.10.0 之前的版本的 sdk 默认只支持 armeabi-v7a，
> * 3.11.0 版本后已经将 armeabi-v7a、arm64-v8a 集成进 sdk，请将本地手动放入的 sdk 的相关 so 库移除，使用 sdk 中提供的。
> * 如果集成新版本 so 库。请移除之前老版本手动集成的库，防止冲突或者代码版本不一致导致的问题
> * 如有其他平台需要可前往 [GitHub](https://github.com/TuyaInc/tuyasmart_home_android_sdk/tree/master/so_libs) 获取。

## 集成安全图片

点击 "下载安全图片" ——"安全图片下载" 下载安全图片。

![](./images/download_t_s.png)

![](./images/download_t_s_1.png)

在集成准备中点击“下载安全图片”。将下载的安全图片命名为 “t_s.bmp”，放置到工程目录的 assets 文件夹下。

![](./images/addt_s.png)



## 设置 Appkey 和 AppSecret

在 AndroidManifest.xml 文件里配置 appkey 和 appSecret，在配置相应的权限等

```xml
<meta-data
android:name="TUYA_SMART_APPKEY"
android:value="应用 Appkey" />
<meta-data
android:name="TUYA_SMART_SECRET"
android:value="应用密钥 AppSecret" />

```

## 混淆配置

在 proguard-rules.pro 文件配置相应混淆配置

```bash
#fastJson
-keep class com.alibaba.fastjson.**{*;}
-dontwarn com.alibaba.fastjson.**

#mqtt
-keep class org.eclipse.paho.client.mqttv3.** { *; }
-dontwarn org.eclipse.paho.client.mqttv3.**

-keep class com.squareup.okhttp.** { *; }
-keep interface com.squareup.okhttp.** { *; }
-dontwarn com.squareup.okhttp.**

-keep class okio.** { *; }
-dontwarn okio.**

-keep class com.tuya.**{*;}
-dontwarn com.tuya.**
```

## 初始化 SDK
**描述**

用于初始化 SDK，请在 Application 中初始化 SDK，确保所有进程都能初始化。

**示例代码**

```java
public class TuyaSmartApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        TuyaHomeSdk.init(this);
      	
    }
}
```


appId 和 appSecret 需要配置 AndroidManifest.xml 文件里，也可以在初始化代码里初始化。

```java
TuyaHomeSdk.init(Application application, String appkey, String appSerect) 
```




## 注销涂鸦智能云连接
在退出应用的时候调用以下接口注销掉。

```java
TuyaHomeSdk.onDestroy();
```

## 调试开关

在 debug 模式下可以开启 SDK 的日志开关，查看更多的日志信息，帮助快速定位问题。在 release 模式下建议关闭日志开关。

```java
TuyaHomeSdk.setDebugMode(true);
```