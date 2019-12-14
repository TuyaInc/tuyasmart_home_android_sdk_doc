## Management

### Create SigMesh

MeshId is assigned by the cloud. Only one Mesh can be created in a family.

##### 【Method Invocation】
```java
* @param callback   
void createSigMesh(ITuyaResultCallback<SigMeshBean> callback);
```

##### 【Example Codes】
``` java
TuyaHomeSdk.newHomeInstance("homeId").createSigMesh(new ITuyaResultCallback<SigMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "create sigmesh fail "+ errorMsg, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onSuccess(SigMeshBean sigMeshBean) {
        Toast.makeText(mContext, "create sigmesh success", Toast.LENGTH_LONG).show();
    }
});
```

### Remove SigMesh

##### 【Example Codes】
```java
TuyaHomeSdk.newSigMeshDeviceInstance(meshId).removeMesh(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
	    Toast.makeText(mContext, "remove sigmesh fail "+ errorMsg, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onSuccess() {
	    Toast.makeText(mContext, "remove sigmesh success", Toast.LENGTH_LONG).show();
    }
});

```

### Get Mesh Data From Cache
##### 【Method Invocation】
```java
TuyaHomeSdk.getSigMeshInstance().getSigMeshList()
```
##### 【Method Invocation】
```java
ITuyaHome mTuyaHome = TuyaHomeSdk.newHomeInstance("homeId");
if (mTuyaHome.getHomeBean() != null){
	List<SigMeshBean> meshList = TuyaHomeSdk.getSigMeshInstance().getSigMeshList()
}
```

###  Get Mesh Sub-device Data From Cache 
##### 【Method Invocation】
```java
List<DeviceBean> meshSubDevList = TuyaHomeSdk.newSigMeshDeviceInstance("meshId").getMeshSubDevList();

```


### Mesh Initialization And Destruction
It is recommended to destroy the current mesh and re-initialize the mesh in the family when the family switches

##### 【Method Invocation】
```java
//init mesh
TuyaHomeSdk.getTuyaSigMeshClient().initMesh(String meshId);

//destroy current mesh
TuyaHomeSdk.getTuyaSigMeshClient().destroyMesh();
```


### Mesh Sub-device Connect And Disconnect
##### 【Description】
ITuyaBlueMeshClientProvides start connection, disconnect, start scan, stop scan

##### 【Method Invocation】
```java
// start connection
TuyaHomeSdk.getTuyaSigMeshClient().startClient(mSigMeshBean);

// start connection and specify the time of the scan
TuyaHomeSdk.getTuyaSigMeshClient().startClient(mSigMeshBean,searchTime);

//disconnect
TuyaHomeSdk.getTuyaSigMeshClient().stopClient();

//start scan
TuyaHomeSdk.getTuyaSigMeshClient().startSearch()

//stop scan
TuyaHomeSdk.getTuyaSigMeshClient().stopSearch();

```

##### 【Precautions】
###### startClient(mSigMeshBean) After opening the connection, it will continuously scan the surrounding connectable devices in the background until the connection is successful.
###### startClient(mSigMeshBean,searchTime) After the connection is opened, the device will not be scanned within the search time.
###### Scanning in the background always consumes resources. You can control scanning in the background by startSearch and stopSearch.
###### When startClient () is not started, calling startSearch () and stopSearch () has no effect.
###### When connected to the mesh network, calling startSearch and stopSearch has no effect.