### Network Configuration for ZigBee Gateway

#### Description

The ZigBee Gateway distribution network here refers to the ZigBee Wired Gateway.
Before the ZigBee Gateway is configured, please ensure that the ZigBee Gateway device is connected to the router on the network, and the ZigBee gateway device is in the network configuration state.

Please use Wi-Fi Configuration for ZigBee Wireless Gateway

```sequence
Title: Zigbee Gateway Configuration

participant APP
participant ZigBee Gateway
participant Service

Note over ZigBee Gateway: Reset ZigBee Gateway

APP-->Service: Get Token
Service-->APP: Response Token

APP -> APP: connect mobile phone to the same hotspot of the Gateway

Device-->APP: broadcast configuration data
APP-->APP: Receive Gateway information and active status

APP-->ZigBee Gateway: sends the activation instruction
APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

Note over ZigBee Gateway: device receives the activation data

ZigBee Gateway->Service: activate the device
Service-->ZigBee Gateway: network configuration succeeds

Server-->APP: Network configuration succeeds
```

#### Initialize Parameters

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
**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| timeout         | Configuration timeout, default setting is 100s, unit is second|
| context         | context |

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Tuya Cloud.
The term of validity of Token is 5 minutes, and the Token become invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure network.

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
**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| homeId          | Family ID, please refer to the family management section for details |

#### Configuration Method Invocation

```java
ITuyaActivator mITuyaActivator = TuyaHomeSdk.getActivatorInstance().newGwActivator(builder);
//开始配网
mITuyaActivator.start()
//停止配网
mITuyaActivator.stop()
//退出页面清理
mITuyaActivator.onDestroy()
```


