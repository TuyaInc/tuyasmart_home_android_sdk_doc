# Section IV——Single BLE OTA
Bluetooth devices can be OTA upgraded for firmware update. Before reading this chapter, you need to read [Section 1](./BLE.md), [Section 2](./BLE_Activator.md), and [Section 3](./BLE_Operator.md).

**OTA process**

- Checking firmware information
- Upgrade OTA

## Checking Firmware Information

**Declaration**

```java
void requestUpgradeInfo(String devId, IRequestUpgradeInfoCallback callback);
```

**Parameters**

| Parameters |type|description|
|--|--|--|
|devId|String|devId|
|callback|IRequestUpgradeInfoCallback|callback|

**Example**

```java
TuyaHomeSdk.getMeshInstance().requestUpgradeInfo(mDevID, new IRequestUpgradeInfoCallback() {
    @Override
    public void onSuccess(ArrayList<BLEUpgradeBean> bleUpgradeBeans) {
       
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
    }
});
```

`BLEUpgradeBean`  data model

| Parameters |type|description|
|------|------|-------|
|upgradeStatus|int|0: No new version 1: New version available 2: In upgrade|
|version| String|Latest version|
|currentVersion| String |Current version|
|timeout| int| timeout, Unit s|
|upgradeType|int|0:Reminds to upgrade 2: Forced upgrade 3: Detect upgrade|
|type|int|0: Wi-Fi 1: BLE  2: GPRS 3: Zigbee 9: MCU|
|typeDesc| String |Upgrade description|
|lastUpgradeTime|long|Last upgrade time|
|**url**|String|New firmware download url, `type` =` 1` or `9` has value|
|fileSize|long|New firmware size|
|md5|String|New firmware MD5 value|

## OTA Upgrade

You need to download the  new firmware to the local, in the previous step, and then perform OTA upgrade.

**Declaration**

```java
void startBleOta(String uuid, int type, String version, String binPackagePath, OnBleUpgradeListener listener);
```

**Parameters**

| Parameters |type|description|
|--|--|--|
|uuid|String| `deviceBean.getUuid()`|
|type|int|0: means `BLEUpgradeBean.type` = 1; 1: means` BLEUpgradeBean.type` = 9|
|version|String|New firmware version|
|binPackagePath|String|Local firmware path |
|listener|OnBleUpgradeListener|callback|
```java
TuyaHomeSdk.getBleManager().startBleOta(uuid, type, version, binPackagePath, new  OnBleUpgradeListener() {
        @Override
        public void onUpgrade(int percent) {

        }

        @Override
        public void onSuccess() {

        }

        @Override
        public void onFail(String errorCode, String errorMsg) {

        }
    });
```

## Error Code 

Upgrade error code, See  [Bluetooth Error Code](./BLE_Activator.md#error-code)

