# Mesh Devices

## Found Mesh Devices

**Example**

```java
DeviceBean deviceBean=TuyaHomeSdk.getDataInstance().getDeviceBean(mDevId);

if(deviceBean.isBlueMesh()){
    L.d(TAG, "This device is blue mesh device");
 }

if(deviceBean.isBlueMeshWifi()){
    L.d(TAG, "This device is blue mesh wifi device");
 }
```
##  Sub-devices Rename

**Declaration**

```java
void renameMeshSubDev(String devId, String name, IResultCallback callback);
```

**Parameters**

|param|type|describe|
|--|--|--|
|devId  |String| Device Id |
|name		|String|New name|
|callback|IResultCallback|Callback|

**Example**

```java
mTuyaBlueMesh.renameMeshSubDev(devBean.getDevId(),"device name", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });
```

##  Sub-devices Remove

**Declaration**

```java
void removeMeshSubDev(String devId, IResultCallback callback);
```
**Parameters**

|param|type|describe|
|--|--|--|
|devId  |String| Device Id |
|pcc		|String|Device type|
|callback|IResultCallback|Callback|

**Example**

```java
mTuyaBlueMesh.removeMeshSubDev(devBean.getDevId(), new IResultCallback(){
  @Override
  public void onError(String code, String errorMsg) {
 }

 @Override
 public void onSuccess() {
  Toast.makeText(mContext, "sub-deivces remove success", Toast.LENGTH_LONG).show();
  }});
```

## Query Single Sub-devices

Get dp data from cloud maybe not real-time data, can use it search real-time data and `IMeshDevListener`'s `onDpUpdate` will be callback.

**Declaration**

```java
void querySubDevStatusByLocal(String pcc, String nodeId, IResultCallback callback);
```

**Parameters**

|param|type|describe|
|--|--|--|
|pcc  |String| Device type |
|nodeId		|String|Device nodeId|
|callback|IResultCallback|Callback|

**Example**

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