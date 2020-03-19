# 固件升级

固件升级主要用于修复设备bug和增加设备新功能。固件升级主要分两种，第一种是设备升级，第二种是MCU升级。升级的接口位于ITuyaOta中。
从SDK 2.9.1版本起支持zigbe 子设备升级。

## 查询固件升级信息

**接口说明**

wifi、zigbee网关、摄像头等设备初始化接口

```java
ITuyaOta newOTAInstance(String devId)
```

**参数说明**

| 参数  | 说明   |
| ----- | ------ |
| devId | 设备id |

**接口说明**

子设备初始化接口

```java
ITuyaOta newOTAInstance(String meshId, String devId, String nodeId);
```

**参数说明**

| 参数   | 说明                                           |
| ------ | ---------------------------------------------- |
| meshId | zigbee网关id                                   |
| devId  | zigbee子设备id                                 |
| nodeId | igbee子设备mac地址（从子设备的DeviceBean获取） |

**示例代码**

获取固件升级信息

```java
TuyaHomeSdk.newOTAInstance(mDevId).getOtaInfo(new IGetOtaInfoCallback({
	@Override
	void onSuccess(List<UpgradeInfoBean> list){
	
	}
	@Override
	void onFailure(String code, String error);
	
});

TuyaHomeSdk.newOTAInstance("xxxmeshId","xxxdevId","xxxmac address").getOtaInfo(new IGetOtaInfoCallback({
	@Override
	void onSuccess(List<UpgradeInfoBean> list){
	
	}
	@Override
	void onFailure(String code, String error);
	
});

```

`UpgradeInfoBean`返回固件升级的信息，提供以下信息

| 字段            | 类型   | 描述                                                |
| --------------- | ------ | --------------------------------------------------- |
| upgradeStatus   | int    | 升级状态，0:无新版本 1:有新版本 2:在升级中          |
| version         | String | 最新版本                                            |
| currentVersion  | String | 当前版本                                            |
| timeout         | int    | 超时时间，单位：秒                                  |
| upgradeType     | int    | 0:app提醒升级 2-app强制升级 3-检测升级              |
| type            | int    | 0:wifi设备 1:蓝牙设备 2:GPRS设备 3:zigbee设备 9:MCU |
| typeDesc        | String | 模块描述                                            |
| lastUpgradeTime | long   | 上次升级时间，单位：毫秒                            |

**示例代码**

```java
iTuyaOta.getOtaInfo(new IGetOtaInfoCallback() {
    @Override
    public void onSuccess(List<UpgradeInfoBean> list) {
        
        }
    }

    @Override
    public void onFailure(String code, String error) {
        L.e(TAG, "check error " + code + "----error=" + error);
    }
        });
```

## 设置升级状态回调

ota之前需要注册监听，以实时获取升级状态

**示例代码**

```java
//otaType 升级的设备类型，同`UpgradeInfoBean`的type字段
iTuyaOta.setOtaListener(new IOtaListener() {
    @Override
    public void onSuccess(int otaType) {
        
    }

    @Override
    public void onFailure(int otaType, String code, String error) {

    }

    @Override
    public void onProgress(int otaType, int progress) {

    }
});
```

## 开始升级

 调用该方法开始升级,调用后注册的ota监听会把升级状态返回回来，以便开发者构建UI

**示例代码**

```java
iTuyaOta.startOta();
```

## 销毁

离开升级页面后要销毁，回收内存。

**示例代码**

```java
iTuyaOta.onDestroy();
```

#### 