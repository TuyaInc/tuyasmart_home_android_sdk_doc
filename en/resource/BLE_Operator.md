# Section III——Single BLE Function
This section will introduce activated single-point devices, how to perform status query, connection, unbinding, etc. It is recommended to read Bluetooth  [Section 1](./BLE.md) and [Section 2](./BLE_Activator.md).

**Summary**

1. Device status query
2. Device connection
3. Device sends instructions
4. Modify the device
5. Unbind the device


## Prepare
1. Before developing BLE, you need to understand the basic logic of TuyaHomeSDK. You must already use TuyaHomeSdk to complete the basic operations such as initialization, login, and home creation.
2. After successful activation, you will get `deviceBean` and` devId`, and subsequent operations are mainly based on devId.

## Device Status Query
* The general query is the same as the Wi-Fi device (this status is a comprehensive status, if the Bluetooth device is added under the gateway, the Bluetooth device can be online in the cloud)
```java
TuyaHomeSdk.getDataInstance().getDeviceBean(devId).getIsOnline();
```
* Query if the device is locally connected
```java
TuyaHomeSdk.getBleManager().isBleLocalOnline(devId);
```
> Usually only the local state needs to be considered. Only Bluetooth devices that join the gateway need to consider whether the cloud is online.

## Connect Device
If the device is offline, you can call the connection method to connect the device.

**Declaration**

```java
void addScanLinkTaskIds(String idJsonString);
```

**Parameters**

|param|type|description|
|--|--|--|
|idJsonString|String|devId List to json|

**Example**

```java
 List<String> devIdList = new ArrayList<>();
 devIdList.add(devId1); //devId1
 devIdList.add(devId2); //devId2
 
 String ids = JSONObject.toJSONString(devIdList);
 TuyaHomeSdk.getBleManager().addScanLinkTaskIds(ids);
```

## Device Function
Can monitor device status. This section is similar to Wi-Fi devices, please refer to it for more information [WIFI Function](./Device.md)

#### Device Information Acquisition

Consistent with Wi-Fi device  [Device Information Acquisition](./Device.md#device- information-acquisition)

#### Initial Device Control

Consistent with Wi-Fi device  [Initial Device Control](./Device.md#initial-device-control)

#### Register Device Listener

Consistent with Wi-Fi device  [Register Device Listener](./Device.md#register-device-listener)

#### Unregister Device Listener

Consistent with Wi-Fi device  [Unregister Device Listener](./Device.md#unregister-device-listener)

#### Function Points of Device
Consistent with Wi-Fi device  [Function Points of Device](./Device.md#function-points-of-device)

#### Device Control Method

Unlike Wi-Fi devices, it does not have the LAN delivery function. Only some delivery functions are supported.

**Declaration**

```java
void publishDps(String dps, IControlCallback callback);
```

**Parameters**

|param|type|description|
| ---- |--|--- |
| dps |String|data points|
| callback|IControlCallback|callback|

**Example**

Assuming that the device function point of the light is 101, the control code of the light is as follows:
	
```java
mDevice.publishDps("{\"101\": true}", new IControlCallback() {
    @Override
    public void onError(String code, String error) {
    }
	
    @Override
    public void onSuccess() {
    }
});
}
```

#### Rename Device

Consistent with Wi-Fi device  [Rename Device](./Device.md#rename-device)

#### Remove Device

Consistent with Wi-Fi device  [Remove Device](./Device.md#remove-device)

> The unbinding of Bluetooth devices is consistent with the Wi-Fi device.
> `TuyaHomeSdk.newDeviceInstance("devId").removeDevice()` or `resetFactory()` 
> But in addition to BLE cloud removal. If the device is locally connected at this time, the device will be automatically removed. If the device is offline at this time, only the cloud will be removed.

#### Recycling Device Resources

Consistent with Wi-Fi device  [Recycling Device Resources](./Device.md#recycling-device-resources)
