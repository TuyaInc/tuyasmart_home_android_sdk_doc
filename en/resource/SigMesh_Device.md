# SigMesh Devices
`ITuyaBlueMeshDevice` provides all operations for Mesh devices.

```java
ITuyaBlueMeshDevice  mTuyaBlueMeshDevice = TuyaHomeSdk.newSigMeshDeviceInstance(meshId);
```

##  Found SigMesh Devices

**Example**

```java
DeviceBean deviceBean=TuyaHomeSdk.getDataInstance().getDeviceBean(mDevId);

if(deviceBean.isSigMesh()){
    L.d(TAG, "This device is sigmesh device");
 }

if(deviceBean.isSigMeshWifi()){
    L.d(TAG, "This device is sigmesh wifi device");
 }
```
## Mesh Device Online Status

**Example**

```java
DeviceBean deviceBean=TuyaHomeSdk.getDataInstance().getDeviceBean(mDevId);

//online status (Including local online and gateway online)
boolean online=deviceBean.getIsOnline()
//local online
boolean localOnline=deviceBean.getIsLocalOnline()
//gateway online
boolean wifiOnline=deviceBean.isCloudOnline() && gwBean.getIsOnline() 
```

##  Sub-devices Rename

**Declaration**

```java
void renameMeshSubDev(String devId, String name, IResultCallback callback);
```
**Parameters**

|param|describe|
|--|--|
|devId|Device Id|
|name|New name|
|callback|Callback|

**Example**

```java
mTuyaBlueMesh.renameMeshSubDev(devBean.getDevId(),"new name", new IResultCallback() {
     @Override
     public void onError(String code, String errorMsg) {
     }

     @Override
     public void onSuccess() {
   }});
```

##  Sub-devices Remove

**Declaration**

```java
void removeMeshSubDev(String devId, IResultCallback callback);
```

**Parameters**

|param|说明|
|--|--|
|devId|Device Id|
|pcc|Device type|
|callback|Callback|

**Example**

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

### Query Single Sub-devices 

Get dp data from cloud maybe not real-time data, can use it search real-time data and `IMeshDevListener`'s `onDpUpdate` will be callback.

**Declaration**

```java
void querySubDevStatusByLocal(String pcc, final String nodeId, final IResultCallback callback);
```

**Parameters**

|param|describe|
|--|--|
|pcc|Device type|
|nodeId|Device nodeId|
|callback|Callback|

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