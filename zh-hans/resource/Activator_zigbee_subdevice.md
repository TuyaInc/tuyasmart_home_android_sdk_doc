### ZigBee 子设备配网

#### 描述

ZigBee 子设备配网需要 ZigBee 网关设备云在线的情况下才能发起,且子设备处于配网状态。

```sequence
Title: ZigBee 子设备激活

participant APP
participant SDK
participant Zigbee 网关
participant Service

Note over Zigbee 网关: 将 ZigBee 子设备重置
APP->SDK: 发送子设备激活指令
SDK->Zigbee 网关: 发送子设备激活指令

Note over Zigbee 网关: 收到子设备激活信息

Zigbee 网关->Service: 通知云端子设备激活
Service-->Zigbee 网关: 子设备激活成功

Zigbee 网关-->SDK: 子设备激活成功
SDK-->APP: 子设备激活成功

```

#### 初始化配网参数

```java
TuyaGwSubDevActivatorBuilder builder = new TuyaGwSubDevActivatorBuilder()
        .setDevId(mDevId)
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
| mDevId          | 设置网关 ID |
| timeout         | 配网的超时时间设置，默认是 100s ，单位是秒 |

#### 配网方法调用

```java
ITuyaActivator mTuyaGWSubActivator = TuyaHomeSdk.getActivatorInstance().newGwSubDevActivator(builder);
//开始配网
mTuyaGWSubActivator.start();
//停止配网
mTuyaGWSubActivator.stop();
//销毁
mTuyaGWSubActivator.onDestory();
```