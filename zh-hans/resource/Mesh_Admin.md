# Mesh 管理
##  创建 Mesh

**接口说明**
```java
void createBlueMesh(String meshName, ITuyaResultCallback<BlueMeshBean> callback);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|meshName|String|mesh 的名称（不超过 16 字节）|
|callback|ITuyaResultCallback|回调|

**示例代码**

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

## 删除 Mesh

**接口说明**

```java
void removeMesh(IResultCallback callback);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|callback|IResultCallback|回调|


**示例代码**

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

## 从缓存中获取 Mesh 数据
**接口说明**

```java
List<BlueMeshBean> getMeshList();
```
**示例代码**
```java
ITuyaHome mTuyaHome = TuyaHomeSdk.newHomeInstance("homeId");
if (mTuyaHome.getHomeBean() != null){
	List<BlueMeshBean> meshList = mTuyaHome.getHomeBean().getMeshList();
	BlueMeshBean meshBean= meshList.get(0);
}            
```

## 从缓存中获取 Mesh 下的子设备数据
**接口说明**

```java
List<DeviceBean> getMeshSubDevList();
```
**示例代码**

```java
List<DeviceBean> meshSubDevList = TuyaHomeSdk.newBlueMeshDeviceInstance("meshId").getMeshSubDevList();
```


## Mesh 初始化和销毁
建议在家庭切换的时候 销毁当 Mesh  然后重新初始化家庭中的 Mesh

**接口调用**

```java
//初始化mesh
TuyaHomeSdk.getTuyaBlueMeshClient().initMesh(String meshId);       

//销毁当前mesh
TuyaHomeSdk.getTuyaBlueMeshClient().destroyMesh();       
```


## Mesh 子设备连接和断开
ITuyaBlueMeshClient 提供 开始连接、断开连接、开启扫描、停止扫描

**接口调用**

```java
// 开启连接
TuyaHomeSdk.getTuyaBlueMeshClient().startClient(mBlueMeshBean);

//断开连接
TuyaHomeSdk.getTuyaBlueMeshClient().stopClient();

//开启扫描
TuyaHomeSdk.getTuyaBlueMeshClient().startSearch()

//停止扫描
TuyaHomeSdk.getTuyaBlueMeshClient().stopSearch();

```

**注意事项** 

 -  开启连接后，会在后台不断的去扫描周围可连接设备，直到连接成功为止。
 -  后台一直扫描会消耗资源，可以通过通过开启扫描和停止扫描来控制后台的扫描
 -  当未 `startClient()` 时候，调用 `startSearch()` 和 `stopSearch()` 是没有效果的
 -  当已经连接到 Mesh 网的时候，调用 `startSearch()` 和 `stopSearch()` 是没有效果的

