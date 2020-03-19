# Mesh Manager
##  Create Mesh

**Declaration**

```java
void createBlueMesh(String meshName, ITuyaResultCallback<BlueMeshBean> callback);
```
**Parameters**

|field|type|describe|
|--|--|--|
|meshName|String|mesh's name（limit 16）|
|callback|ITuyaResultCallback|callback|

**Example**

``` java
TuyaHomeSdk.newHomeInstance("homeId").createBlueMesh("meshName", new ITuyaResultCallback<BlueMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override	
    public void onSuccess(BlueMeshBean blueMeshBean) {
    }
});
```

## Delete Mesh

**Declaration**

```java
void removeMesh(IResultCallback callback);
```
**Parameters**

|field|type|describe|
|--|--|--|
|callback|IResultCallback|callback|

**Example**

```java
TuyaHomeSdk.newBlueMeshDeviceInstance(meshId).removeMesh(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }
	
    @Override
    public void onSuccess() {
    }
});

```

## Get Data of Mesh From Cache
**Declaration**

```java
List<BlueMeshBean> getMeshList();
```
**Example**

```java
ITuyaHome mTuyaHome = TuyaHomeSdk.newHomeInstance("homeId");
if (mTuyaHome.getHomeBean() != null){
	List<BlueMeshBean> meshList = mTuyaHome.getHomeBean().getMeshList();
	BlueMeshBean meshBean= meshList.get(0);
}            
```

## Get Data of Mesh's Sub-devices From Cache 
**Declaration**

```java
List<DeviceBean> getMeshSubDevList();
```
**Example**

```java
List<DeviceBean> meshSubDevList = TuyaHomeSdk.newBlueMeshDeviceInstance("meshId").getMeshSubDevList();
    
```


## Mesh Init and Destroy
recommend to destroy the Mesh and re-initialize the Mesh in the family when the family switches.

**Example**

```java
//init
TuyaHomeSdk.getTuyaBlueMeshClient().initMesh(String meshId);       

//destroy
TuyaHomeSdk.getTuyaBlueMeshClient().destroyMesh();       
```


## Mesh Sub-devices's Connect and Disconnect
ITuyaBlueMeshClient has start connecting, disconnect, start scanning, stop scanning.

**Example**

```java
//start connecting
TuyaHomeSdk.getTuyaBlueMeshClient().startClient(mBlueMeshBean);

//disconnect
TuyaHomeSdk.getTuyaBlueMeshClient().stopClient();

//start scanning
TuyaHomeSdk.getTuyaBlueMeshClient().startSearch()

//stop scanning
TuyaHomeSdk.getTuyaBlueMeshClient().stopSearch();

```

**Precautions** 

 -  Start connecting and will be scanning the connectable devices in the background until the connection is successful.
 -  Scanning always consumes resources, can control scanning by turning on scanning and stopping scanning.
 -  Use `startSearch()` or `stopSearch()` must be after calling `startClient()`.
 -   `startSearch()` or `stopSearch()` will be not working when connected to the Mesh.

