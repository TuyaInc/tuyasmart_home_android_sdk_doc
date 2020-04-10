## 常见问题

1. 接口提示签名错误/权限校验失败

  确认 appKey、appSecret、安全图片是否与 IoT 平台上的信息一致，任意一个不匹配都将校验失败。具体请按照 [集成准备](https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/zh-hans/resource/Preparation.html) 和 [集成 SDK](https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/zh-hans/resource/Integrated.html) 章节来进行检查

2. 升级 SDK 后出现如下问题：

  ```
  java.lang.IllegalAccessError: Class okhttp3.EventListener extended by class com.tuya.smart.android.network.http.HttpEventListener is inaccessible (declaration of 'com.tuya.smart.android.network.http.HttpEventListener'***)
  ```

  请升级 SDK 依赖的 okhttp 版本号：

  `implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.12.3'`

## 配网常见问题

1. [Wi-Fi 设备配网常见问题请参照文档](Activator_wifi_faq.md)

