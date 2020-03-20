### EZ 模式

```sequence
Title: EZ 配网

participant APP
participant Device
participant Server

Note over APP: 连上路由器
Note over Device: Wi-Fi 灯快闪

APP-->Server: 获取 token
Server-->APP: 返回 token

Note over APP: 开始配网，通过广播、组播循环发 ssid/pwd/token
Device->Device: 捕捉到 ssid/password/token

APP-->Server: 根据 token 2 秒钟轮询一次入网激活设备列表(总时长默认 100s)

Device-->Server: 去激活设备
Server-->Device: 激活成功

Server-->APP: 激活成功，返回成功设备列表

```
#### 初始化配网参数

```java
ActivatorBuilder builder = new ActivatorBuilder()
        .setSsid(ssid)
        .setContext(context)
        .setPassword(password)
        .setActivatorModel(ActivatorModelEnum.TY_EZ)
        .setTimeOut(timeout)
        .setToken(token)
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
| context         | 需要传入 activity 的 context |
| ssid            | 配网之后，设备工作WiFi的名称（家庭网络）|
| password        | 配网之后，设备工作WiFi的密码（家庭网络）|
| activatorModel  | 配网模式，EZ 模式请传入：ActivatorModelEnum.TY_EZ |
| timeout         | 配网的超时时间设置，默认是 100s，单位是秒 |

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
ITuyaActivator mTuyaActivator = TuyaHomeSdk.getActivatorInstance().newMultiActivator(builder);
//开始配网
mTuyaActivator.start();
//停止配网
mTuyaActivator.stop(); 
//退出页面销毁一些缓存和监听
mTuyaActivator.onDestroy(); 
```