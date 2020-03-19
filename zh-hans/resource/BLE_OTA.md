# 蓝牙第四节——单点设备 OTA
蓝牙设备可以进行 OTA 升级用于更新固件。再进行本章节阅读之前 需要先阅读[第一节](./BLE.md)、[第二节](./BLE_Activator.md) 、[第三节](./BLE_Operator.md) 。

**升级 OTA 流程**

- 检查固件信息
- 升级 OTA

## 检查固件信息

**接口说明**

```java
void requestUpgradeInfo(String devId, IRequestUpgradeInfoCallback callback);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|devId|String|需要升级的设备 devId|
|callback|IRequestUpgradeInfoCallback|检查回调|

**示例代码**
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

`BLEUpgradeBean` 返回固件升级的信息，提供以下信息

| 字段   | 类型   | 描述     |
| ------ | ------ | ------- |
| upgradeStatus | int | 升级状态，0：无新版本 1：有新版本 2：在升级中 |
| version  | String | 最新版本  |
| currentVersion  | String | 当前版本 |
| timeout         | int    | 超时时间，单位：秒  |
| upgradeType     | int    | 0：app 提醒升级 2：app 强制升级 3： 检测升级  |
| type            | int    | 0：wifi设备 1：蓝牙设备 2：GPRS设备 3：zigbee设备 9：MCU |
| typeDesc        | String | 模块描述|
| lastUpgradeTime | long   | 上次升级时间，单位：毫秒   |
| **url** | String   | **新固件下载地址，`type` = `1` 或者 `9` 的时候 有值** |
| fileSize | long   | 新固件大小|
| md5 | String   | 新固件 MD5 值 |

## OTA 升级

需要将上一步检查到有新固件的固件下载到本地后 进行 OTA 升级。

**接口说明**

```java
void startBleOta(String uuid, int type, String version, String binPackagePath, OnBleUpgradeListener listener);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|uuid|String|需要升级的设备 uuid。 `deviceBean.getUuid()`|
|type|int|0：蓝牙固件升级`BLEUpgradeBean.type`=1；  1：mcu 升级`BLEUpgradeBean.type` = 9|
|version|String|新固件版本号|
|binPackagePath|String|下载到本地的固件的 path |
|listener|OnBleUpgradeListener|升级进度回调|
```java
TuyaHomeSdk.getBleManager().startBleOta(uuid, type, version, binPackagePath, new  OnBleUpgradeListener() {
    @Override
    public void onUpgrade(int percent) {
        // 升级进度 百分比
    }

    @Override
    public void onSuccess() {
        //升级成功
    }

    @Override
    public void onFail(String errorCode, String errorMsg) {
        //升级失败
    }
});
```

## 错误码 

升级错误码 见配网部分错误码 [单点蓝牙错误码](./BLE_Activator.md#错误码)

