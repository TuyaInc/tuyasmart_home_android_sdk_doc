# 检查固件信息
子设备升级分为 2 种，一种是普通子设备升级，一种是 Mesh 网关升级

**接口说明**

```java
void requestUpgradeInfo(String devId, IRequestUpgradeInfoCallback callback);
```
**参数说明**

|参数|说明|
|--|--|
|devId|需要升级的设备 devId|
|callback|检查回调|

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

`BLEUpgradeBean`返回固件升级的信息，提供以下信息

| 字段   | 类型   | 描述     |
| ------ | ------ | ------- |
| upgradeStatus | int | 升级状态，0：无新版本 1：有新版本 2：在升级中 |
| version  | String | 最新版本  |
| currentVersion  | String | 当前版本 |
| timeout         | int    | 超时时间，单位：秒  |
| upgradeType     | int    | 0：app 提醒升级 2：app 强制升级 3：检测升级  |
| type            | int    | 0：wifi设备 1：蓝牙设备 2：GPRS设备 3：zigbee设备 9：MCU |
| typeDesc        | String | 模块描述|
| lastUpgradeTime | long   | 上次升级时间，单位：毫秒   |
| **url** | String   | **新固件下载地址，type = 1 或者 9 的时候 有值** |
| fileSize | long   | 新固件大小|
| md5 | String   | 新固件 MD5 值|


### 普通子设备升级

**升级接口**

```java
void startOta();
```

**示例代码**

```java
private MeshUpgradeListener mListener = new MeshUpgradeListener() {
        @Override
        public void onUpgrade(int percent) {
        	//升级进度
        }

        @Override
        public void onSendSuccess() {
        	//固件数据发送成功
        }

        @Override
        public void onUpgradeSuccess() {
        	//升级成功
        	 mMeshOta.onDestroy();
        }

        @Override
        public void onFail(String errorCode, String errorMsg) {
        	//升级失败
        	 mMeshOta.onDestroy();
        }
    };
//获取指定文件的字节流
byte data[] = getFromFile(path);

TuyaBlueMeshOtaBuilder build = new TuyaBlueMeshOtaBuilder()
        .setData(data)
        .setMeshId(mDevBean.getMeshId())
        .setProductKey(mDevBean.getProductId())
        .setNodeId(mDevBean.getNodeId())
        .setDevId(mDevID)
        .setVersion("version")
        .setTuyaBlueMeshActivatorListener(mListener)
        .bulid();
ITuyaBlueMeshOta  = TuyaHomeSdk.newMeshOtaManagerInstance(build);

//开始升级
mMeshOta.startOta();
```

**入参说明**

`TuyaBlueMeshOtaBuilder`

|参数|类型|说明|
|--|--|--|
|data|byte[]|待升级固件的字节流|
|meshId|String|设备 MeshId|
|productKey|String|设备产品 Id|
|mNodeId|String|设备 NodeId|
|devId|String|设备 Id|
|version|String|待升级固件的版本号|


### 网关设备升级

参考网关升级，以下为示例代码

**示例代码**

```java
private IOtaListener iOtaListener = new IOtaListener() {
        @Override
        public void onSuccess(int otaType) {
            //升级成功
  		}

        @Override
        public void onFailure(int otaType, String code, String error) {
         	//升级失
        }

        @Override
        public void onProgress(int otaType, final int progress) {
           //升级进度         
        }
    };

ITuyaOta iTuyaOta = TuyaHomeSdk.newOTAInstance(mDevID);
iTuyaOta.setOtaListener(mOtaListener);
//开始升级
iTuyaOta.startOta();

//销毁升级
iTuyaOta.onDestroy();

```