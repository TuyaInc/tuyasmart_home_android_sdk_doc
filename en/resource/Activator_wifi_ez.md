### EZ Mode Configuration

```sequence
Title: EZ Mode

participant APP
participant Device
participant Service

Note over APP: Connect to the WiFi of router
Note over Device: Switch to the EZ mode

APP-->Service: Get Token
Service-->APP: Response Token

Note over APP: Start network configuration (send configuration data), broadcast configuration data
Device->Device: Get configuration data

APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

Device->Service: Activate the device
Service-->Device: Network configuration succeeds

Server-->APP: Network configuration succeeds
```

#### Initialize Parameters

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
**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| context         | context |
| ssid            | WiFi ssid|
| password        | WiFi password|
| activatorModel  | Configuration Mode，EZ Mode：ActivatorModelEnum.TY_EZ |
| timeout         | Configuration timeout, default setting is 100s, unit is second|

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
ITuyaActivator mTuyaActivator = TuyaHomeSdk.getActivatorInstance().newMultiActivator(builder);
//Start configuration
mTuyaActivator.start();
//Stop configuration
mTuyaActivator.stop(); 
//Exit the page to destroy some cache data and monitoring data.
mTuyaActivator.onDestroy(); 
```