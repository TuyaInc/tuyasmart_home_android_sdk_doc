# Management
### Create Mesh

##### 【Method Invocation】
```java
* @param meshName   mesh name（no more than 16 bytes）
* @param callback   
void createBlueMesh(String meshName, ITuyaResultCallback<BlueMeshBean> callback);
```

##### 【Example Codes】
``` java
TuyaHomeSdk.newHomeInstance("homeId").createBlueMesh("meshName", new ITuyaResultCallback<BlueMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "create mesh fail "+ errorMsg, Toast.LENGTH_LONG).show();
    }

    @Override	
    public void onSuccess(BlueMeshBean blueMeshBean) {
        Toast.makeText(mContext, "creat mesh success", Toast.LENGTH_LONG).show();
    }
});
```

### Remove Mesh

##### 【Example Codes】
```java
TuyaHomeSdk.newBlueMeshDeviceInstance(meshId).removeMesh(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
	    Toast.makeText(mContext, "remove mesh fail "+ errorMsg, Toast.LENGTH_LONG).show();
    }
	
    @Override
    public void onSuccess() {
	    Toast.makeText(mContext, "remove mesh success ", Toast.LENGTH_LONG).show();
    }
});

```

### Get Mesh Data From Cache
##### 【Method Invocation】
```java
TuyaHomeSdk.newHomeInstance("homeId").getHomeBean().getMeshList()
```
##### 【Example Codes】
```java
ITuyaHome mTuyaHome = TuyaHomeSdk.newHomeInstance("homeId");
if (mTuyaHome.getHomeBean() != null){
	List<BlueMeshBean> meshList = mTuyaHome.getHomeBean().getMeshList();
	BlueMeshBean meshBean= meshList.get(0);
}            
```

###  Get Mesh Sub-device Data From Cache 
##### 【Example Codes】
```java
List<DeviceBean> meshSubDevList = TuyaHomeSdk.newBlueMeshDeviceInstance("meshId").getMeshSubDevList();
    
```


### Mesh Initialization And Destruction
建议在家庭切换的时候 销毁当前mesh  然后重新初始化家庭中的mesh

##### 【Method Invocation】
```java
//初始化mesh
TuyaHomeSdk.getTuyaBlueMeshClient().initMesh(String meshId);       

//销毁当前mesh
TuyaHomeSdk.getTuyaBlueMeshClient().destroyMesh();       
```


### Mesh Sub-device Connect And Disconnect
##### 【Description】
ITuyaBlueMeshClientProvides start connection, disconnect, start scan, stop scan

##### 【Method Invocation】

```java
// start connection
TuyaHomeSdk.getTuyaBlueMeshClient().startClient(mBlueMeshBean);

//disconnect
TuyaHomeSdk.getTuyaBlueMeshClient().stopClient();

//start scan
TuyaHomeSdk.getTuyaBlueMeshClient().startSearch()

//stop scan
TuyaHomeSdk.getTuyaBlueMeshClient().stopSearch();

```

##### 【Precautions】 
###### startClient(mSigMeshBean) After opening the connection, it will continuously scan the surrounding connectable devices in the background until the connection is successful.

###### startClient(mSigMeshBean,searchTime) After the connection is opened, the device will not be scanned within the search time.

###### Scanning in the background always consumes resources. You can control scanning in the background by startSearch and stopSearch.

###### When startClient () is not started, calling startSearch () and stopSearch () has no effect.

###### When connected to the mesh network, calling startSearch and stopSearch has no effect.