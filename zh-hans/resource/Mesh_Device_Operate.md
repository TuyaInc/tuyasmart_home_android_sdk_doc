

# Mesh 控制
`ITuyaBlueMeshDevice` 类提供了对 Mesh 设备的操作

##  控制指令下发-控制设备

发送控制指令按照以下格式： 
```java
{"(dpId)":"(dpValue)"}  
```
**接口说明**

```java
void publishDps(String nodeId, String pcc, String dps, IResultCallback callback);
```

**参数说明**

|参数|说明|
|--|--|
|nodeId|子设备本地编号|
|pcc|设备产品大小类|
|dps|控制指令|
|callback|回调|

**示例代码**

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
##  控制指令下发-控制群组

发送控制指令按照以下格式： 

```java
{
  "(dpId)":"(dpValue)"
}  
```

**接口说明**

```java
void multicastDps(String localId, String pcc, String dps, IResultCallback callback)
```

**参数说明**

|参数|说明|
|--|--|
|localId|群组本地编号|
|pcc|设备产品大小类|
|dps|控制指令|
|callback|回调|


**示例代码**

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

##  数据监听

Mesh 网内相关信息（ dp 数据、状态变更、设备名称、设备移除）会实时同步到 `IMeshDevListener` 

**示例代码**

```java
mTuyaBlueMeshDevice.registerMeshDevListener(new IMeshDevListener() {

   /**
    * 数据更新
    * @param nodeId    更新设备的nodeId
    * @param dps       dp数据
    * @param isFromLocal   数据来源 true表示从本地蓝牙  false表示从云端
    */
   @Override
   public void onDpUpdate(String nodeId, String dps,boolean isFromLocal) {
   //可以通过node来找到相对应的DeviceBean
   DeviceBean deviceBean = mTuyaBlueMeshDevice.getMeshSubDevBeanByNodeId(nodeId);
   }

   /**
    * 设备状态的上报
    * @param online    在线设备列表
    * @param offline   离线设备列表
    * @param gwId      状态的来源 gwId不为空表示来自云端（gwId是上报数据的网关Id）   为空则表示来自本地蓝牙
    */
   @Override
   public void onStatusChanged(List<String> online, List<String> offline,String gwId) {
   }

   /**
    * 网络状态变化
    * @param devId
    * @param status
    */
   @Override
   public void onNetworkStatusChanged(String devId, boolean status) {

   }

   /**
    * raw类型数据上报
    * @param bytes
    */
   @Override
   public void onRawDataUpdate(byte[] bytes) {

   }

   /**
    * 设备信息变更（名称等）
    * @param bytes
    */            
   @Override
   public void onDevInfoUpdate(String devId) {
   }
   /**
    * 设备移除
    * @param devId
    */
   @Override
   public void onRemoved(String devId) {
   }
});
```


## 创建群组
Mesh 网内支持创建 28672 个群组  返回时 id 范围 8000 ~ EFFF  （ 16 进制）  由本地进行维护

**接口说明**

```java
void addGroup(String name, String pcc, String localId,IAddGroupCallback callback);
```

**参数说明**

|参数|说明|
|--|--|
|name|群组名称|
|pcc|群组中设备的大小类  (支持跨小类创建  FF01 表示覆盖灯大类)|
|localId|群组的 localId  (范围 8000 ~ EFFF 16 进制字符串)|
|callback|回调|

**示例代码**

```java
mITuyaBlueMesh.addGroup("群组名称","大小类", "8001", new IAddGroupCallback() {
   @Override
   public void onError(String errorCode, String errorMsg) {
   }   

   @Override
   public void onSuccess(long groupId) {
   }
});
```

