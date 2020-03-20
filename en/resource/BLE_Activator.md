# Section II——BLE Device Scanning and Activation
This section will introduce the scanning and activation of Tuya single-point equipment and dual-mode equipment. It is recommended to read [Section 1](./BLE.md)
## Prepare
Before developing BLE, you need to understand the basic logic of TuyaHomeSDK. You must already use TuyaHomeSdk to complete the basic operations such as initialization, login, and home creation.

## Scanning Device
Unactivated Bluetooth devices will send Bluetooth broadcast packets to the surroundings, and the SDK will analyze the broadcast packets according to the protocol to find the surrounding Tuya Bluetooth single-point devices and dual-mode devices.

> Remind again: permissions check is required before scanning,  **Only permissions allowable can work**
> 1、The Phone Bluetooth is on
> 2、APP has positioning permission

**Declaration**

```java
void startLeScan(int timeout, ScanType type, TyBleScanResponse response);
```
**Parameters**

| param    | description  |
| ----------- | ---------- |
|timeout|Activation timeout, unit ms, 60s recommended|
|type|ScanType.SINGLE|
|response|calback,can not be empty|

**Example**

```java
TuyaHomeSdk.getBleOperator().startLeScan(60000, ScanType.SINGLE, new    TyBleScanResponse() {
            @Override
            public void onResult(ScanDeviceBean bean) {
                
            }
        });

```

**Callback Description** 

`ScanDeviceBean` description

|Attributes|description|
|:---|---|
|id|Scan ID usually consists of uuid, which can uniquely distinguish the device|
|name|Bluetooth name of the device, usually blank|
|providerName|SingleBleProvider|
|data|raw data|
|**configType**|config_type_single：single Device;config_type_wifi:Dual-mode device|
|productId|product id|
|uuid|product uuid,Device unique code|
|mac|device mac|
|isbind|binding status|
|flag|bit0:Whether to support 5G Wi-Fi|

## Stop Scanning
Stop scanning devices, such as exiting the activation page

**Declaration**

```java
void stopLeScan();
```

**Example**

```java
TuyaHomeSdk.getBleOperator().stopLeScan();
```

## Single BLE Device Activation
Scanned devices `configType = config_type_single` represents a single BLE device. `config_type_wifi` is a dual-mode device.

**Declaration**

```java
void startBleConfig(long homeId, String devUuid, Map<String, Object> params, ITuyaBleConfigListener configListener);
```
**Parameters**

|param|description|
|--|--|
|homeId|Current home's Id|
|devUuid|ScanDeviceBean.uuid|
|params|null,not need by SingleBLE|
|configListener|callback|

**Example**

```java
TuyaHomeSdk.getBleManager().startBleConfig(123456, "abc12345678", null, new ITuyaBleConfigListener() {
            @Override
            public void onSuccess(DeviceBean bean) {

            }

            @Override
            public void onFail(String code, String msg, Object handle) {
               // code msg ,see #Error Code
            }
        });
```
## Cancel Activation
Stop it during Activation.

**Declaration**

```java
void stopBleConfig(String devUuid);
```
**Parameters**

|param|description|
|--|--|
|devUuid|ScanDeviceBean.uuid|

**Example**

```java
TuyaHomeSdk.getBleManager().stopBleConfig("abc12345678");
```

## Dual-mode Device Activation
Scanned devices `configType = config_type_single` represents a single BLE device. `config_type_wifi` is a dual-mode device.

**Declaration**
```java
void startBleConfig(long homeId, String devUuid, Map<String, Object> params, ITuyaBleConfigListener configListener);
```
**Parameters**

|param|description|
|--|--|
|homeId|Current home's Id|
|devUuid|ScanDeviceBean.uuid|
|params|Wi-Fi Network information: ssid, pwd, token|
|configListener|callback|
> If not specified, The Device only support 2.4G Wi-Fi network, and some devices support 5G. Can be determined based on `ScanDeviceBean.flag`.
> token: The way to obtain the token is the same as  the Wi-Fi device. [Get Token](./Activator_wifi.md#get-network-configuration-token)

**Example**

```java
 Map<String, Object> param = new HashMap<>();
  param.put("ssid", "Tuya-Wi-Fi-2.4G"); //Wi-Fi ssid
  param.put("password", "12345678"); //Wi-Fi pwd
  param.put("token", "xxxxxxxxxxxxx"); // user token
TuyaHomeSdk.getBleManager().startBleConfig(123456, "xyz12345678", param, new ITuyaBleConfigListener() {
            @Override
            public void onSuccess(DeviceBean bean) {
            }

            @Override
            public void onFail(String code, String msg, Object handle) {
            // code msg ,see #ErrorCode
            }
        });
```

**Callback Description**

`DeviceBean` Description
See [DeviceBean Data Model](./Device.md#device-information-acquisition)

## Cancel Dual-mode Device Activation
Stop it during Activation.

**Declaration**

```java
void stopBleConfig(String devUuid);
```

**Parameters**

|param|description|
|--|--|
|devUuid|ScanDeviceBean.uuid|

**Example**

```java
TuyaHomeSdk.getBleManager().stopBleConfig("xyz12345678");
```
## Error Code

|code|description|
|--|--|
|1|Format of the packet received by the device is incorrect |
|2|The device cannot find the router|
|3|Wi-Fi password error|
|4|Device cannot connect to router|
|5|Device DHCP failed|
|6|The device fails to connect to the cloud|
|100|User cancels activation|
|101|Bluetooth connection error|
|102|Bluetooth service error found|
|103|Failed to open Bluetooth communication channel|
|104|Bluetooth failed to get device information|
|105|Bluetooth pairing failed|
|106|Activation timeout|
|107|Wi-Fi information transmission failed|
|108|Token is invalid|
|109|Failed to get Bluetooth encryption key|
|110|Device does not exist|
|111|Device cloud registration failed|
|112|Device cloud activation failed|
|113|Cloud device has been bound|
|114|Active disconnect|
|115|Failed to get device information in the cloud|
|116|The device is being networked by other methods at this time|
|117|OTA upgrade failed|
|118|OTA upgrade timeout|
|119|Wi-Fi parameter verification failed|

