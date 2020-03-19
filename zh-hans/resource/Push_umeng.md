# 集成友盟

国内 Push 功能是基于友盟推送开发的，请先参考[友盟文档](https://developer.umeng.com/docs/66632/detail/66744)将友盟集成到项目中，涂鸦云支持友盟第三方通道，如果需要小米、华为、魅族通道，去各个平台申请，并且依照友盟文档初始化。

### 配置信息

将友盟申请方式可以参考文档[**友盟推送 Key 申请流程**](https://docs.tuya.com/docDetail?code=K8uhkjmak2nn8)

将申请到的 app key 等信息复制到 “APP 工作台”-“APP SDK”-对应应用的配置中，

> ⚠️请勿将信息配置错误：
>
> * 确认友盟后台包名与 sdk 应用包名一致
> * Umeng Message Secret 和 App Master Secret 不要配置反了
> * 友盟后台 “启用服务器 IP 地址” 需要手动关闭

<img src="images/push_umeng_config.png" style="zoom: 33%;" />

### 设置用户别名

在确保友盟已经集成到项目中后，通过友盟 SDK 设置用户 id，推送时会按照用户 id 向用户推送消息

```java
mPushAgent.setAlias(aliasId, ALIAS_TYPE, new UTrack.ICallBack() {
    @Override
    public void onMessage(boolean isSuccess, String message) {
    }
});
```

**参数说明**

| 参数       | 说明                                      |
| ---------- | ----------------------------------------- |
| aliasId    | 可以是你的应用为每个用户自动生成的唯一 id |
| ALIAS_TYPE | 需要填 "TUYA_SMART"                       |

### 注册涂鸦云 Push

将 aliasId 注册到涂鸦云，（必须！）

**参数说明**

| 参数         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| aliasId      | 用户别名 将上一步中拿到的别名注册到涂鸦云，涂鸦云将会以该别名向 app 推送消息 |
| pushProvider | 注册 push 的类别 ，友盟需填写："umeng"                       |

**示例代码**

```java
TuyaHomeSdk.getPushInstance().registerDevice(String aliasId, String pushProvider, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }

    @Override
    public void onSuccess() {

    }
});
```

### 第三方通道设置

如果使用了友盟第三方通道，弹窗的 activity 必须命名为 SpecialPushActivity.

以小米为例，SpecialPushActivity继承自 UmengNotifyClickActivity ，并且完整的包名路径为`com.activity.SpecialPushActivity`.

### Push消息接收

继承 UmengMessageService, 实现自己的 Service 来完全控制达到消息的处理，参考友盟文档

```java
public class MyPushIntentService extends UmengMessageService {
    @Override
    public void onMessage(Context context, Intent intent) {
        try {
            String message = intent.getStringExtra(AgooConstants.MESSAGE_BODY);
            UMessage msg = new UMessage(new JSONObject(message);
            Log.d(TAG, "message=" + message);      //消息体
            Log.d(TAG, "custom=" + msg.custom);    //自定义消息的内容
            Log.d(TAG, "title=" + msg.title);      //通知标题
            Log.d(TAG, "text=" + msg.text);        //通知内容
            
            PushBean pushBean = PushBean.formatMessage(msg.custom)

        } catch (Exception e) {
            L.e(TAG, e.toString());
        }
}
```

>说明
> - msg.custom 中的内容就是收到的推送信息
> - msg.custom 的具体协议格式：
>	custom=tuya://message?a=view&ct="title"&cc="content"&p=>{}&link=tuyaSmart%3A%2F%2Fbrowser%3Furl%3Dhttp%253A%252F%252Fwww.baidu.com;
>- 通过 PushBean.formatMessage() 来对数据进行解析得到 PushBean

### 用户解绑

**接口说明**

在用户退出登录等需要解除应用和用户关系的操作下调用友盟的移除别名的方法

```java
mPushAgent.deleteAlias(aliasId, "TUYA_SMART", new UTrack.ICallBack() {
    @Override
    public void onMessage(boolean isSuccess, String message) {
    }
});
```

**参数说明**

| 参数       | 说明                  |
| ---------- | --------------------- |
| aliasId    | 用户自动生成的唯一 id |
| ALIAS_TYPE | TUYA_SMART            |

### 发送 Push

#### 新增运营 Push

涂鸦开发者平台 - 用户运营 - 消息中心 - 新增消息

![](images/android-push-setting-operation.png)

#### 新增告警 Push

涂鸦开发者平台 - 对应产品 - 扩展功能 - 告警设置 - 新增告警规则(应用推送方式)

![](images/android-push-setting-warning.png)