### ZigBee 网关配网

#### 描述

这里的 ZigBee 网关配网是指有线配网，不用输入路由器的热点名称和密码。
ZigBee 网关配网前，请确保 ZigBee 网关设备连接上外网联通的路由器，并使 ZigBee 网关设备处于配网状态

无线网关请使用 WiFi 配网方式

```sequence
Title: Zigbee 网关配网

participant APP
participant Device
participant Server

Note over Device: 将 Zigbee 网关连上路由器，并置于配网状态
APP --> APP: APP 连上和网关相同的路由器热点
Device-->APP: 发送广播包，待配网设备
APP-->APP: 收到设备信息及 active 状态

APP-->Server: 获取 token
Server-->APP: 返回 token

APP-->Device: 发送激活命令给网关设备
APP-->Server: 根据 token 2秒钟轮询一次入网激活设备列表(总时长默认100s)

Note over Device: 设备收到 APP 激活广播信息

Device->Server: 去云端进行激活
Server-->Device: 激活成功

Server-->APP: 激活成功，返回成功设备列表

```

#### 初始化配网参数

```java
ITuyaActivator mITuyaActivator = TuyaHomeSdk.getActivatorInstance().newGwActivator(
        new TuyaGwActivatorBuilder()
            .setToken(token)
            .setTimeOut(timeout)
            .setContext(context)
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
| token           | 配网所需要的激活 key |
| timeout         | 配网的超时时间设置，默认是100s ，单位是秒|
| context         | 需要传入 activity 的 context |

**获取配网 token**

开始配网之前，SDK 需要在联网状态下从涂鸦云获取配网 Token，Token 的有效期为5分钟，且配置成功后就会失效（再次配网需要重新获取）。

```java
TuyaHomeSdk.getActivatorInstance().getActivatorToken(homeId, 
        new ITuyaActivatorGetToken() {
        
            @Override
            public void onSuccess(String token) {
            
            }
            
            @Override
            public void onFailure(String s, String s1) {
            
            }
        });
```
**参数说明**

| 参数         | 说明 |
| ------------ | -------------------------- |
| homeId          | 家庭 id，详情参考家庭管理章节 |

#### 配网方法调用

```java
ITuyaActivator mITuyaActivator = TuyaHomeSdk.getActivatorInstance().newGwActivator(builder);
//开始配网
mITuyaActivator.start()
//停止配网
mITuyaActivator.stop()
//退出页面清理
mITuyaActivator.onDestroy()
```


