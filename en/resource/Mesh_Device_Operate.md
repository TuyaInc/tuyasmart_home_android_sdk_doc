# Mesh Control
`ITuyaBlueMeshDevice` provides operations for Mesh devices.

##  Control Command - Control Devices

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
|:-|--|
|nodeId|Sub-devices No.|
|pcc|Devices type|
|dps|Control command|
|callback|Callback|

**Example**

```java
String dps = {"1":false};
ITuyaBlueMeshDevice mTuyaBlueMeshDevice=TuyaHomeSdk.newBlueMeshDeviceInstance("meshId");
mTuyaBlueMeshDevice.publishDps(devBean.getNodeId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String s, String s1) {
            }

            @Override
            public void onSuccess() {
            }
        });
```
##  Control Command - Control Group

Format： 

```java
{"(dpId)":"(dpValue)"}  
```

**Declaration**

```java
void multicastDps(String localId, String pcc, String dps, IResultCallback callback)
```

**Parameters**

|field|describe|
|--|--|
|localId|Group No.|
|pcc|Device type|
|dps|Control command|
|callback|Callback|

**Example**

```java     
String dps = {"1":false};
ITuyaBlueMeshDevice mTuyaBlueMeshDevice= TuyaHomeSdk.newBlueMeshDeviceInstance("meshId");
mTuyaBlueMeshDevice.multicastDps(groupBean.getLocalId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String errorCode, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```

##  Data Monitor

Mesh info（ dp data、status change、device name、device remove）will real-time sync to `IMeshDevListener` 

**Example**

```java
mTuyaBlueMeshDevice.registerMeshDevListener(new IMeshDevListener() {

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
}});
```


## Create Group
Mesh can create 28672 groups, id in [8000 ~ EFFF]  (Hexadecimal)  and locally maintained.

**Declaration**

```java
void addGroup(String name, String pcc, String localId,IAddGroupCallback callback);
```

**Parameters**

|field|describe|
|--|--|
|name|Group name|
|pcc|Device size|
|localId|Group's localId|
|callback|Callback|

**Example**

```java
mITuyaBlueMesh.addGroup("group name","device size", "8001", new IAddGroupCallback() {
			@Override
            public void onError(String errorCode, String errorMsg) {
            }   
            	
            @Override
            public void onSuccess(long groupId) {
            }
        
        });
```

