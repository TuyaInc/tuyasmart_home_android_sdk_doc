## Mesh 设备

## Mesh 设备判断方法

**使用方法**

```java
DeviceBean deviceBean=TuyaHomeSdk.getDataInstance().getDeviceBean(mDevId);
// blue mesh 设备判断 （子设备+网关）
if(deviceBean.isBlueMesh()){
    L.d(TAG, "This device is blue mesh device");
 }

// blue mesh 网关设备判断
if(deviceBean.isBlueMeshWifi()){
    L.d(TAG, "This device is blue mesh wifi device");
}
```
##  子设备重命名

**接口说明**

```java
void renameMeshSubDev(String devId, String name, IResultCallback callback);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|devId  |String| 设备 Id|
|name		|String|重命名名称|
|callback|IResultCallback|回调|

**代码示例**
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

|参数|类型|说明|
|--|--|--|
|devId  |String| 设备 Id|
|pcc		|String|设备大小类|
|callback|IResultCallback|回调|

**代码示例**

```java
mTuyaBlueMesh.removeMeshSubDev(devBean.getDevId(), new IResultCallback(){
  @Override
  public void onError(String code, String errorMsg) {
    Toast.makeText(mContext, "子设备移除失败 "+ errorMsg,     Toast.LENGTH_LONG).show();
  }

  @Override
  public void onSuccess() {
    Toast.makeText(mContext, "子设备移除成功", Toast.LENGTH_LONG).show();
  }
});
```

## 单个子设备信息查询

云端获取到的 dp 点数据可能不是当前设备实时的数据，可以通过该命令去查询设备的当前数据值，结果通过 `IMeshDevListener` 的 `onDpUpdate` 方法返回

**接口说明**

```java
void querySubDevStatusByLocal(String pcc, String nodeId, IResultCallback callback);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|pcc  |String| 设备大小类|
|nodeId		|String|设备 nodeId|
|callback|IResultCallback|回调|

**代码示例**

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