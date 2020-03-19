# 管理
包含 MeshId 创建

## 创建 SigMesh

由云端分配 MeshId，一个家庭下只能创建一个 Mesh。

**接口方法**
```java
void createSigMesh(ITuyaResultCallback<SigMeshBean> callback);
```

**示例代码**

```java
TuyaHomeSdk.newHomeInstance("homeIdxxxx")
  .createSigMesh(new ITuyaResultCallback<SigMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onSuccess(SigMeshBean sigMeshBean) {
    }
});
```

## 删除 SigMesh
删除 SigMesh MeshId

**接口方法**
```java
void removeMesh(IResultCallback callback);
```

**示例代码**
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

## 从缓存中获取 Mesh 数据
**接口说明**
```java
List<SigMeshBean> getSigMeshList();
```
**示例代码**
```java
ITuyaHome mTuyaHome = TuyaHomeSdk.newHomeInstance("homeIdxxxx");
if (mTuyaHome.getHomeBean() != null){
	List<SigMeshBean> meshList = TuyaHomeSdk.getSigMeshInstance().getSigMeshList()
}
```

## 从缓存中获取 Mesh 下的子设备数据
**接口说明**
```java
List<DeviceBean> getMeshSubDevList();
```
**示例代码**
```java
List<DeviceBean> meshSubDevList = TuyaHomeSdk.newSigMeshDeviceInstance("meshIdxxxxx").getMeshSubDevList();
```

## Mesh 初始化
建议在家庭切换的时候 销毁当前 Mesh  然后重新初始化家庭中的 Mesh。

**接口说明**
```java
void initMesh(String meshId);
```
**示例代码**
```java
TuyaHomeSdk.getTuyaSigMeshClient().initMesh("meshIdxxxxx");
```
## Mesh 销毁
**接口说明**

```java
void destroyMesh();
```
**示例代码**
```java
TuyaHomeSdk.getTuyaSigMeshClient().destroyMesh();
```

## Mesh 子设备连接和断开
`ITuyaBlueMeshClient` 提供 开始连接、断开连接、开启扫描、停止扫描

**代码示例**
```java
// 开启连接
TuyaHomeSdk.getTuyaSigMeshClient().startClient(mSigMeshBean);
// 开启连接 指定扫描的时间 
TuyaHomeSdk.getTuyaSigMeshClient().startClient(mSigMeshBean,searchTime);

//断开连接
TuyaHomeSdk.getTuyaSigMeshClient().stopClient();

//开启扫描
TuyaHomeSdk.getTuyaSigMeshClient().startSearch()

//停止扫描
TuyaHomeSdk.getTuyaSigMeshClient().stopSearch();

```

**注意事项**

 - `startClient(mSigMeshBean)` 开启连接后，会在后台不断的去扫描周围可连接设备，直到连接成功为止。
 - `startClient(mSigMeshBean,searchTime)` 开启连接后， `searchTime` 时间内没有扫描到设备就停止扫描.
 - 后台一直扫描会消耗资源，可以通过通过开启扫描和停止扫描来控制后台的扫描
 - 当未 `startClient()` 时候，调用 `startSearch()` 和 `stopSearch()` 是没有效果的
 - 当已经连接到 Mesh 网的时候，调用 `startSearch` 和 `stopSearch` 是没有效果的
