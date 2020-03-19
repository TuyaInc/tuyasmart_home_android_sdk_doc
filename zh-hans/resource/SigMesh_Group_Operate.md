# 群组
`ITuyaGroup` 类提供了对 Mesh 群组的操作

## Mesh 群组判断方法

**描述**

可以通过群组中是否具备 MeshId 来区分 Mesh 群组和普通 WiFi 群组

**代码示例**

```java
GroupBean groupBean=TuyaHomeSdk.getDataInstance().getGroupBean("groupId");
if(!TextUtils.isEmpty(groupBean.getMeshId())){    
   L.d(TAG, "This group is mesh group");
}
```

## 创建群组

**描述**

一个 Mesh 网内支持创建 16128 个群组  返回时 id 范围  C000 - FEFF （16 进制）  由本地进行维护

**接口说明**

```java
void addGroup(String name, String pcc, String localId,IAddGroupCallback callback);
```
**参数说明**

|参数|说明|
|--|--|
|name|群组名称|
|pcc|群组中设备的大小类  (支持跨小类创建)|
|localId|群组的 localId (范围 C000 - FEFF 16 进制字符串)|
|callback|回调|

**代码示例**

```java
ITuyaBlueMeshDevice mTuyaSigMeshDevice= TuyaHomeSdk.newSigMeshDeviceInstance("meshId");
mTuyaSigMeshDevice.addGroup("群组名称","大小类", "8001", new IAddGroupCallback() {
			@Override
     public void onError(String errorCode, String errorMsg) {
     }

     @Override
     public void onSuccess(long groupId) {
     }
});
```



## 添加子设备到群组

**接口说明**

```java
void addDevice(String devId,IResultCallback callback);
```
**参数说明**

|参数|说明|
|--|--|
|devId|设备 Id|
|callback|回调|

**代码示例**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.addDevice("devId", new IResultCallback() {
   @Override
   public void onError(String code, String errorMsg) {
      Toast.makeText(mContext, "添加设备到群组失败 "+ errorMsg, Toast.LENGTH_LONG).show();
   }

   @Override
   public void onSuccess() {
      Toast.makeText(mContext, "添加设备到群组成功 ", Toast.LENGTH_LONG).show();
   }
});
```


### 从群组中移除子设备

**接口说明**

```java
void removeDevice(String devId,IResultCallback callback);
```
**参数说明**

|参数|说明|
|--|--|
|devId|设备 Id|
|callback|回调|

**代码示例**
```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.removeDevice("devId", new IResultCallback() {
   @Override
   public void onError(String code, String errorMsg) {
   }
   @Override
   public void onSuccess() {
   }
});
```

### 解散群组

**接口说明**

```java
void dismissGroup(IResultCallback callback);
```
**参数说明**

|参数|说明|
|--|--|
|callback|回调|

**代码示例**
```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.dismissGroup(new IResultCallback() {
   @Override
   public void onError(String code, String errorMsg) {
   }

   @Override
   public void onSuccess() {
   }
});
```


### 重命名群组

**接口说明**

```java
void renameGroup(String groupName,IResultCallback callback);
```

**参数说明**

|参数|说明|
|--|--|
|groupName|重命名名称|
|callback|回调|

**代码示例**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.renameGroup("群组名称",new IResultCallback() {
   @Override
   public void onError(String code, String errorMsg) {
   }

   @Override
   public void onSuccess() {
   }
});
```