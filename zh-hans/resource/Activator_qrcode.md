### 扫设备二维码配网

#### 描述

该功能只适用于已连接互联网的设备


```sequence

Title: 扫设备二维码配网

participant Device
participant httpdns
participant mqtt
participant APP
participant cloud

Note over Device: 设备上电联网
Note over Device: 重置设备为待配网状态

Device -> httpdns: 选择 httpdns，获取 mqttsUrl 域名
httpdns -> Device: 返回 mqttsUrl 域名
Device -> mqtt: 使用 uuid 连接 mqtt

APP -> Device: 扫设备二维码
APP -> cloud: APP 获取设备 uuid，向云端创建 token
APP -> cloud: 根据 token 轮询入网设备

cloud -> mqtt: 推送 token 和 region
mqtt -> Device: 透传给设备

Device -> cloud: 去激活设备
cloud -> Device: 激活成功

cloud-->APP: 激活成功，返回成功设备列表

```

#### 获取设备uuid

```java
Map<String, Object> postData = new HashMap<>();
//二维码扫码得到的url
postData.put("code", url);

TuyaHomeSdk.getRequestInstance().requestWithApiNameWithoutSession("tuya.m.qrcode.parse", "4.0", postData, String.class, new ITuyaDataCallback<String>() {
    @Override
    public void onSuccess(String result) {
      //从result中得到uuid  
      Log.i("TAG" , result);
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
        Log.i("TAG" , errorCode);
    }
});
```

#### 初始化配网参数

```java
TuyaQRCodeActivatorBuilder builder = new TuyaQRCodeActivatorBuilder()
        .setUuid(uuid)
        .setHomeId(homeId)
        .setContext(mActivity)
        .setTimeOut(timeout)
        .setListener(new ITuyaSmartActivatorListener() {
            
                @Override
                public void onError(String errorCode, String errorMsg) {
                    
                }
            
                @Override
                public void onActiveSuccess(DeviceBean devResp) {
                    
                }
            
                @Override
                public void onStep(String step, Object data) {
                    
                }
            }
        ));
```
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| uuid            | 设备 UUID ，可通过扫设备二维码获取 |
| homeId          | 家庭 id，详情参考家庭管理章节 |
| timeout         | 配网的超时时间设置，默认是100s ，单位: 秒 |

#### 配网方法调用

```java
ITuyaActivator mTuyaActivator = TuyaHomeSdk.getActivatorInstance().newQRCodeDevActivator(builder);
//开始配网
mTuyaActivator.start();
//停止配网
mTuyaActivator.stop();
//销毁
mTuyaActivator.onDestory();
```
