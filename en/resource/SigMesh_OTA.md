# Mesh OTA
There are two types of sub-device upgrades, one is ordinary sub-device upgrade, and the other is mesh gateway upgrade.

## Checking Firmware Information

**Declaration**

```java
void requestUpgradeInfo(String devId, IRequestUpgradeInfoCallback callback);
```

**Parameters**

|param|type|description|
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

|param|type|description|
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


## Sub-device Ordinary Upgrade

**Declaration**

```java
void startOta();
```

**Example**

```java
private MeshUpgradeListener mListener = new MeshUpgradeListener() {
        @Override
        public void onUpgrade(int percent) {
        }

        @Override
        public void onSendSuccess() {
        }

        @Override
        public void onUpgradeSuccess() {
        	 mMeshOta.onDestroy();
        }

        @Override
        public void onFail(String errorCode, String errorMsg) {
        	 mMeshOta.onDestroy();
        }
    };
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

//start
mMeshOta.startOta();
```

**Parameter**

`TuyaBlueMeshOtaBuilder`

|param|type|description|
|--|--|--|
|data|byte[]|Byte stream of the firmware to be upgraded|
|meshId|String|Device MeshId|
|productKey|String|Product Id|
|mNodeId|String|Device NodeId|
|devId|String|Device Id|
|version|String|Version|


## Sub-device Gateway Upgrade

Refer to the gateway upgrade, the following is the sample code

**Example**

```java
private IOtaListener iOtaListener = new IOtaListener() {
        @Override
        public void onSuccess(int otaType) {
  		}

        @Override
        public void onFailure(int otaType, String code, String error) {
        }

        @Override
        public void onProgress(int otaType, final int progress) {     
        }
    };

ITuyaOta iTuyaOta = TuyaHomeSdk.newOTAInstance(mDevID);
iTuyaOta.setOtaListener(mOtaListener);
//start
iTuyaOta.startOta();

//destroy
iTuyaOta.onDestroy();

```