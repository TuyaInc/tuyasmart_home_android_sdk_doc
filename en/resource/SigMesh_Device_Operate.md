# SigMesh Control
`ITuyaBlueMeshDevice` provides operations for Mesh devices.

###  Control Command - Control Devices

Format： 
```java
{"(dpId)":"(dpValue)"}  
```

**Declaration**

```java
void publishDps(String nodeId, String pcc, String dps, IResultCallback callback);
```

**Parameters**

|param|describe|
|--|--|
|nodeId|Sub-devices No.|
|pcc|Devices type|
|dps|dps|
|callback|Callback|

**Example**

```java
String dps = {"1":false};
ITuyaBlueMeshDevice mTuyaSigMeshDevice=TuyaHomeSdk.newSigMeshDeviceInstance("meshId");
mTuyaSigMeshDevice.publishDps(devBean.getNodeId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String s, String s1) {
            }

            @Override
            public void onSuccess() {
            }
        });
```

###  Control Command - Control Group

**Declaration**

```java
void multicastDps(String localId, String pcc, String dps, IResultCallback callback)
```

**Parameters**

|param|describe|
|--|--|
|localId|Group No.|
|pcc|Device type|
|dps|dps|
|callback|Callback|

**Example**

```java      
String dps = {"1":false};
ITuyaBlueMeshDevice mTuyaSigMeshDevice= TuyaHomeSdk.newSigMeshDeviceInstance("meshId");
mTuyaSigMeshDevice.multicastDps(groupBean.getLocalId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String errorCode, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```
###  Data Monitor

Mesh info（ dp data、status change、device name、device remove）will real-time sync to `IMeshDevListener` 

**Example**

```java
mTuyaSigMeshDevice.registerMeshDevListener(new IMeshDevListener() {

@Override
public void onDpUpdate(String nodeId, String dps,boolean isFromLocal) {
    DeviceBean deviceBean = mTuyaBlueMeshDevice.getMeshSubDevBeanByNodeId(nodeId);
}
  
@Override
public void onStatusChanged(List<String> online, List<String> offline,String gwId) {
}
 
@Override
public void onNetworkStatusChanged(String devId, boolean status) {
      
}        

@Override
public void onRawDataUpdate(byte[] bytes) {

}
         
@Override
public void onDevInfoUpdate(String devId) {
}  

@Override
public void onRemoved(String devId) {
}
});
```

