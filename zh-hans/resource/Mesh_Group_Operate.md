# Mesh 群组操作
`ITuyaGroup` 类提供了对 Mesh 群组的操作
## Mesh 群组判断方法

可以通过群组中是否具备 MeshId 来区分 Mesh 群组和普通 Wi-Fi 群组

**代码调用**

```java
GroupBean groupBean=TuyaHomeSdk.getDataInstance().getGroupBean("groupId");
if(!TextUtils.isEmpty(groupBean.getMeshId())){    
	L.d(TAG, "This group is mesh group");
}
```

## 添加子设备到群组

**接口说明**

```java
void addDevice(String devId,IResultCallback callback);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|devId|String|设备 Id|
|callback|IResultCallback|回调|

**示例代码**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.addDevice("devId", new IResultCallback() {
  @Override
  public void onError(String code, String errorMsg) {
  }

  @Override
  public void onSuccess() {
  }
}); 
```


## 从群组中移除子设备
**接口说明**

```java
void removeDevice(String devId,IResultCallback callback);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|devId|String|设备 Id|
|callback|IResultCallback|回调|



**示例代码**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.removeDevice("devId", new IResultCallback() {
  @Override
  public void onError(String code, String errorMsg) {
  }

  @Override
  public void onSuccess() {
  }
});
```

## 解散群组

**接口说明**

```java
void dismissGroup(IResultCallback callback);
```
**参数说明**

|参数|类型|说明|
|--|--|--|
|callback|IResultCallback|回调|

**接口说明**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.dismissGroup(new IResultCallback() {
  @Override
  public void onError(String code, String errorMsg) {
  }

  @Override
  public void onSuccess() {
  }
});
```


## 重命名群组

**接口说明**

```java
void renameGroup(String groupName,IResultCallback callback);
```

**参数说明**

|参数|类型|说明|
|--|--|--|
|groupName|String|重命名名称|
|callback|IResultCallback|回调|

**示例代码**

```java
ITuyaGroup mGroup = TuyaHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.renameGroup("群组名称",new IResultCallback() {
  @Override
  public void onError(String code, String errorMsg) {
  }

  @Override
  public void onSuccess() {
  }
});
```