# 设备
ITuyaBlueMeshDevice 类封装了对指定 Mesh 内所有设备的操作

```java
ITuyaBlueMeshDevice  mTuyaBlueMeshDevice = TuyaHomeSdk.newSigMeshDeviceInstance(meshId);
```

## SigMesh 设备和网关判断方法

**示例代码**

```java
DeviceBean deviceBean=TuyaHomeSdk.getDataInstance().getDeviceBean(mDevId);
// 判读是否是 sigmesh 设备 （子设备+网关）
if(deviceBean.isSigMesh()){
    L.d(TAG, "This device is sigmesh device");
}

// 判读是否是 sigmesh 网关设备
if(deviceBean.isSigMeshWifi()){
    L.d(TAG, "This device is sigmesh wifi device");
}
```
## Mesh 设备在线状态判断方法

**示例代码**

```java
DeviceBean deviceBean=TuyaHomeSdk.getDataInstance().getDeviceBean(mDevId);

//在线状态  (包括本地在线和网关在线)
boolean online=deviceBean.getIsOnline()
//设备本地蓝牙在线状态
boolean localOnline=deviceBean.getIsLocalOnline()
//设备网关在线状态  (需要网关在线)
boolean wifiOnline=deviceBean.isCloudOnline() && gwBean.getIsOnline() 
```

##  子设备重命名

**接口说明**

```java
void renameMeshSubDev(String devId, String name, IResultCallback callback);
```
**参数说明**

|参数|说明|
|--|--|
|devId|设备 Id|
|name|重命名名称|
|callback|回调|

**示例代码**

```java
mTuyaBlueMesh.renameMeshSubDev(devBean.getDevId(),"设备名称", new IResultCallback() {
     @Override
     public void onError(String code, String errorMsg) {
     }

     @Override
     public void onSuccess() {
     }
});
```

##  子设备移除

**接口说明**

```java
void removeMeshSubDev(String devId, IResultCallback callback);
```

**参数说明**

|参数|说明|
|--|--|
|devId|设备 Id|
|pcc|设备大小类|
|callback|回调|

**示例代码**
```java
mTuyaBlueMesh.removeMeshSubDev(devBean.getDevId(),devBean.getCategory(), new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }
            @Override
            public void onSuccess() {
            }
        });
```

### 单个子设备信息查询

云端获取到的 dp 点数据可能不是当前设备实时的数据，可以通过该命令去查询设备的当前数据值，结果通过 `IMeshDevListener` 的 `onDpUpdate` 方法返回

**接口说明**

```java
void querySubDevStatusByLocal(String pcc, final String nodeId, final IResultCallback callback);
```

**参数说明**

|参数|说明|
|--|--|
|pcc|设备大小类|
|nodeId|设备 nodeId|
|callback|回调|

**示例代码**
```java
mTuyaBlueMeshDevice.querySubDevStatusByLocal(devBean.getCategory(), devBean.getNodeId(), new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }
            @Override
            public void onSuccess() {
            }
        });
```