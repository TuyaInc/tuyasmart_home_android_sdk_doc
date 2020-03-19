# SigMesh Manager
Contains MeshId creation, destruction

## Create SigMesh

MeshId is created by the cloud. Only one Mesh can be created in a family.

**Declaration**
```java
void createSigMesh(ITuyaResultCallback<SigMeshBean> callback);
```

**Example**

```java
TuyaHomeSdk.newHomeInstance("homeIdxxxx").createSigMesh(new ITuyaResultCallback<SigMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onSuccess(SigMeshBean sigMeshBean) {
    }
});
```

## Delete SigMesh
Delete SigMesh MeshId

**Declaration**
```java
void removeMesh(IResultCallback callback);
```

**Example**
```java
TuyaHomeSdk.newSigMeshDeviceInstance(meshId).removeMesh(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onSuccess() {
    }
});

```

## Get Mesh Data From Cache

**Declaration**

```java
List<SigMeshBean> getSigMeshList();
```
**Example**
```java
ITuyaHome mTuyaHome = TuyaHomeSdk.newHomeInstance("homeIdxxxx");
if (mTuyaHome.getHomeBean() != null){
	List<SigMeshBean> meshList = TuyaHomeSdk.getSigMeshInstance().getSigMeshList()
}
```

## Get Sub-device Data From Cache 

**Declaration**

```java
 List<DeviceBean> getMeshSubDevList();
```
**Example**
```java
List<DeviceBean> meshSubDevList = TuyaHomeSdk.newSigMeshDeviceInstance("meshIdxxxxx").getMeshSubDevList();
```

## Mesh Init  & Destroy
It is recommended to destroy the current mesh and re-initialize the mesh when the family switches.

**Declaration**
```java
//init mesh
void initMesh(String meshId);
//destroy current mesh
void destroyMesh();
```
**Example**
```java
//init mesh
TuyaHomeSdk.getTuyaSigMeshClient().initMesh("meshIdxxxxx");

//destroy current mesh
TuyaHomeSdk.getTuyaSigMeshClient().destroyMesh();
```

## Mesh Sub-device Connect and disconnect
`ITuyaBlueMeshClient` provides connect, disconnect, scan, stop scan.

**Example**
```java
// start connect
TuyaHomeSdk.getTuyaSigMeshClient().startClient(mSigMeshBean);
// start connect with timeout
TuyaHomeSdk.getTuyaSigMeshClient().startClient(mSigMeshBean,searchTime);

//disconnect
TuyaHomeSdk.getTuyaSigMeshClient().stopClient();

//start scan
TuyaHomeSdk.getTuyaSigMeshClient().startSearch()

//stop scan
TuyaHomeSdk.getTuyaSigMeshClient().stopSearch();

```

**Precautions**

 - `startClient(mSigMeshBean)` After calling, it will continuously scan the surrounding connectable devices in the background until the connection is successful.
 - Scanning in the background always consumes resources. You can control background scanning by starting and stopping
 - if not call  `startClient()` , `startSearch()` and  `stopSearch()` is not working
 - When connected to the Mesh network, calling startSearch and stopSearch is not working.
