### Network Configuration for ZigBee Sub-device

#### Description

The network configuration for ZigBee sub-device can be initiated only when the cloud for ZigBee gateway device is online, and the sub-device has been configured.

```sequence
Title: Zigbee sub-device configuration

participant APP
participant SDK
participant Zigbee Gateway
participant Service

Note over Zigbee Gateway: Reset zigbee sub device
APP->SDK: sends the subdevice activation instruction
SDK->Zigbee Gateway: sends the activation instruction

Note over Zigbee Gateway: zigbee gateway receives the activation data

Zigbee Gateway->Service: activate the sub device
Service-->Zigbee Gateway: network configuration succeeds

Zigbee Gateway-->SDK: network configuration succeeds
SDK-->APP: network configuration succeeds

```

#### Initialize Parameters

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
**Parameter Description**

| Parameter         | Description |
| ------------ | -------------------------- |
| mDevId           | Setting the gateway ID |
| timeout         | Setting the time-out period for network configuration |

#### Configuration Method Invocation

```java
ITuyaActivator mTuyaGWActivator = TuyaHomeSdk.getActivatorInstance(). newGwSubDevActivator(builder);
// Start network configuration
mTuyaGWActivator.start();
// Stop network configuration
mTuyaGWActivator.stop();
// Destroy
mTuyaGWActivator.onDestory();
```
